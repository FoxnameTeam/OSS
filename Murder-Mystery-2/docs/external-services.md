# External Services, Remotes and Hooks

All network destinations, game remotes, and hooks used by [`main.luau`](../main.luau).

## Network

| Target | Line | Purpose |
| --- | --- | --- |
| WindUI Mirror Fallbacks (`raw.githubusercontent.com`, `fastly.jsdelivr.net`, `cdn.jsdelivr.net`, `github.com releases`) | 501-570 | UI library loader with multi-source download retries and local disk caching (`Foxname/WindUI_cache.lua`). |
| `raw.githubusercontent.com/Footagesus/Icons/main/Main-v2.lua` | 6289, 10143 | Lucide icon module (`loadstring`). |
| `raw.githubusercontent.com/FoxnameTeam/OSS/main/Murder-Mystery-2/icons/<file>` | 10025 | Mobile touch button PNG icons (stored in [icons/](../icons)). |
| `raw.githubusercontent.com/FoxnameTeam/OSS/main/Murder-Mystery-2/main.luau` | 8870 | Script re-execution URL for server hops (`queue_on_teleport`). |
| `discord.com/api/v10/invites/v8ZPq4y2nD` | 885 | Community member counts. |
| `cdn.discordapp.com/icons/...` | 916 | Community Discord icon. |
| `games.roblox.com/v1/games/<id>/servers/Public` | 8962 | Public server browser API for server hopping. |
| `roblox.com/headshot-thumbnail/...` | 6069 | Avatar preview for Discord webhook embeds. |
| User-configured Discord Webhook | 6022, 14654 | Optional coin farm status notifications. |

## Removed External Calls & Checks

- **Ban list & HWID telemetry**: Stripped. The script does not read `gethwid()` or query ban lists.
- **Inventory rarity scanner / payload loader**: Stripped. `foxnameRunIndependentCheck` and remote payload queries have been deleted.
- **Admin action tracking**: `Hub.ProcessedAdminActions` and arbitrary third-party release URLs (`xv3gasx/Murder-Mystery-2`) replaced with standard open-source repository endpoints.

## Game Remotes

| Path | Line | Purpose |
| --- | --- | --- |
| `ReplicatedStorage.Remotes.Inventory.GetProfileData` | 1962 | Read player level and profile XP. |
| `ReplicatedStorage.Remotes.Inventory.Prestige` | 2064 | Auto Prestige event trigger. |
| `ReplicatedStorage.Remotes.*.CoinCollected` | 8071 | Coin collection listener in farm engine. |
| `ReplicatedStorage.Remotes.*.LoadingMap` | 8136 | Map change detection. |
| Fake Bomb `.Remote` | 9727, 9854 | Bomb Jump launch impulse. |
| `playSong` | 13230 | FE Radio playback remote. |
| `ReplicatedStorage.GetIcons` (instantiated by script) | 480-488 | Client-side icon resolution bridge. |

## Metamethod Hooks

| Line | Hook | Purpose |
| --- | --- | --- |
| 11894 | `hookmetamethod(game, "__namecall", ...)` | Emote synchronization (`PlayEmote`, `PlayEmoteAndGetAnimTrackById`). |
| 19115 | `hookmetamethod(game, "__namecall", ...)` | Silent aim weapon redirection. Active only when `silentAimSupported` is true. |

Both hooks check `checkcaller()` to ensure internal executor calls are never intercepted.
