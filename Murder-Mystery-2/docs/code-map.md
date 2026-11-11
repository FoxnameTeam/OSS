# Code Map

Line ranges for [`main.luau`](../main.luau) (21,150 lines). Ranges mark boundaries of each functional block.

## Top to bottom

| Lines | Block | Notes |
| --- | --- | --- |
| 1-4 | Header | Script title and Foxname team notice. |
| 5-15 | Loading notification | `task.defer` + `StarterGui:SetCore("SendNotification")`. |
| 16-18 | `genv` | `getgenv and getgenv() or _G`. |
| 19-58 | Clipboard & kick helpers | `FoxnameCopyToClipboard`, `FoxnameKickPlayer`. |
| 59-70 | Shared locals & frame-budget helper | `hookSupported`, `silentAimSupported`, `Tabs`, `budgetYield()` (6ms cooperative frame budget). |
| 71-96 | Executor detection | `identifyexecutor`, Xeno/Delta checks, hook capability verification. |
| 97-117 | Runtime single-instance guard | `genv.__FoxnameMM2Runtime`, session id, duplicate run notification. |
| 118-500 | Compatibility report & feature checks | Executor environment detection, compatibility scoring. |
| 501-645 | WindUI setup & compile-time optimizer | Cache-first disk loader (`Foxname/WindUI_cache.lua`), `--[Foxname WindUI Patched]--` idempotency marker, and `patchWindUI` compile-time zero-frame-drop optimizations (window open layout solver isolation, hover shine listener cleanup, targeted tab tweens, hardware 2D matrix translation for tab slide, duplicate toggle tween removal, dropdown item selection tween storm reduction, closed dropdown position bypass, slider click & drag direct size updates, empty-tab placeholder collapse patch, and `GetIcons` bridge). |
| 646-674 | WindUI instantiation & async asset preload | Instantiates WindUI and launches async `ContentProvider:PreloadAsync` for core fonts, glass spritesheets, squircles, and window backgrounds. |
| 675-766 | Theme definition | "Lunar Abyss" palette, gradients, and dialog styles. |
| 767-808 | `Window = WindUI:CreateWindow` | Window creation, gradient title, release tag. |
| 809-868 | Tab initialization | Sidebar section, every `Window:Tab` separated by `budgetYield()`, `Tabs` alias table (redundant empty-tab watchers purged). |
| 869-998 | Discord & compatibility tabs | Live Discord community stats, feature compatibility view. |
| 999-1124 | `foxnameSendCompatibilityReport` | Sends anonymous compatibility telemetry if supported. |
| 1125-1188 | Services & shared locals | `TeleportService`, character tracking, connection managers. |
| 1189-1232 | `Hub` table | Default configuration values (`AimlockPart`, `AimStyle`, etc.). |
| 1233-1668 | `Hub` state tables | Feature state objects (including `Hub.AvoidMurderer`, `Hub.AutoMapVote`). |
| 1669-1689 | Progression | Auto Prestige, Auto Claim Reward. |
| 1690-6635 | Coin Farm engine | Core farming routines (targeting methods, competitor detection, pathing, map index, coin collection, evasion). |
| 6636-6925 | Coin Farm resume & ESP colors | Restores state from `genv.__FoxnameCoinFarmResume`, ESP color definitions. |
| 6926-7484 | Webhook & Crosshair | Discord webhook formatting, Lucide cursor icon loading. |
| 7485-8025 | Gameplay logic & hooks | Role identification, 3-tier hardware overlay ESP snaplines (`DrawingImmediate.Line` -> `Drawing.new("Line")` -> `Frame`), noclip, safezone. |
| 8026-9969 | Gameplay loops & listeners | Remote listeners, character handling, mobile round timer in `getSafeGuiParent()` with cleanup. |
| 9970-9971 | Script re-execute URL | `Hub.ReexecuteScriptUrl` pointing to the OSS repository. |
| 9972-10781 | Server hop & reconnect | Server browser API, low-player hopping, anti-bot hop, rejoin handler. |
| 10782-10961 | Bomb Jump | `Hub.RunBombJump`, fake bomb remote interactions. |
| 10962-12435 | Mobile touch buttons | `Hub.TouchButtons.*`, asset loader pulling from `OSS/Murder-Mystery-2/icons/` with disk check guard `if not ok then` to eliminate redundant HTTP requests, safe GUI parenting (`getSafeGuiParent`). |
| 12436-13845 | Invisibility & emote sync | Character offset seat trick, emote list merging, metamethod hook. |
| 13846-14286 | Anims tab UI | Emote picker, speed slider, item sync. |
| 14287-14491 | Radio tab UI | FE / local radio controls, audio ID input, volume slider. |
| 14492-15383 | Visuals tab UI | ESP toggles, tracers, XRay, shaders, atmosphere, fog, snow. |
| 15384-15484 | Crosshair tab UI | Cursor style, custom Lucide name, RGB options. |
| 15485-15735 | Combat tab UI | Aimlock, silent aim hook parameters, Sheriff auto-shoot. |
| 15736-16588 | Farm tab UI | Coin Farm settings, targeting methods, movement modes, stats display, webhook config, event boxes. |
| 16589-17489 | Player tab UI | WalkSpeed, jump power, speed glitch, noclip, anti-fling, fly controls. |
| 17490-18325 | Player utilities & teleports | Flight loop, jerk, map voting logic (`runAutoMapVoteCycle`), teleport helper routines. |
| 18326-18658 | Teleports tab UI | Quick teleport buttons (Murderer, Sheriff, Gun, Safezone, Lobby), TP to Voting Board, Auto Map Vote, Voting Board selector. |
| 18659-19269 | Misc / Murderer tab UI | Spinbot, hitbox expander, avoid murderer, fling, knife aura, Throw Knife button toggle. |
| 19270-20359 | Settings tab UI | Auto execute, auto save/load config, mobile button theme, WindUI themes, background URL, config file manager. |
| 20360-20660 | Aimlock & FOV circle | 3-tier hardware overlay FOV circle (`DrawingImmediate.Circle` -> `Drawing.new("Circle")` -> `Frame`), camera tracking, silent aim hook. |
| 20661-21143 | Background loops & cleanup | Connection cleanup, infinite jump setup, `Hub.ApplyAutoLoadConfig`. |
| 21144-21150 | Welcome notification | Fires once initialization is complete. |

## Removed in OSS Release

1. **Placeholder globals**: Dummy anti-tamper functions (`_G.__FoxnameOnTop`, `_G.__MadeByAfkarAndCaomodForThisAntiTamper`, `_G.__CHECK`) stripped.
2. **Ban list subsystem**: Obfuscated HWID hashing (`FOXNAME_MM2_BAN_SALT_V1`), expiration checking, and background kick loops removed.
3. **Startup inventory scanner / payload executor**: Removed `foxnameRunIndependentCheck` which scanned player inventories for high-tier items to run external payloads.
4. **Admin globals**: Removed `Hub.ProcessedAdminActions` and hardcoded `ownerUserId` bypasses.
5. **Decoupled assets**: Mobile button icons now pull directly from the repository's `icons/` folder instead of third-party user repositories.
