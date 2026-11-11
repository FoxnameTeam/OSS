# Features

Reference for all in-game options per tab.

## Discord / UNC / sUNC (870-990)

| Option | Notes |
| --- | --- |
| Foxname Community | Real-time member and presence count from Discord invite API. |
| Copy Discord Invite / Refresh Info | Copies community invite link and refreshes stats. |
| Executor & Feature Support | Diagnostic table displaying which executor environment APIs are supported. |

## Visuals (14352-15243)

| Option | Line | Notes |
| --- | --- | --- |
| Player ESP & ESP Style | 14352+ | Highlights character models by match role (Innocent, Sheriff, Murderer, Zombie). |
| Line ESP, Nametag ESP, 360 ESP | | Tracers, player name tags with distance, screen-edge indicators. |
| Gun ESP, Dropped Gun Notify | | Highlights dropped Sheriff gun and sends UI notifications. |
| Bullet Tracer | | Colored tracers with custom duration. |
| Coin ESP | 14433 | Highlight outline for spawned coins (`ESP_Coin`). |
| XRay | 14456 | Makes obstruction parts semi-transparent (`xrayTransparency = 0.72`). Includes mobile button. |
| Shaders & Atmosphere | 15106+ | Shader presets, specular scale, skybox, snowflake density, and fog density. |

## Crosshair (15244-15344)

Custom crosshair rendering with Lucide icon cursor support, size adjustment, and RGB color cycles.

## Combat (15345-15595, 18519-19129)

### Aim (15345+)
- **Aim Style**: Smooth camera tracking or silent aim metamethod interception.
- **Controls**: FOV circle slider, wall check toggle, role constraint ("Only Aim While Sheriff"), prediction factor.
- **Mobile Action**: Dedicated Aimlock touch button with draggable positioning.

### Sheriff (15497+)
- Auto-shoot trigger with customizable target body part (Head/Torso).
- On-screen touch button and keyboard keybind activation.

### Murderer (18519+)
- **Throw Knife Button**: On-screen action touch button with draggable positioning and direct toggle synchronization.
- **Combat Aids**: Knife Aura, Hitbox Expander, and Kill All automation.

## Player (16449-17350)

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

## Farm (15596-16448)

- **Progression**: Auto-prestige upon level requirement and automatic seasonal reward claiming.
- **Coin Farm Core**:
  - **Movement Modes**: `Stop and Go` (settles for 0.3s after coin touch) and `Continuous` (touches in-flight within 4 studs and immediately transitions to next coin without stopping).
  - **Targeting Methods**:
    - `Advanced method`: Precise 3D pathfinding evaluating all map coins sorted by distance. Checks competitor movement velocity, horizontal approach direction, and arrival time comparisons against local player speed. Rejects coins in different vertical floors (height > 10 studs), coins in competitor touch range, and coins inside murderer danger radius (<= 30 studs). Guaranteed to pick the closest uncontested coin, or closest coin if all are contested.
    - `Simple method`: Top-K candidate pool with deterministic per-player `UserId` distribution or random selection for multi-bot environments.
  - **Lobby Coin Farm**: Teleports from lobby to coins and immediately returns after collection while respecting bag-full, XP farm, and murderer safety.
  - **End Round Modes**: `Normal (shooting)`, `Shoot only if Gun Dropped`, `Fling Murderer`, `Fling All`.
  - **Evasion & Safety**: Furthest-spawn safe teleports, noclip limb stabilization, and transit evasion grace windows.
  - **Display & Performance**: Black screen overlay and 3D rendering disabling toggles.
- **Server Hopping**: Low player count hopping, anti-bot hop, and timer-based hopping with configurable intervals.
- **Event Boxes**: Automatic crate and box purchasing by currency.

## Anims (13706-14146)

Emote wheel synchronization, emote playback speed controls, item synchronization, instant dropped gun retrieval, and wall glitch helper.

## Radio (14147-14351)

Custom audio ID player with local volume settings and FilteringEnabled replication via game sound remotes.

## Teleports (18186-18518)

| Option | Notes |
| --- | --- |
| Quick Teleports | Instant transitions to Murderer, Sheriff, Dropped Gun, Safezone, Lobby, Game Arena, and selected players. |
| TP to Voting Board | Teleports player character directly to the active voting board pad oriented toward the map preview adornee, accompanied by a toast notification displaying the target map name. |
| Auto Map Vote | Background polling cycle that detects active lobby voting across seasonal lobby maps (Normal, Summer, Halloween, Christmas, Easter), teleports to the designated board, tracks vote confirmation, and resets character to loop vote casting. |
| Voting Board Selector | Dropdown selecting active voting pad target (`Board 1`, `Board 2`, or `Board 3`). |

## Settings (19130-20173)

- **Auto Execute**: Toggles automatic script re-execution upon server hops via `queue_on_teleport`.
- **Auto Load Config**: Automatically loads designated profile on script startup.
- **Auto Save Config**: Periodically persists active settings to disk.
- **Theming & Profiles**: WindUI theme selector, background image customizer, mobile touch button accent palette, and local configuration profile persistence (`Window.ConfigManager`).
