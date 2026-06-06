# DOMAIN.md - PongTest

## 1. Project Identity

| Field | Value |
|---|---|
| Full name | PongTest |
| Short name | PongTest |
| Type | Browser-based Pong game |
| Primary platform | Desktop web browser |
| Technology | Vanilla JavaScript with HTML5 Canvas API |
| Framework | Autonomous Duck Deployment Framework 3.5 |
| Requirements document | `docs/requirements.md` |
| Decision record | `DECISIONS.md` |

## 2. What This Project Is

PongTest is a local browser Pong game. It uses a Canvas playfield, two paddles, one ball, keyboard input, basic AI, scoring, and local high-score persistence.

The game is intended to run by opening `index.html` in a modern desktop browser. It does not require installation, account setup, server hosting, network access, or a build step.

## 3. v1.0 Product Scope

### In Scope

- Browser-based Pong running from local static files.
- Vanilla JavaScript with the HTML5 Canvas API.
- Runtime files: `index.html`, `styles.css`, and `game.js`.
- 800 by 500 internal canvas playfield.
- Two player configurations selectable at game start:
  - Two Players.
  - Vs AI.
- Two win modes:
  - First to 10 points.
  - 3 Lives high-score mode for Vs AI.
- Fixed keyboard controls:
  - `W` and `S` for the left paddle.
  - `ArrowUp` and `ArrowDown` for the right human paddle in Two Players mode.
  - Number keys for mode selection.
  - `Enter` to confirm selection.
  - `Space` to serve.
  - `R` to restart from Game Over.
- Basic AI controlling the right paddle in Vs AI mode.
- Paddle and ball collision.
- Top and bottom wall bounce.
- Score, lives, and high-score display.
- Local high-score persistence for 3 Lives mode.
- Game states: Not Started, Ready to Serve, Playing, Point Reset, Game Over.
- No server and no build step.

### Out of Scope

The following are v1.0 non-goals:

- Online multiplayer.
- Server-backed gameplay.
- Global leaderboards.
- User accounts.
- Database storage.
- Mobile or touch controls.
- Sound effects.
- Music.
- Power-ups.
- Obstacles.
- Visual themes.
- Player names.
- Fullscreen mode.
- Pause mode or pause menu.
- Settings menu.
- Remappable controls.
- Multiple AI difficulty levels.
- Predictive AI.
- Timed matches.
- Sudden death.
- Phaser.js.
- p5.js.
- npm setup.
- Bundlers or build tooling.

## 4. Target Users

| User type | Primary need |
|---|---|
| Local player | Open the game in a browser and play immediately. |
| Two local players | Share one keyboard and play a first-to-10 Pong match. |
| Solo player | Play against a basic AI opponent and attempt a local high score. |
| Developer | Implement the game from approved requirements after ADDF dry run approval. |

## 5. Core Gameplay Concepts

| Concept | Meaning |
|---|---|
| Playfield | The 800 by 500 Canvas area where gameplay occurs. |
| Paddle | A vertical rectangle controlled by a human or AI. |
| Ball | The moving object that bounces off paddles and top/bottom boundaries. |
| Two Players | Mode where both paddles are controlled by human keyboard input. |
| Vs AI | Mode where the left paddle is human-controlled and the right paddle is AI-controlled. |
| First to 10 | Match mode where the first side to reach 10 points wins. |
| 3 Lives | Single-player Vs AI high-score mode where the human starts with 3 lives. |
| Local high score | A high score saved in browser-local storage, not a global leaderboard. |
| Ready to Serve | State where the game waits for `Space` before moving the ball. |

## 6. Technology Rules

1. Use vanilla browser APIs only for v1.0.
2. Use Canvas for rendering the playfield, paddles, ball, scores, lives, and prompts.
3. Use `requestAnimationFrame()` for the game loop.
4. Use elapsed time for movement so gameplay is not tied to refresh rate.
5. Use classic script loading, not JavaScript modules.
6. Use browser-local storage only for the 3 Lives high score.
7. Do not introduce external dependencies without a new accepted decision.

## 7. Domain Rules

1. Anything not explicitly in v1.0 scope is deferred.
2. Requirements control implementation; code must not invent gameplay behavior.
3. If an implementation ambiguity appears, return to Design Mode before coding around it.
4. High scores are local-only and not trusted as competitive or anti-cheat data.
5. Browser compatibility must be validated with local file execution.

## 8. File Naming

| File type | Convention | Example |
|---|---|---|
| Project brain files | `UPPER_SNAKE_CASE.md` | `STATE.md` |
| Runtime entry point | Lowercase root HTML | `index.html` |
| Runtime stylesheet | Lowercase root CSS | `styles.css` |
| Runtime script | Lowercase root JavaScript | `game.js` |
| Research notes | Lowercase kebab case | `research/technology-options.md` |
| Documentation pages | Lowercase kebab case | `docs/requirements.md` |
| Sprint folders | `sprint_NNN` | `planning/sprints/sprint_001` |
| Sprint files | Lowercase snake case | `dry_run.md` |
