# Features

Reference for all in-game options per tab.

## Discord / UNC / sUNC (765-890)

| Option | Notes |
| --- | --- |
| Foxname Community | Real-time member and presence count from Discord invite API. |
| Copy Discord Invite / Refresh Info | Copies community invite link and refreshes stats. |
| Executor & Feature Support | Diagnostic table displaying which executor environment APIs are supported. |

## Visuals (13237-14082)

| Option | Line | Notes |
| --- | --- | --- |
| Player ESP & ESP Style | 13237+ | Highlights character models by match role. |
| Line ESP, Nametag ESP, 360 ESP | | Tracers, player name tags with distance, screen-edge indicators. |
| Gun ESP, Dropped Gun Notify | | Highlights dropped Sheriff gun and sends UI notifications. |
| Bullet Tracer | | Colored tracers with custom duration. |
| Coin ESP | 13319 | Highlight outline for spawned coins (`ESP_Coin`). |
| XRay | 13345 | Makes obstruction parts semi-transparent (`xrayTransparency = 0.72`). Includes mobile button. |
| Shaders & Atmosphere | 13950+ | Shader presets, specular scale, skybox, snowflake density, and fog density. |

## Crosshair (14084-14155)

Custom crosshair rendering with Lucide icon cursor support, size adjustment, and RGB color cycles.

## Combat (14185-14420)

### Aim (14185+)
- **Aim Style**: Smooth camera tracking or silent aim metamethod interception.
- **Controls**: FOV circle slider, wall check toggle, role constraint ("Only Aim While Sheriff"), prediction factor.
- **Mobile Action**: Dedicated Aimlock touch button with draggable positioning.

### Sheriff (14337+)
- Auto-shoot trigger with customizable target body part (Head/Torso).
- On-screen touch button and keyboard keybind activation.

## Player (15084-15383)

| Option | Notes |
| --- | --- |
| WalkSpeed / JumpPower | Humanoid property modifiers. |
| Speed Glitch | Jump-assisted forward propulsion multiplier. |
| Noclip | Step-bound part collision suppression with touch button toggle. |
| Anti Fling | Velocity cancellation protecting against physics griefing. |
| Flight | Directional velocity controller with configurable speed slider. |
| Infinite Jump | Jump request connection bypass. |
| Invisibility | Seat-based character offset technique. |
| Jerk | Custom character motion simulation. |

## Farm (14431-15057)

- **Progression**: Auto-prestige upon level requirement and automatic seasonal reward claiming.
- **Coin Farm**: Pathfinding and tween-assisted coin collection, bag-full detection, evasion mechanics, and rendering toggles (Black Screen, disable 3D).
- **Server Hopping**: Low player threshold hopping, anti-bot analysis hop, and timeout hop.
- **Event Boxes**: Automatic crate and box purchasing by currency.

## Anims (12599-12807)

Emote wheel synchronization, emote playback speed controls, item synchronization, instant dropped gun retrieval, and wall glitch helper.

## Radio (12962-13102)

Custom audio ID player with local volume settings and FilteringEnabled replication via game sound remotes.

## Teleports (16893-16965)

Instant position transitions: Murderer, Sheriff, Dropped Gun, Safezone, Lobby, Game Arena, and selected players.

## Settings (17792-18728)

WindUI theme selector, background image customizer, mobile touch button accent palette, and local configuration profile persistence (`Window.ConfigManager`).
