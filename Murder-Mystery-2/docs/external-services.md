# External Services, Remotes and Hooks

All network destinations, game remotes, and hooks used by [`main.luau`](../main.luau).

## Network

| Target | Line | Purpose |
| --- | --- | --- |
| WindUI Mirror Fallbacks (`raw.githubusercontent.com`, `fastly.jsdelivr.net`, `cdn.jsdelivr.net`, `github.com releases`) | 489-560 | UI library loader with multi-source download retries and local disk caching (`Foxname/WindUI_cache.lua`). |
| `raw.githubusercontent.com/Footagesus/Icons/main/Main-v2.lua` | 7438, 11322 | Lucide icon module (`loadstring`). |
| `raw.githubusercontent.com/FoxnameTeam/OSS/main/Murder-Mystery-2/icons/<file>` | 11204 | Mobile touch button PNG icons (stored in [icons/](../icons)). |
| `raw.githubusercontent.com/FoxnameTeam/OSS/main/Murder-Mystery-2/main.luau` | 9832 | Script re-execution URL for server hops (`queue_on_teleport`). |
| `discord.com/api/v10/invites/v8ZPq4y2nD` | 868 | Community member counts. |
| `cdn.discordapp.com/icons/...` | 899 | Community Discord icon. |
| `games.roblox.com/v1/games/<id>/servers/Public` | 9922 | Public server browser API for server hopping. |
| `roblox.com/headshot-thumbnail/...` | 7019 | Avatar preview for Discord webhook embeds. |
| User-configured Discord Webhook | 7022, 15668 | Optional coin farm status notifications. |

## Removed External Calls & Checks

- **Ban list & HWID telemetry**: Stripped. The script does not read `gethwid()` or query ban lists.
- **Inventory rarity scanner / payload loader**: Stripped. `foxnameRunIndependentCheck` and remote payload queries have been deleted.
- **Admin action tracking**: `Hub.ProcessedAdminActions` and arbitrary third-party release URLs (`xv3gasx/Murder-Mystery-2`) replaced with standard open-source repository endpoints.

## Game Remotes

| Path | Line | Purpose |
| --- | --- | --- |
| `ReplicatedStorage.Remotes.Inventory.GetProfileData` | 1865 | Read player level and profile XP. |
| `ReplicatedStorage.Remotes.Inventory.Prestige` | 1967 | Auto Prestige event trigger. |
| `ReplicatedStorage.Remotes.*.CoinCollected` | 9202 | Coin collection listener in farm engine. |
| `ReplicatedStorage.Remotes.*.LoadingMap` | 9267 | Map change detection. |
| Fake Bomb `.Remote` | 10686 | Bomb Jump launch impulse. |
| `playSong` | 13934 | FE Radio playback remote. |
| `ReplicatedStorage.GetIcons` (instantiated by script) | 480-488 | Client-side icon resolution bridge. |

## Metamethod Hooks

| Line | Hook | Purpose |
| --- | --- | --- |
| 13102 | `hookmetamethod(game, "__namecall", ...)` | Emote synchronization (`PlayEmote`, `PlayEmoteAndGetAnimTrackById`). |
| 20525 | `hookmetamethod(game, "__namecall", ...)` | Silent aim weapon redirection. Active only when `silentAimSupported` is true. |

Both hooks check `checkcaller()` to ensure internal executor calls are never intercepted.
