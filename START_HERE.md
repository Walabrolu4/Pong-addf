# START_HERE.md - PongTest

Use this file to orient a new developer or a new AI session.

## 1. Current Project

PongTest is a browser-based Pong game. v1.0 will be built with vanilla JavaScript and the HTML5 Canvas API.

The game is designed to run as local static files:

- `index.html`
- `styles.css`
- `game.js`

If these files do not exist yet, the project is still before approved Develop Mode implementation.

## 2. Open and Run the Game

After implementation files exist, open the game immediately:

### Option A - File Explorer

1. Open this repository folder.
2. Double-click `index.html`.
3. Confirm the Not Started state appears.

### Option B - PowerShell

```powershell
Start-Process .\index.html
```

No server, installation, network access, npm install, or build step is required for v1.0.

## 3. Important Files

Load these first in a new AI session:

- `AGENTS.md`
- `STATE.md`
- `DOMAIN.md`
- `SECURITY.md`

Then load files for the task:

- Requirements: `docs/requirements.md`
- Decisions: `DECISIONS.md`
- Open questions: `QUESTIONS.md`
- Risks: `RISKS.md`
- Commands: `COMMANDS.md`
- Style guide: `STYLE_GUIDE.md`

Research and validation files live in:

- `research/technology-options.md`
- `research/game-design-research.md`
- `research/requirements-validation.md`

Sprint files will live in:

- `planning/sprints/sprint_001/requirements.md`
- `planning/sprints/sprint_001/blueprint.md`
- `planning/sprints/sprint_001/acceptance.md`
- `planning/sprints/sprint_001/dry_run.md`
- `planning/sprints/sprint_001/implementation_log.md`

## 4. Current v1.0 Scope

PongTest v1.0 includes:

- Two Players mode.
- Vs AI mode.
- First to 10 mode.
- Vs AI 3 Lives high-score mode.
- Local browser high-score persistence.
- Fixed keyboard controls.
- Canvas rendering.
- Local static file execution.

Anything not listed in `docs/requirements.md` is deferred.

## 5. Before Coding

Do not create or modify `index.html`, `styles.css`, or `game.js` until Develop Mode dry run approval exists.

Before implementation:

1. Review `docs/requirements.md`.
2. Review `DECISIONS.md`.
3. Review `QUESTIONS.md`.
4. Resolve or explicitly accept any open validation questions.
5. Generate the Sprint 001 sprint pack.
6. Enter Develop Mode at Permission Level 0.
7. Produce `dry_run.md`.
8. Wait for human authorization.

## 6. Exact Develop Mode Authorization

Develop Mode may continue only after the human sends:

```text
Dry run approved.
Permission Level [LEVEL] authorized.
Proceed according to requirements.md, blueprint.md, acceptance.md, and dry_run.md.
```

## 7. Quick Manual Acceptance Path

After implementation, check:

1. Open `index.html` locally.
2. Select Two Players and First to 10.
3. Verify both paddles move.
4. Verify scoring to 10 ends the game.
5. Select Vs AI and First to 10.
6. Verify the AI paddle moves and the match can end.
7. Select Vs AI and 3 Lives.
8. Verify lives, current score, and high score behavior.
9. Reload the browser and check high-score persistence.
10. Confirm no server, build, or network access was required.
