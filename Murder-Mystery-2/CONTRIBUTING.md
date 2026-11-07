# Contributing

Thanks for helping out. This project is licensed under [GPLv3](LICENSE).

## Licensing

- By submitting a contribution you agree it is licensed under GPLv3 (or later), the same as the project.
- Only submit code you wrote or code whose license is GPLv3-compatible. Credit its origin in the PR.
- Keep the license header at the top of `main.luau`. Do not remove it.
- New files need the same header.

## Workflow

1. Fork the repo and create a branch (`fix/aimlock-fov`, `feat/new-esp`).
2. Make a focused change. One feature or fix per PR.
3. Test in a live Murder Mystery 2 server with an executor. Check the console for errors.
4. Open a PR describing what changed and how you tested it.

## Code style

- Luau, tabs for indentation.
- Guard executor globals before use, e.g. `type(fn) == "function"`.
- Keep comments short and only for the *why*. No banners or dividers.
- New UI options need a unique `Flag` so config saving works.
- Remote names and game paths are hardcoded; mention any game update that forced a change.

## Reporting bugs

Open an issue with: executor name, what you did, expected vs actual, and console output.

## Not accepted

Anything that steals accounts or credentials, logs user data, or loads closed-source payloads.
