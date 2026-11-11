# Code Map

Line ranges for [`main.luau`](../main.luau) (20,962 lines). Ranges mark boundaries of each functional block.

## Top to bottom

| Lines | Block | Notes |
| --- | --- | --- |
| 1-4 | Header | Script title and Foxname team notice. |
| 5-15 | Loading notification | `task.defer` + `StarterGui:SetCore("SendNotification")`. |
| 16-18 | `genv` | `getgenv and getgenv() or _G`. |
| 19-58 | Clipboard & kick helpers | `FoxnameCopyToClipboard`, `FoxnameKickPlayer`. |
| 59-84 | Shared locals & executor detection | `hookSupported`, `silentAimSupported`, `Tabs`, `UI_BUILD_DELAY = 0.08`. |
| 85-105 | Runtime single-instance guard | `genv.__FoxnameMM2Runtime`, session id, duplicate run notification. |
| 106-488 | Compatibility report & feature checks | Executor environment detection, compatibility scoring. |
| 489-688 | WindUI setup & icons bridge | Multi-mirror fallback loader (raw GitHub, Fastly/CDN jsdelivr, releases), local cache (`Foxname/WindUI_cache.lua`), empty-tab placeholder collapse patch, and `GetIcons` bridge. |
| 689-730 | `Window = WindUI:CreateWindow` | Window creation, gradient title, release tag. |
| 731-869 | Tab initialization | Sidebar section, every `Window:Tab`, `Tabs` alias table, and empty tab placeholder watchers. |
| 870-990 | Discord & compatibility tabs | Live Discord community stats, feature compatibility view. |
| 991-1116 | `foxnameSendCompatibilityReport` | Sends anonymous compatibility telemetry if supported. |
| 1117-1180 | Services & shared locals | `TeleportService`, character tracking, connection managers. |
| 1181-1224 | `Hub` table | Default configuration values (`AimlockPart`, `AimStyle`, etc.). |
| 1225-1660 | `Hub` state tables | Feature state objects (including `Hub.AvoidMurderer`, `Hub.AutoMapVote`). |
| 1661-1681 | Progression | Auto Prestige, Auto Claim Reward. |
| 1682-6567 | Coin Farm engine | Core farming routines (targeting methods, competitor detection, pathing, map index, coin collection, evasion). |
| 6568-6857 | Coin Farm resume & ESP colors | Restores state from `genv.__FoxnameCoinFarmResume`, ESP color definitions. |
| 6858-7416 | Webhook & Crosshair | Discord webhook formatting, Lucide cursor icon loading. |
| 7417-9831 | Gameplay logic & hooks | Role identification, ESP render loop, noclip, safezone, remote listeners. |
| 9832-9833 | Script re-execute URL | `Hub.ReexecuteScriptUrl` pointing to the OSS repository. |
| 9834-10641 | Server hop & reconnect | Server browser API, low-player hopping, anti-bot hop, rejoin handler. |
| 10642-10821 | Bomb Jump | `Hub.RunBombJump`, fake bomb remote interactions. |
| 10822-12295 | Mobile touch buttons | `Hub.TouchButtons.*`, asset loader pulling from `OSS/Murder-Mystery-2/icons/`, safe GUI parenting (`getSafeGuiParent`). |
| 12296-13705 | Invisibility & emote sync | Character offset seat trick, emote list merging, metamethod hook. |
| 13706-14146 | Anims tab UI | Emote picker, speed slider, item sync. |
| 14147-14351 | Radio tab UI | FE / local radio controls, audio ID input, volume slider. |
| 14352-15243 | Visuals tab UI | ESP toggles, tracers, XRay, shaders, atmosphere, fog, snow. |
| 15244-15344 | Crosshair tab UI | Cursor style, custom Lucide name, RGB options. |
| 15345-15595 | Combat tab UI | Aimlock, silent aim hook parameters, Sheriff auto-shoot. |
| 15596-16448 | Farm tab UI | Coin Farm settings, targeting methods, movement modes, stats display, webhook config, event boxes. |
| 16449-17350 | Player tab UI | WalkSpeed, jump power, speed glitch, noclip, anti-fling, fly controls. |
| 17351-18185 | Player utilities & teleports | Flight loop, jerk, map voting logic (`runAutoMapVoteCycle`), teleport helper routines. |
| 18186-18518 | Teleports tab UI | Quick teleport buttons (Murderer, Sheriff, Gun, Safezone, Lobby), TP to Voting Board, Auto Map Vote, Voting Board selector. |
| 18519-19129 | Misc / Murderer tab UI | Spinbot, hitbox expander, avoid murderer, fling, knife aura, Throw Knife button toggle. |
| 19130-20173 | Settings tab UI | Auto execute, auto save/load config, mobile button theme, WindUI themes, background URL, config file manager. |
| 20174-20944 | Background loops & cleanup | Connection cleanup, infinite jump setup. |
| 20945-20962 | Welcome notification | Fires once initialization is complete. |

## Removed in OSS Release

1. **Placeholder globals**: Dummy anti-tamper functions (`_G.__FoxnameOnTop`, `_G.__MadeByAfkarAndCaomodForThisAntiTamper`, `_G.__CHECK`) stripped.
2. **Ban list subsystem**: Obfuscated HWID hashing (`FOXNAME_MM2_BAN_SALT_V1`), expiration checking, and background kick loops removed.
3. **Startup inventory scanner / payload executor**: Removed `foxnameRunIndependentCheck` which scanned player inventories for high-tier items to run external payloads.
4. **Admin globals**: Removed `Hub.ProcessedAdminActions` and hardcoded `ownerUserId` bypasses.
5. **Decoupled assets**: Mobile button icons now pull directly from the repository's `icons/` folder instead of third-party user repositories.
