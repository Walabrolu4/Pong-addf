# COMMANDS.md - PongTest

PongTest v1.0 is a local static browser game. It uses vanilla JavaScript, HTML, and CSS. There is no package install, no build step, and no server requirement.

## Setup

No setup command is required for v1.0.

Do not run `npm install` unless a future accepted decision adds a dependency. The current technology decision excludes Phaser.js, p5.js, npm packages, bundlers, and build tooling.

## Run the Game

Use this after `index.html`, `styles.css`, and `game.js` exist from an approved Develop Mode sprint.

### Windows PowerShell

```powershell
Start-Process .\index.html
```

### Browser Manual Run

1. Open the repository folder.
2. Double-click `index.html`.
3. Verify the Not Started state appears.
4. Use the controls listed in `docs/requirements.md`.

## Development

There is no local dev server for v1.0.

Development workflow after dry run approval:

1. Edit approved implementation files only.
2. Refresh the browser.
3. Check the browser console for uncaught errors.
4. Verify behavior against `docs/requirements.md` and the active sprint `acceptance.md`.

## Testing

No automated test command is currently defined.

Manual v1.0 verification must include:

- Opening `index.html` directly from the filesystem.
- Confirming the game runs without network access.
- Checking Two Players First to 10 mode.
- Checking Vs AI First to 10 mode.
- Checking Vs AI 3 Lives high-score mode.
- Confirming `W`, `S`, `ArrowUp`, `ArrowDown`, `Enter`, `Space`, and `R` behavior.
- Confirming the browser console has no uncaught startup errors.
- Confirming no third-party game library is loaded.

## Build

No build command exists for v1.0.

Expected result:

```text
No build required.
```

## Deployment

v1.0 deployment is local static file execution. Hosted deployment is deferred.

To package manually after implementation:

1. Include `index.html`, `styles.css`, and `game.js`.
2. Include project documentation separately.
3. Do not include generated build output.
4. Do not add server configuration.

## Future Commands

If a later decision adds automated tests, a local server, hosted deployment, or build tooling, record the decision in `DECISIONS.md` and update this file before Develop Mode uses the new command.
