# Features

Reference for all in-game options per tab.

## Discord / UNC / sUNC (869-998)

| Option | Notes |
| --- | --- |
| Foxname Community | Real-time member and presence count from Discord invite API. |
| Copy Discord Invite / Refresh Info | Copies community invite link and refreshes stats. |
| Executor & Feature Support | Diagnostic table displaying which executor environment APIs are supported. |

## Visuals (14492-15383)

| Option | Line | Notes |
| --- | --- | --- |
| Player ESP & ESP Style | 14492+ | Highlights character models by match role (Innocent, Sheriff, Murderer, Zombie). |
| Line ESP, Nametag ESP, 360 ESP | 14530+ | Tracers (rendered with 3-tier hardware overlay: `DrawingImmediate` -> `Drawing` -> `Frame`), player name tags with distance, screen-edge indicators. |
| Gun ESP, Dropped Gun Notify | | Highlights dropped Sheriff gun and sends UI notifications. |
| Bullet Tracer | | Colored tracers with custom duration. |
| Coin ESP | 14573 | Highlight outline for spawned coins (`ESP_Coin`). |
| XRay | 14596 | Makes obstruction parts semi-transparent (`xrayTransparency = 0.72`). Includes mobile button. |
| Shaders & Atmosphere | 15246+ | Shader presets, specular scale, skybox, snowflake density, and fog density. |

## Crosshair (15384-15484)

Custom crosshair rendering with Lucide icon cursor support, size adjustment, and RGB color cycles.

## Combat (15485-15735, 18659-19269)

### Aim (15485+)
- **Aim Style**: Smooth camera tracking or silent aim metamethod interception.
- **Controls**: FOV circle slider (rendered with 3-tier hardware overlay: `DrawingImmediate` -> `Drawing` -> `Frame`), wall check toggle, role constraint ("Only Aim While Sheriff"), prediction factor.
- **Mobile Action**: Dedicated Aimlock touch button with draggable positioning.

### Sheriff (15637+)
- Auto-shoot trigger with customizable target body part (Head/Torso).
- On-screen touch button and keyboard keybind activation.

### Murderer (18659+)
- **Throw Knife Button**: On-screen action touch button with draggable positioning and direct toggle synchronization.
- **Combat Aids**: Knife Aura, Hitbox Expander, and Kill All automation.

## Player (16589-17489)

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

## Farm (15736-16588)

- **Progression**: Auto-prestige upon level requirement and automatic seasonal reward claiming.
- **Coin Farm Core**:
  - Targeting Methods: Advanced (optimal cluster pathing) or Simple (nearest coin).
  - Movement Modes: Stop and Go (stealthy step intervals) or Continuous (steady navigation).
  - Safety & Evasion: Murderer avoidance radius, safezone teleports, black screen CPU throttling, rendering suppression.
  - Automation: Anti-bot server hopping, player threshold triggers, scheduled hop timer, Discord webhook statistics dispatch.
  - Event Boxes: Auto-buy seasonal crates with selectable currencies.

## Anims (13846-14286)

- Emote browser with synchronization hooks.
- Custom animation player and playback speed multiplier.
- Instant gun pickup helper.

## Radio (14287-14491)

- Client-side and FE audio playback.
- Track search, custom Sound ID input, and volume normalization.

## Teleports (18326-18658)

- Instant location presets: Murderer, Sheriff, Dropped Gun, Safezone, Lobby.
- Lobby Map Voting: Automated voting board interaction (`runAutoMapVoteCycle`) with configurable board target.

## Settings (19270-20359)

- Configuration manager: Save, load, and auto-restore profiles (`WindUI/Foxname_MM2/config/`).
- Mobile action button customization: Shape, size, and accent styling.
- Interface themes: Built-in presets and custom background image URLs.
- Automation toggles: Auto execute on teleport, auto save (60s timer), and auto load on startup.
