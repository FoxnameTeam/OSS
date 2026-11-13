# Features

Reference for all in-game options per tab.

## Discord / UNC / sUNC (1121-1390)

| Option | Notes |
| --- | --- |
| Foxname Community | Real-time member and presence count from Discord invite API. |
| Copy Discord Invite / Refresh Info | Copies community invite link and refreshes stats. |
| Executor & Feature Support | Diagnostic table displaying which executor environment APIs are supported. |

## Visuals (15825-16716)

| Option | Notes |
| --- | --- |
| Player ESP & ESP Style | Highlights character models by match role (Innocent, Sheriff, Murderer, Zombie). |
| Line ESP, Nametag ESP, 360 ESP | Tracers (rendered with 3-tier hardware overlay: `DrawingImmediate` -> `Drawing` -> `Frame`), player name tags with distance, screen-edge indicators. |
| Gun ESP, Dropped Gun Notify | Highlights dropped Sheriff gun and sends UI notifications. |
| Bullet Tracer | Colored tracers with custom duration. |
| Coin ESP | Highlight outline for spawned coins (`ESP_Coin`). |
| XRay | Makes obstruction parts semi-transparent (`xrayTransparency = 0.72`). Includes mobile button. |
| Shaders & Atmosphere | Shader presets, specular scale, skybox, snowflake density, and fog density. |

## Crosshair (16717-16817)

Custom crosshair rendering with Lucide icon cursor support, size adjustment, and RGB color cycles.

## Combat (16818-17068, 20007-20641)

### Aim (16818+)
- **Aim Style**: Smooth camera tracking or silent aim metamethod interception.
- **Controls**: FOV circle slider (rendered with 3-tier hardware overlay: `DrawingImmediate` -> `Drawing` -> `Frame`), wall check toggle, role constraint ("Only Aim While Sheriff"), prediction factor.
- **Mobile Action**: Dedicated Aimlock touch button with draggable positioning.

### Sheriff (16970+)
- Auto-shoot trigger with customizable target body part (Head/Torso), multi-attempt reload retry, clear-shot fallback, and safezone return.
- On-screen touch button and keyboard keybind activation.

### Murderer (20007+)
- **Throw Knife Button**: On-screen action touch button with draggable positioning and direct toggle synchronization.
- **Combat Aids**: Knife Aura, Hitbox Expander, and Kill All automation.

## Player (17936-18840)

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

## Farm (17069-17935)

- **Progression**: Auto-prestige upon level requirement and automatic seasonal reward claiming.
- **Coin Farm Core**:
  - Farm Modes: `CFrame`, `Tween`, and `Lobby` (stays in Lobby with a safe delay, syncs server position before touching the coin/candy, and returns to Lobby).
  - Targeting Methods: Advanced (optimal cluster pathing) or Simple (nearest coin).
  - Movement Modes: Stop and Go (stealthy step intervals) or Continuous (steady navigation).
  - End Round Modes: `Normal (shooting)`, `Shoot only if Gun Dropped`, `Fling Murderer`, or `Fling All`, plus safezone XP waiting.
  - Safety & Evasion: Murderer avoidance radius, safezone teleports, black screen CPU throttling, rendering suppression.
  - Automation: Anti-bot server hopping, player threshold triggers, scheduled hop timer, Discord webhook statistics dispatch.
  - Event Boxes: Auto-buy seasonal crates with selectable currencies.

## Anims (15175-15615)

- Emote browser with synchronization hooks.
- Custom animation player and playback speed multiplier.
- Instant gun pickup helper.

## Radio (15616-15824)

- Client-side and FE audio playback.
- Track search, custom Sound ID input, and volume normalization.

## Teleports (19673-20006)

- Instant location presets: Murderer, Sheriff, Dropped Gun, Safezone, Lobby.
- Lobby Map Voting: Automated voting board interaction (`runAutoMapVoteCycle`) with configurable board target.

## Settings (20642-21778)

- Configuration manager: Save, load, and auto-restore profiles (`WindUI/Foxname_MM2/config/`).
- Mobile action button customization: Shape, size, and accent styling.
- Interface themes: Built-in presets and custom background image URLs.
- Automation toggles: Auto execute on teleport, auto save (60s timer), and auto load on startup.
