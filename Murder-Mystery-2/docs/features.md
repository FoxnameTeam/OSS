# Features

Reference for all in-game options per tab.

## Discord / UNC / sUNC (882-1002)

| Option | Notes |
| --- | --- |
| Foxname Community | Real-time member and presence count from Discord invite API. |
| Copy Discord Invite / Refresh Info | Copies community invite link and refreshes stats. |
| Executor & Feature Support | Diagnostic table displaying which executor environment APIs are supported. |

## Visuals (13401-14247)

| Option | Line | Notes |
| --- | --- | --- |
| Player ESP & ESP Style | 13401+ | Highlights character models by match role. |
| Line ESP, Nametag ESP, 360 ESP | | Tracers, player name tags with distance, screen-edge indicators. |
| Gun ESP, Dropped Gun Notify | | Highlights dropped Sheriff gun and sends UI notifications. |
| Bullet Tracer | | Colored tracers with custom duration. |
| Coin ESP | 13483 | Highlight outline for spawned coins (`ESP_Coin`). |
| XRay | 13509 | Makes obstruction parts semi-transparent (`xrayTransparency = 0.72`). Includes mobile button. |
| Shaders & Atmosphere | 14110+ | Shader presets, specular scale, skybox, snowflake density, and fog density. |

## Crosshair (14248-14348)

Custom crosshair rendering with Lucide icon cursor support, size adjustment, and RGB color cycles.

## Combat (14349-14599)

### Aim (14349+)
- **Aim Style**: Smooth camera tracking or silent aim metamethod interception.
- **Controls**: FOV circle slider, wall check toggle, role constraint ("Only Aim While Sheriff"), prediction factor.
- **Mobile Action**: Dedicated Aimlock touch button with draggable positioning.

### Sheriff (14501+)
- Auto-shoot trigger with customizable target body part (Head/Torso).
- On-screen touch button and keyboard keybind activation.

### Murderer (17474+)
- **Throw Knife Button**: On-screen action touch button with draggable positioning and direct toggle synchronization.
- **Combat Aids**: Knife Aura, Hitbox Expander, and Kill All automation.

## Player (15258-15600)

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

## Farm (14600-15257)

- **Progression**: Auto-prestige upon level requirement and automatic seasonal reward claiming.
- **Coin Farm**: Pathfinding and tween-assisted coin collection, bag-full detection, evasion mechanics, and rendering toggles (Black Screen, disable 3D).
- **Server Hopping**: Low player threshold hopping, anti-bot analysis hop, and timeout hop.
- **Event Boxes**: Automatic crate and box purchasing by currency.

## Anims (12763-13195)

Emote wheel synchronization, emote playback speed controls, item synchronization, instant dropped gun retrieval, and wall glitch helper.

## Radio (13196-13400)

Custom audio ID player with local volume settings and FilteringEnabled replication via game sound remotes.

## Teleports (17141-17473)

| Option | Notes |
| --- | --- |
| Quick Teleports | Instant transitions to Murderer, Sheriff, Dropped Gun, Safezone, Lobby, Game Arena, and selected players. |
| TP to Voting Board | Teleports player character directly to the active voting board pad oriented toward the map preview adornee, accompanied by a toast notification displaying the target map name. |
| Auto Map Vote | Background polling cycle that detects active lobby voting across seasonal lobby maps (Normal, Summer, Halloween, Christmas, Easter), teleports to the designated board, tracks vote confirmation, and resets character to loop vote casting. |
| Voting Board Selector | Dropdown selecting active voting pad target (`Board 1`, `Board 2`, or `Board 3`). |

## Settings (18078-19020)

WindUI theme selector, background image customizer, mobile touch button accent palette, and local configuration profile persistence (`Window.ConfigManager`).
