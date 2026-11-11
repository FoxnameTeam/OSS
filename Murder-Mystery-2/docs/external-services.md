# External Services, Remotes and Hooks

All network destinations, game remotes, hooks, and hardware overlay APIs used by [`main.luau`](../main.luau).

## Network

| Target | Line | Purpose |
| --- | --- | --- |
| WindUI Mirror Fallbacks (`raw.githubusercontent.com`, `fastly.jsdelivr.net`, `cdn.jsdelivr.net`, `github.com releases`) | 588-645 | UI library loader with multi-source download retries and disk-first caching (`Foxname/WindUI_cache.lua`). Only reached if local cache is absent or corrupt. |
| `raw.githubusercontent.com/Footagesus/Icons/main/Main-v2.lua` | 7497, 11462 | Lucide icon module (`loadstring`). |
| `raw.githubusercontent.com/FoxnameTeam/OSS/main/Murder-Mystery-2/icons/<file>` | 11343 | Mobile touch button PNG icons (stored in [icons/](../icons)). Guarded by local disk validation (`isfile` + PNG magic byte check) to eliminate redundant HTTP calls. |
| `raw.githubusercontent.com/FoxnameTeam/OSS/main/Murder-Mystery-2/main.luau` | 9970 | Script re-execution URL for server hops (`queue_on_teleport`). |
| `discord.com/api/v10/invites/v8ZPq4y2nD` | 876 | Community member counts. |
| `cdn.discordapp.com/icons/...` | 907 | Community Discord icon. |
| `games.roblox.com/v1/games/<id>/servers/Public` | 10062 | Public server browser API for server hopping. |
| `roblox.com/headshot-thumbnail/...` | 7037 | Avatar preview for Discord webhook embeds. |
| User-configured Discord Webhook | 7040, 15805 | Optional coin farm status notifications. |

## Hardware Overlays (Potassium / Drawing APIs)

| API | Line | Purpose |
| --- | --- | --- |
| `DrawingImmediate.GetPaint` / `DrawingImmediate.Line` | 7896-7909 | Direct GPU hardware rendering for ESP snaplines without GuiObject allocations or ScreenGui canvas dirtying. |
| `DrawingImmediate.GetPaint` / `DrawingImmediate.Circle` | 20562-20573 | Direct GPU hardware rendering for Aimlock FOV circle with smooth rainbow color cycling. |
| `Drawing.new("Line")` / `Drawing.new("Circle")` | 7925, 20556 | Standard executor Drawing fallback when `DrawingImmediate` is unavailable. |
| GuiObject `Frame` + `UIStroke` | 7937, 20440 | Universal fallback for executors without native Drawing APIs. |

## Removed External Calls & Checks

- **Ban list & HWID telemetry**: Stripped. The script does not read `gethwid()` or query ban lists.
- **Inventory rarity scanner / payload loader**: Stripped. `foxnameRunIndependentCheck` and remote payload queries have been deleted.
- **Admin action tracking**: `Hub.ProcessedAdminActions` and arbitrary third-party release URLs (`xv3gasx/Murder-Mystery-2`) replaced with standard open-source repository endpoints.

## Game Remotes

| Path | Line | Purpose |
| --- | --- | --- |
| `ReplicatedStorage.Remotes.Inventory.GetProfileData` | 1865 | Read player level and profile XP. |
| `ReplicatedStorage.Remotes.Inventory.Prestige` | 1951 | Auto Prestige event trigger. |
| `ReplicatedStorage.Remotes.*.CoinCollected` | 9261 | Coin collection listener in farm engine. |
| `ReplicatedStorage.Remotes.*.LoadingMap` | 9326 | Map change detection. |
| Fake Bomb `.Remote` | 10826 | Bomb Jump launch impulse. |
| `playSong` | 14074 | FE Radio playback remote. |
| `ReplicatedStorage.GetIcons` (instantiated by script) | 480-488 | Client-side icon resolution bridge. |

## Metamethod Hooks

| Line | Hook | Purpose |
| --- | --- | --- |
| 13242 | `hookmetamethod(game, "__namecall", ...)` | Emote synchronization (`PlayEmote`, `PlayEmoteAndGetAnimTrackById`). |
| 20658 | `hookmetamethod(game, "__namecall", ...)` | Silent aim weapon redirection. Active only when `silentAimSupported` is true. |

Both hooks check `checkcaller()` to ensure internal executor calls are never intercepted.
