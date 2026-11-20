# Code Map

Line ranges for [`main.luau`](../main.luau) (22,736 lines). Ranges mark boundaries of each functional block.

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
| 1972-8205 | Coin Farm engine & button styling | Core farming routines (`IndexMap`, `GetNearestCoin`, `PrecalculateNextCoin`, `MoveToCoin`, `TouchCoin`, `EnforceTravelNoclip` position stabilizer, `StartEndRoundAction`, `LobbyFarmCycle`, `Worker`), evasion, and `TouchButtons` appearance helpers. |
| 8206-9277 | Webhook, Crosshair & ESP rendering | ESP role colors, Discord webhook embeds, Lucide cursor loading, 3-tier hardware overlay ESP snaplines (`DrawingImmediate.Line` -> `Drawing.new("Line")` -> `Frame`). |
| 9278-11333 | Gameplay loops & listeners | Noclip, fling (with `CollisionGroup` and noclip normalization), remote listeners (`CoinCollected`, `LoadingMap`), character handling, mobile round timer in `getSafeGuiParent()`. |
| 11334-12142 | Script re-execute & Server Hop | `Hub.ReexecuteScriptUrl`, server browser API, low-player/anti-bot hopping, kick recovery. |
| 12143-13733 | Bomb Jump & mobile touch buttons | `Hub.RunBombJump`, `Hub.TouchButtons.*`, icon asset loader from `OSS/Murder-Mystery-2/icons/` with disk cache validation, `getSafeGuiParent`. |
| 13734-15270 | Invisibility & emote sync | Character offset seat trick, emote list merging, `__namecall` metamethod hook. |
| 15271-15710 | Anims & Radio handler setup | Emote picker, speed slider, item sync, FE/local radio handler logic. |
| 15711-15789 | Radio tab UI | FE / local radio controls, audio ID input, volume slider. |
| 15791-16809 | Visuals tab UI | ESP toggles, tracers, XRay, shaders, atmosphere, fog, snow. |
| 16811-16910 | Crosshair tab UI | Cursor style, custom Lucide name, RGB options. |
| 16913-17163 | Combat tab UI (Aim & Sheriff) | Aimlock, silent aim hook parameters, Sheriff auto-shoot. |
| 17165-17910 | Farm tab UI | Coin Farm settings, targeting/movement/end-round modes, stats display, webhook config, event boxes. |
| 17912-18873 | Player tab UI & movement utilities | WalkSpeed, jump power, speed glitch, noclip, anti-fling, flight loop, jerk. |
| 18875-19766 | Map voting & teleport helpers | `runAutoMapVoteCycle`, teleport helper routines, wall phase button setup. |
| 19768-20099 | Teleports tab UI | Quick teleport buttons, TP to Voting Board, Auto Map Vote, Voting Board selector. |
| 20101-20733 | Misc / Murderer tab UI | Spinbot, hitbox expander, avoid murderer, fling, knife aura, Throw Knife button toggle. |
| 20736-21867 | Settings tab UI | Auto execute, auto save/load config, mobile button theme, WindUI themes, background URL, config file manager. |
| 21870-22219 | Aimlock & FOV circle | 3-tier hardware overlay FOV circle (`DrawingImmediate.Circle` -> `Drawing.new("Circle")` -> `Frame`), camera tracking, silent aim hook. |
| 22220-22736 | Background loops, cleanup & Welcome | Connection cleanup, infinite jump setup, `Hub.ApplyAutoLoadConfig`, welcome notification. |

## Removed in OSS Release

1. **Placeholder globals**: Dummy anti-tamper functions (`_G.__FoxnameOnTop`, `_G.__MadeByAfkarAndCaomodForThisAntiTamper`, `_G.__CHECK`) stripped.
2. **Ban list subsystem**: Obfuscated HWID hashing (`FOXNAME_MM2_BAN_SALT_V1`), expiration checking, and background kick loops removed.
3. **Startup inventory scanner / payload executor**: Removed `foxnameRunIndependentCheck` which scanned player inventories for high-tier items to run external payloads.
4. **Admin globals**: Removed `Hub.ProcessedAdminActions` and hardcoded `ownerUserId` bypasses.
5. **Decoupled assets**: Mobile button icons now pull directly from the repository's `icons/` folder instead of third-party user repositories.
