# External Services, Remotes and Hooks

All network destinations, game remotes, hooks, and hardware overlay APIs used by [`main.luau`](../main.luau).

## Network

| Target | Line | Purpose |
| --- | --- | --- |
| WindUI Mirror Fallbacks (`raw.githubusercontent.com`, `fastly.jsdelivr.net`, `cdn.jsdelivr.net`, `github.com releases`) | 790-868 | UI library loader with multi-source download retries and disk-first caching (`Foxname/WindUI_cache.lua`). Only reached if local cache is absent or corrupt. |
| `raw.githubusercontent.com/Footagesus/Icons/main/Main-v2.lua` | 8718, 12746 | Lucide icon module (`loadstring`). |
| `raw.githubusercontent.com/FoxnameTeam/OSS/main/Murder-Mystery-2/icons/<file>` | 12607 | Mobile touch button PNG icons (stored in [icons/](../icons)). Guarded by local disk validation (`isfile` + PNG magic byte check) to eliminate redundant HTTP calls. |
| `raw.githubusercontent.com/FoxnameTeam/OSS/development/Murder-Mystery-2/main.luau` | 11239 | Script re-execution URL for server hops (`queue_on_teleport`) on the `development` branch. |
| `discord.com/api/v10/invites/v8ZPq4y2nD` | 1140 | Community member counts. |
| `games.roblox.com/v1/games/<id>/servers/Public` | 11329 | Public server browser API for server hopping. |
| `roblox.com/headshot-thumbnail/...` | 8288 | Avatar preview for Discord webhook embeds. |
| User-configured Discord Webhook | 8291, 17159 | Optional coin farm status notifications. |

## Hardware Overlays (Potassium / Drawing APIs)

| API | Line | Purpose |
| --- | --- | --- |
| `DrawingImmediate.GetPaint` / `DrawingImmediate.Line` | 9107-9125 | Direct GPU hardware rendering for ESP snaplines without GuiObject allocations or ScreenGui canvas dirtying. |
| `DrawingImmediate.GetPaint` / `DrawingImmediate.Circle` | 21795-21814 | Direct GPU hardware rendering for Aimlock FOV circle with smooth rainbow color cycling. |
| `Drawing.new("Line")` / `Drawing.new("Circle")` | 9137, 21818 | Standard executor Drawing fallback when `DrawingImmediate` is unavailable. |
| GuiObject `Frame` + `UIStroke` | 9149, 21833 | Universal fallback for executors without native Drawing APIs. |

## Removed External Calls & Checks

- **Ban list & HWID telemetry**: Stripped. The script does not read `gethwid()` or query ban lists.
- **Inventory rarity scanner / payload loader**: Stripped. `foxnameRunIndependentCheck` and remote payload queries have been deleted.
- **Admin action tracking**: `Hub.ProcessedAdminActions` and arbitrary third-party release URLs (`xv3gasx/Murder-Mystery-2`) replaced with standard open-source repository endpoints.

## Game Remotes

| Path | Line | Purpose |
| --- | --- | --- |
| `ReplicatedStorage.Remotes.Inventory.GetProfileData` | 2136 | Read player level and profile XP. |
| `ReplicatedStorage.Remotes.Inventory.Prestige` | 2224 | Auto Prestige event trigger. |
| `ReplicatedStorage.Remotes.*.CoinCollected` | 10595 | Coin collection listener in farm engine. |
| `ReplicatedStorage.Remotes.*.LoadingMap` | 10660 | Map change detection. |
| Fake Bomb `.Remote` | 12100 | Bomb Jump launch impulse. |
| `playSong` | 15403 | FE Radio playback remote. |
| `ReplicatedStorage.GetIcons` (instantiated by script) | 600-665 | Client-side icon resolution bridge. |

## Metamethod Hooks

| Line | Hook | Purpose |
| --- | --- | --- |
| 14538 | `hookmetamethod(game, "__namecall", ...)` | Emote synchronization (`PlayEmote`, `PlayEmoteAndGetAnimTrackById`). |
| 22114 | `hookmetamethod(game, "__namecall", ...)` | Silent aim weapon redirection. Active only when `silentAimSupported` is true. |

Both hooks check `checkcaller()` to ensure internal executor calls are never intercepted.
