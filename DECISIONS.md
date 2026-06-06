# DECISIONS.md - PongTest

Record every decision that would be costly or confusing to reverse here. When superseded, mark it Superseded and record the new decision.

## Decision 1: Technology Stack

**Status:** Accepted  
**Type:** Technology

### Context

PongTest needs a browser game technology before implementation can be planned. The research compared vanilla JavaScript with the HTML5 Canvas API, Phaser.js, and p5.js for a small browser-based Pong game.

### Options Considered

- Vanilla JavaScript with the HTML5 Canvas API.
- Phaser.js.
- p5.js.

### Decision

Use vanilla JavaScript with the HTML5 Canvas API for v1.0.

### Reasoning

The research found that vanilla Canvas provides a built-in browser drawing surface, browser-native input handling, and browser-native animation timing through `requestAnimationFrame()`. It requires no third-party dependency, no CDN, and no build step. The requirements document selects this stack because PongTest is a small self-contained browser game that must run locally without installation.

Phaser.js and p5.js were not chosen for v1.0 because both add third-party library weight. Phaser.js also adds framework concepts beyond what a minimal Pong game needs, while p5.js is less game-specific and still requires the project to implement scoring, collision, and state management.

### Consequences

The project accepts responsibility for implementing the game loop, rendering, input tracking, collision detection, scoring, AI behavior, and game states directly. In exchange, v1.0 has no external game-library dependency, no build process, and fewer moving parts for local browser execution.

---

## Decision 2: Player Configuration

**Status:** Accepted  
**Type:** Design

### Context

PongTest needs to define who can play v1.0 and which play modes are in scope. The game design research compared two human players on the same keyboard, one human player versus an AI opponent, and both options selectable at game start.

### Options Considered

- Two human players on one keyboard.
- One human player versus AI.
- Both options selectable at game start.

### Decision

Support both player configurations at game start: Two Players and Vs AI.

### Reasoning

The research found that two-player keyboard play is closest to classic local Pong and avoids AI complexity, while human-vs-AI makes the game playable alone. The selectable option was identified as more flexible, with the tradeoff that it requires menu/state management and testing of both modes. The requirements document adopts the selectable approach and defines both modes as v1.0 scope.

### Consequences

v1.0 must include a not-started/menu state, player configuration selection, two-player keyboard controls, AI paddle behavior, and acceptance checks for both modes. The project accepts the added UI and testing complexity in exchange for both local multiplayer and solo play.

---

## Decision 3: Win Condition

**Status:** Accepted  
**Type:** Design

### Context

PongTest needs a clear match ending condition so play sessions can finish and be tested. The research compared first-to-N scoring, timed games, and sudden death. It also found that high scores can be saved locally without a server.

### Options Considered

- First to N points, such as 5, 7, 10, or 11.
- Timed game.
- Timed game with sudden death.
- 3-lives high-score mode using local browser storage.

### Decision

Support two v1.0 win modes:

- First to 10 points.
- 3-lives high-score mode for Vs AI.

### Reasoning

The research found that first-to-N scoring is easy to understand, works for local and AI modes, and matches common Pong-style play. The requirements document selects first to 10 as the fixed point-target match. Timed games and sudden death are not selected because they add timer, tie-handling, and additional state complexity.

The 3-lives high-score mode follows the project decision to include a high-score style mode and uses the research finding that browser-local storage can save local personal-best data without a server.

### Consequences

The game must support two scoring paths: a normal two-sided first-to-10 match and a single-player lives-based high-score run. The project accepts additional scoring and game-over logic. Timed matches, sudden death, configurable point targets, global leaderboards, and server-backed score storage are deferred.

---

## Decision 4: Deployment Approach for v1.0

**Status:** Accepted  
**Type:** Architecture

### Context

PongTest needs a v1.0 deployment approach that matches the requirement to run in a browser without installation. The technology research compared local files, GitHub Pages, and static hosts such as Netlify and Vercel.

### Options Considered

- Local static files opened directly in the browser.
- GitHub Pages.
- Netlify.
- Vercel.
- Other static file host.

### Decision

Deploy v1.0 as local static files that run by opening `index.html` directly in a browser.

### Reasoning

The requirements document states that v1.0 must work as a local file, require no server, require no build step, and require no network access. The research found that local files have the least operational setup, while hosted options provide shareable URLs and richer workflows but add platform setup.

### Consequences

v1.0 must avoid server-only assumptions, network dependencies, and build tooling. The game must use browser features that work from local static files. GitHub Pages, Netlify, Vercel, and other hosted deployment options remain possible future choices but are not part of v1.0.

---

## Decision 5: File Structure

**Status:** Accepted  
**Type:** Architecture

### Context

PongTest needs a source file structure before sprint planning. The technology research compared a single self-contained HTML file with multiple local files, and the requirements document defines the v1.0 file structure.

### Options Considered

- Single self-contained HTML file.
- Multiple files: HTML, CSS, and JavaScript.
- Separate development files with bundled or embedded final output.

### Decision

Use a multi-file structure for v1.0:

- `index.html`
- `styles.css`
- `game.js`
- `docs/requirements.md`

### Reasoning

The research found that a single file is the simplest artifact to move or open locally, but becomes harder to maintain as HTML, CSS, and JavaScript grow together. It also found that multiple files improve organization while still supporting local browser use when classic scripts and relative paths are used. The requirements document selects separate HTML, CSS, and JavaScript files for readability and maintainability while still requiring local file execution.

### Consequences

The project accepts a small amount of path-management complexity in exchange for clearer separation of markup, styling, and game logic. v1.0 must avoid JavaScript modules, bundlers, generated build output, and asset loading patterns that would require a local server.

---
