# Configuration

## Flags

Every saved option has a unique `Flag` string (for example `ESP_Coin`, `Farm_TargetingMethod`, `Settings_AutoExecute`). Search `Flag = "` in `main.luau` to inspect existing keys. Any newly added options must define a distinct `Flag` to persist properly.

### Common Flags Reference

| Flag | Category | Purpose |
| --- | --- | --- |
| `ESP_Coin` | Visuals | Highlights spawned coins. |
| `Farm_MovementMode` | Farm | Movement execution style (`Stop and Go` or `Continuous`). |
| `Farm_TargetingMethod` | Farm | Coin selection mode (`Advanced method` or `Simple method`). |
| `Farm_EndRoundMode` | Farm | End round routine (`Normal (shooting)`, `Shoot only if Gun Dropped`, `Fling Murderer`, `Fling All`). |
| `Farm_LobbyFarm` | Farm | Toggles lobby-to-coin collection loop. |
| `Farm_ServerHopTimerEnabled` | Farm | Enables interval-based server hopping. |
| `Teleports_AutoMapVote` | Teleports | Enables automatic map voting cycle in lobby. |
| `Teleports_VotingBoard` | Teleports | Selected voting board target (`Board 1`, `Board 2`, `Board 3`). |
| `Murderer_ThrowKnifeButton` | Combat / Murderer | Displays floating Throw Knife touch action button. |
| `Settings_AutoExecute` | Settings | Enables script re-execution via `queue_on_teleport`. |
| `Settings_AutoLoadConfig` | Settings | Toggles automatic configuration restoration on startup. |
| `Settings_AutoSaveConfig` | Settings | Enables periodic auto-save of active configuration. |
| `Settings_MobileButtonAccent` | Settings | Custom accent color for on-screen action buttons. |
| `Visuals_Fog` | Visuals | Toggles custom environmental fog density and color. |

## Configs (Settings tab, lines 19270-20359)

| Action | Notes |
| --- | --- |
| Config Name / Selected Config | Input field and selector dropdown for named configuration profiles. |
| Auto Load Config | Toggles automatic configuration restoration on startup. |
| Auto Save Config | Periodically writes active settings to file every 60 seconds. |
| Save Config | Writes state to executor storage via `writefile`. |
| Load Selected Config | Restores options from file via `readfile`. |
| Delete Selected Config | Deletes profile file from disk. |
| Refresh Config List | Rescans the configuration folder. |

- Profile files are managed via WindUI's `Window.ConfigManager`. The root folder path is `WindUI/Foxname_MM2/config/`.
- Color updates are synchronized into live memory using `Hub.SyncConfigColorValues`.

## WindUI & Asset Caching

- **WindUI Library Cache**: Pre-patched WindUI source is cached on the executor client at `Foxname/WindUI_cache.lua` with a `--[Foxname WindUI Patched]--` header. The loader checks local cache *first*, bypassing network requests and 260KB of regex pattern evaluations on subsequent executions (<10ms load time).
- **Button Assets**: Mobile button PNG icons are checked on disk (`FoxnameMM2/icons_v1/<name>.png`) before network fetching. If valid PNG data exists on disk, zero HTTP requests are issued.
- **Core Asset Preloading**: WindUI custom fonts, squircle textures, and MM2 backgrounds are preloaded asynchronously into VRAM on startup via `ContentProvider:PreloadAsync` to eliminate first-interaction freezes.
- **Hardware Overlay Rendering**: ESP snaplines and Aimlock FOV circle utilize Potassium's native `DrawingImmediate` hardware pipeline when available (with fallbacks to `Drawing` and Roblox `GuiObject`s), completely avoiding ScreenGui canvas dirtying.
- **Mobile Round Timer**: Parented safely to `getSafeGuiParent()` (`gethui()`) with cleanup across both `getSafeGuiParent()` and `PlayerGui`.

## Mobile Touch Buttons

`Hub.TouchButtons` manages on-screen floating action buttons for mobile devices and touchscreen environments (Aimlock, XRay, Fly, Noclip, Wall Glitch, Get Gun, Bomb Jump, Throw Knife, Auto Shoot).

Each button includes:
- Toggle activation
- Size (Small, Medium, Large)
- Shape styling
- Icon color tinting
- Drag repositioning toggle
- Safe GUI parenting via `getSafeGuiParent()`
- Optional physical keybind

Button asset files are stored locally in the repository under [icons/](../icons) and fetched over raw GitHub content:
`https://raw.githubusercontent.com/FoxnameTeam/OSS/main/Murder-Mystery-2/icons/<name>.png`
