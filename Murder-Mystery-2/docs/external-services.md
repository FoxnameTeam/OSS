# External Services, Remotes and Hooks

All network destinations, game remotes, and hooks used by [`main.luau`](../main.luau).

## Network

| Target | Line | Purpose |
| --- | --- | --- |
| `github.com/Footagesus/WindUI/releases/latest/download/main.lua` | 536, 556 | UI library (`loadstring`). |
| `raw.githubusercontent.com/Footagesus/Icons/main/Main-v2.lua` | 6168, 10022 | Lucide icon module (`loadstring`). |
| `raw.githubusercontent.com/FoxnameTeam/OSS/main/Murder-Mystery-2/icons/<file>` | 9904 | Mobile touch button PNG icons (stored in [icons/](../icons)). |
| `raw.githubusercontent.com/FoxnameTeam/OSS/main/Murder-Mystery-2/main.luau` | 8750 | Script re-execution URL for server hops (`queue_on_teleport`). |
| `discord.com/api/v10/invites/v8ZPq4y2nD` | 768 | Community member counts. |
| `cdn.discordapp.com/icons/...` | 799 | Community Discord icon. |
| `games.roblox.com/v1/games/<id>/servers/Public` | 8842 | Public server browser API for server hopping. |
| `roblox.com/headshot-thumbnail/...` | 5948 | Avatar preview for Discord webhook embeds. |
| User-configured Discord Webhook | 5901, 14488 | Optional coin farm status notifications. |

## Removed External Calls & Checks

- **Ban list & HWID telemetry**: Stripped. The script does not read `gethwid()` or query ban lists.
- **Inventory rarity scanner / payload loader**: Stripped. `foxnameRunIndependentCheck` and remote payload queries have been deleted.
- **Admin action tracking**: `Hub.ProcessedAdminActions` and arbitrary third-party release URLs (`xv3gasx/Murder-Mystery-2`) replaced with standard open-source repository endpoints.

## Game Remotes

| Path | Line | Purpose |
| --- | --- | --- |
| `ReplicatedStorage.Remotes.Inventory.GetProfileData` | 1521 | Read player level and profile XP. |
| `ReplicatedStorage.Remotes.Inventory.Prestige` | 1623 | Auto Prestige event trigger. |
| `ReplicatedStorage.Remotes.*.CoinCollected` | 7951 | Coin collection listener in farm engine. |
| `ReplicatedStorage.Remotes.*.LoadingMap` | 8016 | Map change detection. |
| Fake Bomb `.Remote` | 9607, 9734 | Bomb Jump launch impulse. |
| `playSong` | 12992 | FE Radio playback remote. |
| `ReplicatedStorage.GetIcons` (instantiated by script) | 509-516 | Client-side icon resolution bridge. |

## Metamethod Hooks

| Line | Hook | Purpose |
| --- | --- | --- |
| 11774 | `hookmetamethod(game, "__namecall", ...)` | Emote synchronization (`PlayEmote`, `PlayEmoteAndGetAnimTrackById`). |
| 18859 | `hookmetamethod(game, "__namecall", ...)` | Silent aim weapon redirection. Active only when `silentAimSupported` is true. |

Both hooks check `checkcaller()` to ensure internal executor calls are never intercepted.
