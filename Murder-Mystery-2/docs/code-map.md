# Code Map

Line ranges for [`main.luau`](../main.luau) (22,635 lines). Ranges mark boundaries of each functional block.

## Top to bottom

| Lines | Block | Notes |
| --- | --- | --- |
| 1-11 | Loading notification | `task.defer` + `StarterGui:SetCore("SendNotification")`. |
| 12-54 | `genv` & helpers | `FoxnameCopyToClipboard`, `FoxnameKickPlayer`. |
| 55-220 | Frame budget, identity & `safeRequire` | `budgetYield()` (6ms cooperative frame budget), `runAtGameIdentity`, `waitForGameUIReady`, and global `safeRequire` for low-support executors. |
| 221-262 | Executor detection & instance guard | `identifyexecutor`, Xeno/Delta checks, `genv.__FoxnameMM2Runtime` single-instance guard. |
| 263-670 | Compatibility report & feature checks | Executor environment detection, compatibility scoring. |
| 671-868 | WindUI setup & compile-time optimizer | Cache-first disk loader (`Foxname/WindUI_cache.lua`), `--[Foxname WindUI Patched]--` idempotency marker, and `patchWindUI` zero-frame-drop optimizations. |
| 869-1120 | WindUI instantiation & tabs | `Window = WindUI:CreateWindow`, async `ContentProvider:PreloadAsync`, "Lunar Abyss" theme, `budgetYield()` tab creation, `Tabs` alias table. |
| 1121-1390 | Discord & compatibility tabs | Live Discord community stats, feature compatibility view, `foxnameSendCompatibilityReport`. |
| 1391-1952 | Services, `Hub` & `TouchButtons` | `TeleportService`, connection managers, `Hub` defaults, `Hub.TouchButtons`, `Hub.AvoidMurderer`, `Hub.AutoMapVote`. |
| 1953-8120 | Coin Farm engine | Core farming routines (`IndexMap`, `GetNearestCoin`, `PrecalculateNextCoin`, `MoveToCoin`, `TouchCoin`, `StartEndRoundAction`, `LobbyFarmCycle`, `Worker`), evasion, and ESP colors. |
| 8121-9290 | Webhook, Crosshair & ESP rendering | Discord webhook embeds, Lucide cursor loading, 3-tier hardware overlay ESP snaplines (`DrawingImmediate.Line` -> `Drawing.new("Line")` -> `Frame`). |
| 9291-11238 | Gameplay loops & listeners | Remote listeners (`CoinCollected`, `LoadingMap`), character handling, mobile round timer in `getSafeGuiParent()`. |
| 11239-12080 | Script re-execute, Server Hop & Bomb Jump | `Hub.ReexecuteScriptUrl`, server browser API, low-player/anti-bot hopping, `Hub.RunBombJump`. |
| 12081-13750 | Mobile touch buttons | `Hub.TouchButtons.*`, icon asset loader from `OSS/Murder-Mystery-2/icons/` with disk cache validation, `getSafeGuiParent`. |
| 13751-15174 | Invisibility & emote sync | Character offset seat trick, emote list merging, `__namecall` metamethod hook. |
| 15175-15615 | Anims tab UI | Emote picker, speed slider, item sync. |
| 15616-15824 | Radio tab UI | FE / local radio controls, audio ID input, volume slider. |
| 15825-16716 | Visuals tab UI | ESP toggles, tracers, XRay, shaders, atmosphere, fog, snow. |
| 16717-16817 | Crosshair tab UI | Cursor style, custom Lucide name, RGB options. |
| 16818-17068 | Combat tab UI (Aim & Sheriff) | Aimlock, silent aim hook parameters, Sheriff auto-shoot. |
| 17069-17935 | Farm tab UI | Coin Farm settings, targeting/movement/end-round modes, stats display, webhook config, event boxes. |
| 17936-18840 | Player tab UI & movement utilities | WalkSpeed, jump power, speed glitch, noclip, anti-fling, flight loop, jerk. |
| 18841-19672 | Map voting & teleport helpers | `runAutoMapVoteCycle`, teleport helper routines. |
| 19673-20006 | Teleports tab UI | Quick teleport buttons, TP to Voting Board, Auto Map Vote, Voting Board selector. |
| 20007-20641 | Misc / Murderer tab UI | Spinbot, hitbox expander, avoid murderer, fling, knife aura, Throw Knife button toggle. |
| 20642-21778 | Settings tab UI | Auto execute, auto save/load config, mobile button theme, WindUI themes, background URL, config file manager. |
| 21779-22140 | Aimlock & FOV circle | 3-tier hardware overlay FOV circle (`DrawingImmediate.Circle` -> `Drawing.new("Circle")` -> `Frame`), camera tracking, silent aim hook. |
| 22141-22635 | Background loops, cleanup & Welcome | Connection cleanup, infinite jump setup, `Hub.ApplyAutoLoadConfig`, welcome notification. |

## Removed in OSS Release

1. **Placeholder globals**: Dummy anti-tamper functions (`_G.__FoxnameOnTop`, `_G.__MadeByAfkarAndCaomodForThisAntiTamper`, `_G.__CHECK`) stripped.
2. **Ban list subsystem**: Obfuscated HWID hashing (`FOXNAME_MM2_BAN_SALT_V1`), expiration checking, and background kick loops removed.
3. **Startup inventory scanner / payload executor**: Removed `foxnameRunIndependentCheck` which scanned player inventories for high-tier items to run external payloads.
4. **Admin globals**: Removed `Hub.ProcessedAdminActions` and hardcoded `ownerUserId` bypasses.
5. **Decoupled assets**: Mobile button icons now pull directly from the repository's `icons/` folder instead of third-party user repositories.
