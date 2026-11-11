# Murder Mystery 2 – Script Docs

Documentation for [`main.luau`](../main.luau), a single-file Roblox executor script (21,150 lines) built on [WindUI](https://github.com/Footagesus/WindUI).

| Doc | What it covers |
| --- | --- |
| [code-map.md](code-map.md) | Where everything sits in `main.luau`, by line range |
| [features.md](features.md) | Every UI option, per tab, with the line where it is built |
| [configuration.md](configuration.md) | Flags, configs, touch buttons, themes, and asset caching |
| [external-services.md](external-services.md) | Network calls, game remotes, metamethod hooks, and hardware overlay APIs |

## Requirements

An executor that provides:

| Needed for | Globals |
| --- | --- |
| Loading UI and assets | `loadstring`, `game:HttpGet` |
| Webhook, compatibility report | `request` / `http_request` / `syn.request` |
| Configs & asset cache | `readfile`, `writefile`, `isfile`, `makefolder` |
| Clipboard | `setclipboard` (or `setrbxclipboard`) |
| Silent aim, emote sync | `hookmetamethod`, `getnamecallmethod`, `checkcaller`, `newcclosure` |
| Server hop persistence | `queue_on_teleport` |
| Hardware overlays (optional) | `DrawingImmediate` (Potassium) or `Drawing` |
| Safe GUI container (optional) | `gethui` |

Missing hook functions disable only the features that need them. The **UNC / sUNC** tab shows what your executor supports. Xeno is detected by name and is treated as hook-unsupported.

## How the script runs

1. Shows a "Script is loading" notification.
2. Prevents double execution through `genv.__FoxnameMM2Runtime`. A second run shows "Script already running!".
3. Loads WindUI using cache-first disk bootstrapping (`Foxname/WindUI_cache.lua`) with fast-path `--[Foxname WindUI Patched]--` idempotency, falling back to multi-mirror network requests only if local cache is absent or corrupt.
4. Preloads core assets (fonts, glass spritesheets, squircles, and window backgrounds) asynchronously via `ContentProvider:PreloadAsync` to eliminate initial interaction freezes.
5. Injects zero-frame-drop animation optimizations into WindUI at compile time (layout solver isolation, hover listener cleanup, targeted tab and dropdown tweens, hardware 2D matrix translation).
6. Builds the window and all tabs using a cooperative 6ms frame budget (`budgetYield`), rendering the UI immediately in Frame 0 without blocking the Roblox task scheduler or dropping frames.
7. Builds the `Hub` state table, then every feature module.
8. Registers each UI element, then restores config values via `Hub.ApplyAutoLoadConfig`.
9. Starts background loops, then shows "Welcome user!" once startup data is ready.

## Editing tips

- The file is large. Search by the UI `Title = "..."` or `Flag = "..."` string instead of scrolling.
- Line numbers in these docs match the current file and drift after edits. To find a section again:
  ```powershell
  Select-String -Path main.luau -Pattern 'Window:Tab\(|^Tabs\.\w+:Section|Hub\.CoinFarm = '
  ```
