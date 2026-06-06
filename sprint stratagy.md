# Sprint Strategy - PongTest

This document lays out the recommended sprint order for taking PongTest from the current planning state to a reviewed v1.0 release. Each implementation sprint must still get its own ADDF sprint pack and Develop Mode dry run before any game code is written.

## Current Starting Point

Project state:

- Project brain files are generated.
- `docs/requirements.md` exists.
- `DECISIONS.md` records the major accepted decisions.
- `QUESTIONS.md` contains open validation questions that should be resolved before implementation.
- Runtime files do not exist yet: `index.html`, `styles.css`, and `game.js`.

v1.0 target:

- Local browser Pong built with vanilla JavaScript and HTML5 Canvas.
- Two Players mode.
- Vs AI mode.
- First to 10 mode.
- Vs AI 3 Lives high-score mode.
- No server, no build step, no external game library.

## Sprint 000 - Requirements Closure

**Mode:** Design Mode  
**Goal:** Resolve ambiguity before any implementation sprint begins.

### Scope

- Review `research/requirements-validation.md`.
- Resolve or explicitly accept all open questions in `QUESTIONS.md`.
- Update `docs/requirements.md` where needed.
- Update `DECISIONS.md` if any answer changes project direction.
- Confirm v1.0 non-goals remain unchanged.

### Outputs

- Updated `QUESTIONS.md`.
- Updated `docs/requirements.md` if needed.
- Updated `DECISIONS.md` if needed.
- Ready-to-plan Sprint 001 scope.

### Exit Criteria

- No implementation-blocking open questions remain.
- Requirements are specific enough for a dry run.

## Sprint 001 - Static Game Shell

**Mode:** Develop Mode after approved dry run  
**Goal:** Create the runnable browser shell with Canvas and basic state display.

### Scope

- Create `index.html`.
- Create `styles.css`.
- Create `game.js`.
- Load `styles.css` and `game.js` from `index.html` using local relative paths.
- Create the 800 by 500 Canvas.
- Draw the black playfield, center divider, static paddles, static ball, and basic text.
- Implement initial Not Started state display.
- Confirm the page opens locally without a server.

### Not In Scope

- Ball movement.
- Paddle movement.
- Scoring.
- AI.
- Local storage.

### Exit Criteria

- Opening `index.html` locally shows the game shell.
- Browser console has no uncaught startup errors.
- No network or build step is required.

## Sprint 002 - Input and Game State Foundation

**Mode:** Develop Mode after approved dry run  
**Goal:** Implement menu input and core state transitions without full gameplay.

### Scope

- Implement fixed keyboard input tracking.
- Implement mode selection:
  - `1` for Two Players.
  - `2` for Vs AI.
  - `3` for First to 10.
  - `4` for 3 Lives when valid.
- Implement `Enter` to confirm valid selections.
- Implement Ready to Serve state.
- Implement `Space` to begin play.
- Implement `R` restart from Game Over.
- Prevent `Space` and arrow keys from scrolling the page while the game is focused.

### Not In Scope

- Full collision rules.
- AI behavior.
- High-score persistence.

### Exit Criteria

- All valid menu selections work.
- Invalid menu behavior matches resolved requirements.
- State labels/prompts match the active state.

## Sprint 003 - Core Two-Player Pong

**Mode:** Develop Mode after approved dry run  
**Goal:** Build the complete Two Players First to 10 game loop.

### Scope

- Move left paddle with `W` and `S`.
- Move right paddle with `ArrowUp` and `ArrowDown`.
- Move ball using `requestAnimationFrame()` and elapsed time.
- Implement top and bottom wall bounce.
- Implement paddle collision.
- Implement resolved paddle bounce-angle behavior.
- Implement left/right scoring.
- Implement point reset behavior.
- Implement First to 10 Game Over.
- Implement restart back to Not Started.

### Not In Scope

- Vs AI.
- 3 Lives mode.
- Local high score.

### Exit Criteria

- Two Players First to 10 is playable from start to finish.
- Either side can score.
- Match ends at 10 points.
- Restart clears match score.

## Sprint 004 - Vs AI First to 10

**Mode:** Develop Mode after approved dry run  
**Goal:** Add the basic AI opponent and make Vs AI First to 10 playable.

### Scope

- Add right-paddle AI behavior.
- Use the resolved AI acceptance baseline.
- Ensure human arrow keys do not control the AI paddle.
- Support Vs AI First to 10 scoring.
- Verify human can score against AI.
- Verify AI can score against human.

### Not In Scope

- Multiple AI difficulty levels.
- Predictive AI.
- 3 Lives high-score mode.

### Exit Criteria

- Vs AI First to 10 is playable from start to finish.
- AI paddle movement follows the requirements.
- Match ends at 10 points for either side.

## Sprint 005 - 3 Lives High-Score Mode

**Mode:** Develop Mode after approved dry run  
**Goal:** Add the single-player 3 Lives mode and local high-score persistence.

### Scope

- Enable 3 Lives mode only for Vs AI.
- Start the human player with 3 lives.
- Implement the resolved scoring event for successful human returns.
- Decrease lives on human miss.
- Reset ball and/or paddles according to resolved requirements.
- End game when lives reach 0.
- Save local high score with browser-local storage.
- Treat missing or cleared storage as high score 0.

### Not In Scope

- Global leaderboard.
- User accounts.
- Server-backed persistence.
- Match history.

### Exit Criteria

- 3 Lives mode is playable from start to Game Over.
- Current score increments correctly.
- Lives decrement correctly.
- High score persists after reload in supported browsers when local storage is available.

## Sprint 006 - Visual and Acceptance Hardening

**Mode:** Develop Mode after approved dry run  
**Goal:** Bring visuals, prompts, and edge-case behavior up to v1.0 acceptance quality.

### Scope

- Apply final visual colors from resolved requirements.
- Ensure score, lives, high score, prompts, and Game Over messages are visible.
- Verify text remains readable on the black playfield.
- Fix edge cases found during manual testing:
  - Ball sticking.
  - Double scoring.
  - Multiple hit counting.
  - Invalid menu state.
  - Restart state leaks.
- Confirm no v1.0 non-goals were added.

### Not In Scope

- New features.
- Sound.
- Themes.
- Mobile controls.
- Pause/settings menus.

### Exit Criteria

- All acceptance criteria in `docs/requirements.md` pass or have documented exceptions.
- No uncaught console errors occur during normal play.
- Manual test notes are ready for human review.

## Sprint 007 - Release Readiness and Human Review

**Mode:** Design Mode, with Develop Mode only if approved fixes are needed  
**Goal:** Close v1.0 with review artifacts and release documentation.

### Scope

- Generate sprint retrospective.
- Generate `human_review.md` from acceptance criteria.
- Update `VERSION.md` when v1.0 is approved.
- Update `CHANGELOG.md`.
- Confirm `COMMANDS.md` still matches how the game runs.
- Confirm `START_HERE.md` accurately helps a new developer/player.

### Not In Scope

- New gameplay work unless human review finds blocking issues and a new dry run approves fixes.

### Exit Criteria

- Human review is complete.
- Release docs are current.
- v1.0 can be opened locally and played through all supported modes.

## Recommended Sprint Order

1. Sprint 000 - Requirements Closure.
2. Sprint 001 - Static Game Shell.
3. Sprint 002 - Input and Game State Foundation.
4. Sprint 003 - Core Two-Player Pong.
5. Sprint 004 - Vs AI First to 10.
6. Sprint 005 - 3 Lives High-Score Mode.
7. Sprint 006 - Visual and Acceptance Hardening.
8. Sprint 007 - Release Readiness and Human Review.

## Notes for Sprint Planning

- Keep each sprint small enough to verify manually.
- Do not combine Sprint 003, Sprint 004, and Sprint 005 unless the dry run is very clear and the human approves the larger scope.
- Each Develop Mode sprint needs a sprint pack and dry run before implementation.
- If a sprint uncovers ambiguity, return to Design Mode rather than inventing behavior in code.
- v1.0 ends when all accepted requirements pass human review, not when the code merely runs.
