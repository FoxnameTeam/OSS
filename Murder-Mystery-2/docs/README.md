# Murder Mystery 2 – Script Docs

Documentation for [`main.luau`](../main.luau), a single-file Roblox executor script (about 20k lines) built on [WindUI](https://github.com/Footagesus/WindUI).

| Doc | What it covers |
| --- | --- |
| [code-map.md](code-map.md) | Where everything sits in `main.luau`, by line range |
| [features.md](features.md) | Every UI option, per tab, with the line where it is built |
| [configuration.md](configuration.md) | Flags, configs, touch buttons, themes |
| [external-services.md](external-services.md) | Network calls, game remotes, metamethod hooks, startup checks |

## Requirements

An executor that provides:

| Needed for | Globals |
| --- | --- |
| Loading UI and assets | `loadstring`, `game:HttpGet` |
| Webhook, compatibility report | `request` / `http_request` / `syn.request` |
| Configs | `readfile`, `writefile`, `isfile`, `makefolder` |
| Clipboard | `setclipboard` (or `setrbxclipboard`) |
| Silent aim, emote sync | `hookmetamethod`, `getnamecallmethod`, `checkcaller`, `newcclosure` |
| Server hop persistence | `queue_on_teleport` |

Missing hook functions disable only the features that need them. The **UNC / sUNC** tab shows what your executor supports. Xeno is detected by name and is treated as hook-unsupported.

## How the script runs

1. Shows a "Script is loading" notification.
2. Prevents double execution through `genv.__FoxnameMM2Runtime`. A second run shows "Script already running!".
3. Loads WindUI, builds the window and all tabs (with short `task.wait` pauses so executors don't time out).
4. Builds the `Hub` state table, then every feature module.
5. Registers each UI element, then restores config values.
6. Starts background loops, then shows "Welcome user!" once startup data is ready.

## Editing tips

- The file is large. Search by the UI `Title = "..."` or `Flag = "..."` string instead of scrolling.
- Line numbers in these docs match the current file and drift after edits. To find a section again:
  ```powershell
  Select-String -Path main.luau -Pattern 'Window:Tab\(|^Tabs\.\w+:Section|Hub\.CoinFarm = '
  ```
- Keep the license header at the top. Adding lines shifts every number below.

## License

GPLv3. See [LICENSE](../LICENSE) and [CONTRIBUTING.md](../CONTRIBUTING.md).
