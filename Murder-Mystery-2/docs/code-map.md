# Code Map

Line ranges for [`main.luau`](../main.luau) (19,547 lines). Ranges mark boundaries of each functional block.

## Top to bottom

| Lines | Block | Notes |
| --- | --- | --- |
| 1-19 | GPLv3 license header | Full GNU GPLv3 license notice and reminder. |
| 20-29 | Loading notification | `task.defer` + `StarterGui:SetCore("SendNotification")`. |
| 31-32 | `genv` | `getgenv and getgenv() or _G`. |
| 34-72 | Clipboard & kick helpers | `FoxnameCopyToClipboard`, `FoxnameKickPlayer`. |
| 74-99 | Shared locals & executor detection | `hookSupported`, `silentAimSupported`, `Tabs`, `UI_BUILD_DELAY = 0.08`. |
| 100-126 | Runtime single-instance guard | `genv.__FoxnameMM2Runtime`, session id, duplicate run notification. |
| 128-560 | Compatibility report & feature checks | Executor environment detection, compatibility scoring. |
| 560-658 | WindUI setup & icons bridge | `GetIcons` RemoteFunction bridge, WindUI loader. |
| 659-700 | `Window = WindUI:CreateWindow` | Window creation, gradient title, release tag. |
| 701-760 | Tab initialization | Sidebar section, every `Window:Tab`, `Tabs` alias table. |
| 765-890 | Discord & compatibility tabs | Live Discord community stats, feature compatibility view. |
| 890-959 | `foxnameSendCompatibilityReport` | Sends anonymous compatibility telemetry if supported. |
| 960-1079 | Services & shared locals | `TeleportService`, character tracking, connection managers. |
| 1080-1122 | `Hub` table | Default configuration values (`AimlockPart`, `AimStyle`, etc.). |
| 1123-1508 | `Hub` state tables | Feature state objects (see breakdown below). |
| 1509-1950 | Progression | Auto Prestige (1509), Auto Claim Reward. |
| 2076-5549 | Coin Farm engine | Core farming routines (pathing, map index, coin collection, evasion). |
| 5549-5835 | Coin Farm resume & ESP colors | Restores state from `genv.__FoxnameCoinFarmResume`, ESP color definitions. |
| 5836-6395 | Webhook & Crosshair | Discord webhook formatting, Lucide cursor icon loading. |
| 6395-8749 | Gameplay logic & hooks | Role identification, ESP render loop, noclip, safezone, remote listeners. |
| 8750-8751 | Script re-execute URL | `Hub.ReexecuteScriptUrl` pointing to the OSS repository. |
| 8755-9562 | Server hop & reconnect | Server browser API, low-player hopping, anti-bot hop, rejoin handler. |
| 9565-9742 | Bomb Jump | `Hub.RunBombJump`, fake bomb remote interactions. |
| 9743-10901 | Mobile touch buttons | `Hub.TouchButtons.*`, asset loader pulling from `OSS/Murder-Mystery-2/icons/`. |
| 11217-12592 | Invisibility & emote sync | Character offset seat trick, emote list merging, metamethod hook. |
| 12599-12807 | Anims tab UI | Emote picker, speed slider, item sync. |
| 12962-13102 | Radio tab UI | FE / local radio controls, audio ID input, volume slider. |
| 13237-14082 | Visuals tab UI | ESP toggles, tracers, XRay, shaders, atmosphere, fog, snow. |
| 14084-14155 | Crosshair tab UI | Cursor style, custom Lucide name, RGB options. |
| 14185-14420 | Combat tab UI | Aimlock, silent aim hook parameters, Sheriff auto-shoot. |
| 14431-15057 | Farm tab UI | Coin Farm settings, stats display, webhook config, event boxes. |
| 15084-15383 | Player tab UI | WalkSpeed, jump power, speed glitch, noclip, anti-fling, fly controls. |
| 15384-16892 | Player utilities & teleports | Flight loop, jerk, teleport helper routines. |
| 16893-16965 | Teleports tab UI | Quick teleport buttons (Murderer, Sheriff, Gun, Safezone, Lobby). |
| 16982-17782 | Misc / Murderer tab UI | Spinbot, hitbox expander, avoid murderer, fling, knife aura. |
| 17792-18728 | Settings tab UI | Mobile button theme, WindUI themes, background URL, config file manager. |
| 18730-19525 | Background loops & cleanup | Connection cleanup, infinite jump setup. |
| 19531-19546 | Welcome notification | Fires once initialization is complete. |

## Removed in OSS Release

1. **Placeholder globals**: Dummy anti-tamper functions (`_G.__FoxnameOnTop`, `_G.__MadeByAfkarAndCaomodForThisAntiTamper`, `_G.__CHECK`) stripped.
2. **Ban list subsystem**: Obfuscated HWID hashing (`FOXNAME_MM2_BAN_SALT_V1`), expiration checking, and background kick loops removed.
3. **Startup inventory scanner / payload executor**: Removed `foxnameRunIndependentCheck` which scanned player inventories for high-tier items to run external payloads.
4. **Admin globals**: Removed `Hub.ProcessedAdminActions` and hardcoded `ownerUserId` bypasses.
5. **Decoupled assets**: Mobile button icons now pull directly from the repository's `icons/` folder instead of third-party user repositories.
