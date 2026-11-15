# Code Map

Line ranges for [`main.luau`](../main.luau) (22,758 lines). Ranges mark boundaries of each functional block.

## Top to bottom

| Lines | Block | Notes |
| --- | --- | --- |
| 1-11 | Loading notification | `task.defer` + `StarterGui:SetCore("SendNotification")`. |
| 12-54 | `genv` & helpers | `FoxnameCopyToClipboard`, `FoxnameKickPlayer`. |
| 55-217 | Frame budget, identity & `safeRequire` | `budgetYield()` (6ms cooperative frame budget), `runAtGameIdentity`, `waitForGameUIReady`, and global `safeRequire` for low-support executors. |
| 218-262 | Executor detection & instance guard | `identifyexecutor`, Xeno/Delta checks, `genv.__FoxnameMM2Runtime` single-instance guard. |
| 263-611 | Compatibility report & feature checks | Executor environment detection, compatibility scoring. |
| 612-949 | WindUI setup & runtime patcher | `ReplicatedStorage.GetIcons` bridge, raw-source disk cache (`Foxname/WindUI_cache.lua`, `isRawWindUI`), and `patchWindUI` in-memory optimizations and dropdown positioning fixes. |
| 950-1174 | WindUI instantiation & tabs | `Window = WindUI:CreateWindow`, async `ContentProvider:PreloadAsync`, "Lunar Abyss" theme, `budgetYield()` tab creation, `Tabs` alias table. |
| 1175-1394 | Discord & compatibility tabs | Live Discord community stats and guild icon fetch (`v11:SetImage`), feature compatibility view, `foxnameSendCompatibilityReport`. |
| 1396-1971 | Services, `Hub` & `TouchButtons` | `TeleportService`, connection managers, `Hub` defaults, `Hub.TouchButtons`, `Hub.AvoidMurderer`, `Hub.AutoMapVote`. |
| 1972-8235 | Coin Farm engine & button styling | Core farming routines (`IndexMap`, `GetNearestCoin`, `PrecalculateNextCoin`, `MoveToCoin`, `TouchCoin`, `EnforceTravelNoclip` position stabilizer, `StartEndRoundAction`, `LobbyFarmCycle`, `Worker`), evasion, and `TouchButtons` appearance helpers. |
| 8236-9306 | Webhook, Crosshair & ESP rendering | ESP role colors, Discord webhook embeds, Lucide cursor loading, 3-tier hardware overlay ESP snaplines (`DrawingImmediate.Line` -> `Drawing.new("Line")` -> `Frame`). |
| 9307-11361 | Gameplay loops & listeners | Noclip, fling (with `CollisionGroup` and noclip normalization), remote listeners (`CoinCollected`, `LoadingMap`), character handling, mobile round timer in `getSafeGuiParent()`. |
| 11362-12169 | Script re-execute & Server Hop | `Hub.ReexecuteScriptUrl`, server browser API, low-player/anti-bot hopping, kick recovery. |
| 12170-13760 | Bomb Jump & mobile touch buttons | `Hub.RunBombJump`, `Hub.TouchButtons.*`, icon asset loader from `OSS/Murder-Mystery-2/icons/` with disk cache validation, `getSafeGuiParent`. |
| 13761-15297 | Invisibility & emote sync | Character offset seat trick, emote list merging, `__namecall` metamethod hook. |
| 15298-15738 | Anims & Radio handler setup | Emote picker, speed slider, item sync, FE/local radio handler logic. |
| 15739-15816 | Radio tab UI | FE / local radio controls, audio ID input, volume slider. |
| 15818-16838 | Visuals tab UI | ESP toggles, tracers, XRay, shaders, atmosphere, fog, snow. |
| 16840-16937 | Crosshair tab UI | Cursor style, custom Lucide name, RGB options. |
| 16941-17190 | Combat tab UI (Aim & Sheriff) | Aimlock, silent aim hook parameters, Sheriff auto-shoot. |
| 17192-17940 | Farm tab UI | Coin Farm settings, targeting/movement/end-round modes, stats display, webhook config, event boxes. |
| 17944-18901 | Player tab UI & movement utilities | WalkSpeed, jump power, speed glitch, noclip, anti-fling, flight loop, jerk. |
| 18903-19793 | Map voting & teleport helpers | `runAutoMapVoteCycle`, teleport helper routines, wall phase button setup. |
| 19796-20127 | Teleports tab UI | Quick teleport buttons, TP to Voting Board, Auto Map Vote, Voting Board selector. |
| 20130-20761 | Misc / Murderer tab UI | Spinbot, hitbox expander, avoid murderer, fling, knife aura, Throw Knife button toggle. |
| 20764-21895 | Settings tab UI | Auto execute, auto save/load config, mobile button theme, WindUI themes, background URL, config file manager. |
| 21901-22246 | Aimlock & FOV circle | 3-tier hardware overlay FOV circle (`DrawingImmediate.Circle` -> `Drawing.new("Circle")` -> `Frame`), camera tracking, silent aim hook. |
| 22248-22758 | Background loops, cleanup & Welcome | Connection cleanup, infinite jump setup, `Hub.ApplyAutoLoadConfig`, welcome notification. |

## Removed in OSS Release

1. **Placeholder globals**: Dummy anti-tamper functions (`_G.__FoxnameOnTop`, `_G.__MadeByAfkarAndCaomodForThisAntiTamper`, `_G.__CHECK`) stripped.
2. **Ban list subsystem**: Obfuscated HWID hashing (`FOXNAME_MM2_BAN_SALT_V1`), expiration checking, and background kick loops removed.
3. **Startup inventory scanner / payload executor**: Removed `foxnameRunIndependentCheck` which scanned player inventories for high-tier items to run external payloads.
4. **Admin globals**: Removed `Hub.ProcessedAdminActions` and hardcoded `ownerUserId` bypasses.
5. **Decoupled assets**: Mobile button icons now pull directly from the repository's `icons/` folder instead of third-party user repositories.
