# Configuration

## Flags

Every saved option has a unique `Flag` string (for example `ESP_Coin`, `Settings_MobileButtonAccent`, `Visuals_Fog`). Search `Flag = "` in `main.luau` to inspect existing keys. Any newly added options must define a distinct `Flag` to persist properly.

## Configs (Settings tab, lines 17792-18728)

| Action | Notes |
| --- | --- |
| Config Name / Selected Config | Input field and selector dropdown for named configuration profiles. |
| Auto Load Config | Toggles automatic configuration restoration on startup. |
| Save Config | Writes state to executor storage via `writefile`. |
| Load Selected Config | Restores options from file via `readfile`. |
| Delete Selected Config | Deletes profile file from disk. |
| Refresh Config List | Rescans the configuration folder. |

- Profile files are managed via WindUI's `Window.ConfigManager`. The root folder path is `WindUI/Foxname_MM2/config/`.
- Color updates are synchronized into live memory using `Hub.SyncConfigColorValues`.

## Mobile Touch Buttons

`Hub.TouchButtons` manages on-screen floating action buttons for mobile devices and touchscreen environments (Aimlock, XRay, Fly, Noclip, Wall Glitch, Get Gun, Bomb Jump, Throw Knife).

Each button includes:
- Toggle activation
- Size (Small, Medium, Large)
- Shape styling
- Icon color tinting
- Drag repositioning toggle
- Optional physical keybind

Button asset files are stored locally in the repository under [icons/](../icons) and fetched over raw GitHub content:
`https://raw.githubusercontent.com/FoxnameTeam/OSS/main/Murder-Mystery-2/icons/<name>.png`

Cached assets are stored on the executor client at `FoxnameMM2/icons_v1/<name>.png` using `getcustomasset` / `getsynasset`.

## Server Hop State Transfer

When hopping servers, current farm session statistics and active flags are serialized to JSON in `Foxname_MM2/coin_farm_resume.json` and saved in `genv.__FoxnameCoinFarmResume`. `queue_on_teleport` re-launches the script from `Hub.ReexecuteScriptUrl` once the new server finishes loading.
