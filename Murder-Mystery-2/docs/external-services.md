# External Services, Remotes and Hooks

All network destinations, game remotes, hooks, and hardware overlay APIs used by [`main.luau`](../main.luau).

## Network

| Target | Line | Purpose |
| --- | --- | --- |
| WindUI Mirror Fallbacks (`raw.githubusercontent.com`, `fastly.jsdelivr.net`, `cdn.jsdelivr.net`, `github.com releases`) | 630-935 | UI library loader with multi-source download retries and raw-source disk caching (`Foxname/WindUI_cache.lua`). Only reached if local cache is absent or corrupt. |
| `raw.githubusercontent.com/Footagesus/Icons/main/Main-v2.lua` | 8768, 12842 | Lucide icon module (`loadstring`). |
| `raw.githubusercontent.com/FoxnameTeam/OSS/main/Murder-Mystery-2/icons/<file>` | 12703 | Mobile touch button PNG icons (stored in [icons/](../icons)). Guarded by local disk validation (`isfile` + PNG magic byte check) to eliminate redundant HTTP calls. |
| `raw.githubusercontent.com/FoxnameTeam/OSS/development/Murder-Mystery-2/main.luau` | 11334 | Script re-execution URL for server hops (`queue_on_teleport`) on the `development` branch. |
| `discord.com/api/v10/invites/v8ZPq4y2nD` | 1177 | Community member counts and guild metadata. |
| `cdn.discordapp.com/icons/<id>/<icon>.png?size=1024` | 1206 | Discord server icon displayed on the community tab paragraph. |
| `games.roblox.com/v1/games/<id>/servers/Public` | 11425 | Public server browser API for server hopping. |
| `roblox.com/headshot-thumbnail/...` | 8338 | Avatar preview for Discord webhook embeds. |
| User-configured Discord Webhook | 8321, 17232 | Optional coin farm status notifications. |

## Hardware Overlays (Potassium / Drawing APIs)

| API | Line | Purpose |
| --- | --- | --- |
| `DrawingImmediate.GetPaint` / `DrawingImmediate.Line` | 9163-9172 | Direct GPU hardware rendering for ESP snaplines without GuiObject allocations or ScreenGui canvas dirtying. |
| `DrawingImmediate.GetPaint` / `DrawingImmediate.Circle` | 21895-21904 | Direct GPU hardware rendering for Aimlock FOV circle with smooth rainbow color cycling. |
| `Drawing.new("Line")` / `Drawing.new("Circle")` | 9198, 21915 | Standard executor Drawing fallback when `DrawingImmediate` is unavailable. |
| GuiObject `Frame` + `UIStroke` | 9209, 21931 | Universal fallback for executors without native Drawing APIs. |

## Removed External Calls & Checks

- **Ban list & HWID telemetry**: Stripped. The script does not read `gethwid()` or query ban lists.
- **Inventory rarity scanner / payload loader**: Stripped. `foxnameRunIndependentCheck` and remote payload queries have been deleted.
- **Admin action tracking**: `Hub.ProcessedAdminActions` and arbitrary third-party release URLs (`xv3gasx/Murder-Mystery-2`) replaced with standard open-source repository endpoints.

## Game Remotes

| Path | Line | Purpose |
| --- | --- | --- |
| `ReplicatedStorage.Remotes.Inventory.GetProfileData` | 2176 | Read player level and profile XP. |
| `ReplicatedStorage.Remotes.Inventory.Prestige` | 2225 | Auto Prestige event trigger. |
| `ReplicatedStorage.Remotes.*.CoinCollected` | 10690 | Coin collection listener in farm engine. |
| `ReplicatedStorage.Remotes.*.LoadingMap` | 10755 | Map change detection. |
| Fake Bomb `.Remote` | 12187 | Bomb Jump launch impulse. |
| `playSong` | 15499 | FE Radio playback remote. |
| `ReplicatedStorage.GetIcons` (instantiated by script) | 616-625 | Client-side icon resolution bridge. |

## Metamethod Hooks

| Line | Hook | Purpose |
| --- | --- | --- |
| 14634 | `hookmetamethod(game, "__namecall", ...)` | Emote synchronization (`PlayEmote`, `PlayEmoteAndGetAnimTrackById`). |
| 22209 | `hookmetamethod(game, "__namecall", ...)` | Silent aim weapon redirection. Active only when `silentAimSupported` is true. |

Both hooks check `checkcaller()` to ensure internal executor calls are never intercepted.
