# Foxname - Murder Mystery 2

Open-source Roblox executor script for **Murder Mystery 2**, built on WindUI.

## Features

| Tab | Highlights |
| --- | --- |
| Visuals | Player / Gun / Nametag / Line / 360 ESP, bullet tracer, XRay, shaders, skybox, fog, snow |
| Crosshair | Custom crosshair styles, RGB, custom cursor |
| Combat | Aimlock, silent aim, FOV, prediction, sheriff auto shoot |
| Player | WalkSpeed, speed glitch, noclip, fly, infinite jump, anti fling, invisibility |
| Farm | Coin farm, auto prestige, auto claim, server hop, anti bot, webhook, event boxes |
| Anims | In-game emote / item sync, custom emotes, instant gun pickup |
| Radio | Local and FE radio |
| Teleports | Lobby, map, murderer |

Full details: [docs/README.md](docs/README.md).

## Usage

Run [`main.luau`](main.luau) in a Roblox executor. It needs `getgenv`, `loadstring`, `game:HttpGet`, `writefile`/`readfile`, and `request`.

```lua
loadstring(game:HttpGet("https://raw.githubusercontent.com/FoxnameTeam/OSS/main/Murder-Mystery-2/main.luau"))()
```

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md).

## License

Licensed under the [GNU GPLv3](LICENSE). Forks and derivatives must remain GPLv3 and keep the license header in `main.luau`.

Community: https://discord.gg/v8ZPq4y2nD
