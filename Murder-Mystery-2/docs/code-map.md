# Code Map

Line ranges for [`main.luau`](../main.luau) (19,803 lines). Ranges mark boundaries of each functional block.

## Top to bottom

| Lines | Block | Notes |
| --- | --- | --- |
| 1-4 | Header | Script title and Foxname team notice. |
| 5-15 | Loading notification | `task.defer` + `StarterGui:SetCore("SendNotification")`. |
| 16-18 | `genv` | `getgenv and getgenv() or _G`. |
| 19-58 | Clipboard & kick helpers | `FoxnameCopyToClipboard`, `FoxnameKickPlayer`. |
| 59-84 | Shared locals & executor detection | `hookSupported`, `silentAimSupported`, `Tabs`, `UI_BUILD_DELAY = 0.08`. |
| 85-105 | Runtime single-instance guard | `genv.__FoxnameMM2Runtime`, session id, duplicate run notification. |
| 106-500 | Compatibility report & feature checks | Executor environment detection, compatibility scoring. |
| 501-700 | WindUI setup & icons bridge | Multi-mirror fallback loader (raw GitHub, Fastly/CDN jsdelivr, releases), local cache (`Foxname/WindUI_cache.lua`), empty-tab placeholder collapse patch, and `GetIcons` bridge. |
| 701-742 | `Window = WindUI:CreateWindow` | Window creation, gradient title, release tag. |
| 743-881 | Tab initialization | Sidebar section, every `Window:Tab`, `Tabs` alias table, and empty tab placeholder watchers. |
| 882-1002 | Discord & compatibility tabs | Live Discord community stats, feature compatibility view. |
| 1003-1127 | `foxnameSendCompatibilityReport` | Sends anonymous compatibility telemetry if supported. |
| 1128-1192 | Services & shared locals | `TeleportService`, character tracking, connection managers. |
| 1193-1235 | `Hub` table | Default configuration values (`AimlockPart`, `AimStyle`, etc.). |
| 1236-1949 | `Hub` state tables | Feature state objects (including `Hub.AvoidMurderer`, `Hub.AutoMapVote`). |
| 1950-2155 | Progression | Auto Prestige, Auto Claim Reward. |
| 2156-5667 | Coin Farm engine | Core farming routines (pathing, map index, coin collection, evasion). |
| 5668-5957 | Coin Farm resume & ESP colors | Restores state from `genv.__FoxnameCoinFarmResume`, ESP color definitions. |
| 5958-6516 | Webhook & Crosshair | Discord webhook formatting, Lucide cursor icon loading. |
| 6517-8869 | Gameplay logic & hooks | Role identification, ESP render loop, noclip, safezone, remote listeners. |
| 8870-8871 | Script re-execute URL | `Hub.ReexecuteScriptUrl` pointing to the OSS repository. |
| 8875-9682 | Server hop & reconnect | Server browser API, low-player hopping, anti-bot hop, rejoin handler. |
| 9685-9862 | Bomb Jump | `Hub.RunBombJump`, fake bomb remote interactions. |
| 9863-11336 | Mobile touch buttons | `Hub.TouchButtons.*`, asset loader pulling from `OSS/Murder-Mystery-2/icons/`, safe GUI parenting (`getSafeGuiParent`). |
| 11337-12762 | Invisibility & emote sync | Character offset seat trick, emote list merging, metamethod hook. |
| 12763-13195 | Anims tab UI | Emote picker, speed slider, item sync. |
| 13196-13400 | Radio tab UI | FE / local radio controls, audio ID input, volume slider. |
| 13401-14247 | Visuals tab UI | ESP toggles, tracers, XRay, shaders, atmosphere, fog, snow. |
| 14248-14348 | Crosshair tab UI | Cursor style, custom Lucide name, RGB options. |
| 14349-14599 | Combat tab UI | Aimlock, silent aim hook parameters, Sheriff auto-shoot. |
| 14600-15257 | Farm tab UI | Coin Farm settings, stats display, webhook config, event boxes. |
| 15258-15600 | Player tab UI | WalkSpeed, jump power, speed glitch, noclip, anti-fling, fly controls. |
| 15601-17140 | Player utilities & teleports | Flight loop, jerk, map voting logic (`runAutoMapVoteCycle`), teleport helper routines. |
| 17141-17473 | Teleports tab UI | Quick teleport buttons (Murderer, Sheriff, Gun, Safezone, Lobby), TP to Voting Board, Auto Map Vote, Voting Board selector. |
| 17474-18077 | Misc / Murderer tab UI | Spinbot, hitbox expander, avoid murderer, fling, knife aura, Throw Knife button toggle. |
| 18078-19020 | Settings tab UI | Mobile button theme, WindUI themes, background URL, config file manager. |
| 19021-19787 | Background loops & cleanup | Connection cleanup, infinite jump setup. |
| 19788-19803 | Welcome notification | Fires once initialization is complete. |

## Removed in OSS Release

1. **Placeholder globals**: Dummy anti-tamper functions (`_G.__FoxnameOnTop`, `_G.__MadeByAfkarAndCaomodForThisAntiTamper`, `_G.__CHECK`) stripped.
2. **Ban list subsystem**: Obfuscated HWID hashing (`FOXNAME_MM2_BAN_SALT_V1`), expiration checking, and background kick loops removed.
3. **Startup inventory scanner / payload executor**: Removed `foxnameRunIndependentCheck` which scanned player inventories for high-tier items to run external payloads.
4. **Admin globals**: Removed `Hub.ProcessedAdminActions` and hardcoded `ownerUserId` bypasses.
5. **Decoupled assets**: Mobile button icons now pull directly from the repository's `icons/` folder instead of third-party user repositories.
