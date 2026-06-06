# PongTest Requirements

## 1. Project Overview

PongTest is a browser-based Pong game for desktop browsers. The game runs from local static files without installation, accounts, a backend server, or a build step.

v1.0 supports:

- A selectable player configuration at game start.
- Two human players sharing one keyboard.
- One human player versus a basic AI opponent.
- A first-to-10 points match mode.
- A 3-lives high-score mode for one-player versus AI play.

## 2. Technology Decision

PongTest v1.0 uses vanilla JavaScript with the HTML5 Canvas API.

This choice follows `research/technology-options.md`, which found that vanilla Canvas:

- Provides a built-in browser drawing surface.
- Requires no third-party game library.
- Can run as plain local HTML, CSS, and JavaScript.
- Is suitable for a small self-contained Pong game.

The tradeoff is that PongTest must implement its own game loop, rendering, input tracking, collision rules, scoring, AI behavior, and game states. Phaser.js and p5.js are excluded from v1.0.

## 3. Gameplay Requirements

### 3.1 Playfield

- The game canvas must use an internal coordinate size of 800 pixels wide by 500 pixels tall.
- The playfield origin must be the top-left corner.
- The left goal boundary is the left edge of the canvas.
- The right goal boundary is the right edge of the canvas.
- The top and bottom edges are bounce boundaries.

### 3.2 Player Configuration

- On load, the game must show a not-started state where the player can choose a player configuration.
- The available player configurations must be:
  - Two Players.
  - Vs AI.
- Two Players mode must use a left human paddle and a right human paddle.
- Vs AI mode must use a left human paddle and a right AI paddle.

### 3.3 Win Mode Selection

- After or during player configuration selection, the game must allow win mode selection.
- First to 10 mode must be available for Two Players and Vs AI.
- 3 Lives mode must be available for Vs AI.
- 3 Lives mode must not be offered as a Two Players win mode in v1.0.

### 3.4 Ball Behaviour

- The ball must be drawn as a white square or circle with a 10 pixel visual size.
- At the start of each match, the ball must be placed at the center of the playfield.
- After each point, life loss, or AI miss reset, the ball must return to the center of the playfield.
- The ball must not move until the player starts the serve.
- The first serve of a match must choose a horizontal direction randomly.
- After a score in First to 10 mode, the next serve must travel toward the player who conceded the point.
- The ball must move with both horizontal and vertical velocity.
- The ball's initial speed must be 320 pixels per second.
- The ball must use elapsed time from the animation loop so movement speed is not tied to monitor refresh rate.
- When the ball hits the top or bottom boundary, its vertical direction must reverse.
- When the ball hits a paddle while moving toward that paddle, its horizontal direction must reverse.
- Paddle bounce angle must depend on where the ball hits the paddle:
  - A center hit produces a shallow return.
  - An edge hit produces a steeper return.
  - The maximum outgoing angle must be capped at 60 degrees from the horizontal direction.
- The ball must not become perfectly vertical after a paddle hit.
- The ball must not remain stuck inside a paddle or wall after collision resolution.
- Automatic ball speed acceleration is not required for v1.0.

### 3.5 Paddle Behaviour

- Each paddle must be drawn as a rectangle.
- Paddle size must be 12 pixels wide by 90 pixels tall.
- The left paddle must be placed 30 pixels from the left edge.
- The right paddle must be placed 30 pixels from the right edge.
- Paddles must start vertically centered at the beginning of each match.
- Paddles must move only up and down.
- Paddles must move at 420 pixels per second while their movement key is held.
- Paddles must stop at the top and bottom playfield boundaries.
- Paddles must not move outside the visible canvas.

### 3.6 AI Opponent Behaviour

- The AI paddle is used only in Vs AI mode.
- The AI must control the right paddle.
- The AI must move toward the ball's vertical position when the ball is moving toward the AI side.
- The AI must move toward the vertical center of the playfield when the ball is moving away from the AI side.
- The AI paddle speed must be lower than the human paddle speed.
- The AI paddle speed must be 330 pixels per second.
- The AI must be beatable by a human player through angled returns.
- Multiple AI difficulty levels are excluded from v1.0.

### 3.7 First to 10 Scoring

- Both sides start with 0 points.
- If the ball exits the left edge, the right side gains 1 point.
- If the ball exits the right edge, the left side gains 1 point.
- After a point, the ball and paddles must reset to their starting positions.
- The match ends when either side reaches 10 points.
- The game over state must identify the winning side.

### 3.8 3 Lives High-Score Scoring

- 3 Lives mode is a single-player Vs AI mode.
- The human player starts with 3 lives.
- The current run score starts at 0.
- Each successful human paddle return increases the current run score by 1.
- If the ball exits the left edge, the human player loses 1 life.
- If the ball exits the right edge, the ball resets and the run continues.
- The game ends when the human player has 0 lives.
- The game must display the current run score during play.
- The game must display the saved high score during play.
- If the current run score is greater than the saved high score at game over, the saved high score must update.

### 3.9 Game States

- Not Started: The game shows player configuration and win mode choices.
- Ready to Serve: The match has valid choices and waits for the player to start the ball.
- Playing: The ball and paddles update each animation frame.
- Point Reset: A point, life loss, or AI miss occurred; scores/lives update and the ball returns to center.
- Game Over: The match or high-score run has ended and the player can restart.
- Paused is not a v1.0 game state.

## 4. Input Requirements

### 4.1 Menu and Global Inputs

- `1` must select Two Players.
- `2` must select Vs AI.
- `3` must select First to 10 mode.
- `4` must select 3 Lives mode when Vs AI is selected.
- `Enter` must confirm the current valid selections and enter Ready to Serve.
- `Space` must start the serve from Ready to Serve.
- `R` must restart from Game Over and return to Not Started.

### 4.2 Paddle Inputs

- Left paddle up: `W`.
- Left paddle down: `S`.
- Right paddle up in Two Players mode: `ArrowUp`.
- Right paddle down in Two Players mode: `ArrowDown`.
- In Vs AI mode, the right paddle must ignore human arrow-key movement.

### 4.3 Browser Input Behaviour

- Holding a movement key must move the matching paddle continuously.
- Releasing a movement key must stop that paddle's movement in that direction.
- Arrow keys and `Space` must not scroll the page while the game is focused.
- Controls are fixed in v1.0; remappable controls are excluded.

## 5. Visual Requirements

- The page must show the 800 by 500 game canvas centered in the browser viewport.
- The playfield background must be black.
- Paddles and ball must be white.
- A vertical center divider must be visible in a muted grey.
- Text must use high contrast against the background.
- In First to 10 mode, the left and right scores must be visible at the top of the playfield.
- In 3 Lives mode, the display must show:
  - Current run score.
  - Saved high score.
  - Remaining lives.
- The Not Started state must show the available player configuration and win mode choices.
- Ready to Serve must show a visible prompt to press `Space`.
- Game Over must show the winner or final run score and a visible prompt to press `R`.

## 6. Technical Requirements

- The game must run in a modern desktop browser without installation.
- The game must work by opening `index.html` locally from the filesystem.
- The game must not require a local development server for v1.0.
- The game must not require a build step.
- The game must not use Phaser.js, p5.js, or another external game library.
- The game must not require network access.
- The game must use a classic script file rather than JavaScript modules, so local file loading remains compatible.
- The game loop must use `requestAnimationFrame()`.
- High-score persistence must use browser-local storage.
- The local high-score storage key must be documented in the implementation.
- The game must tolerate missing or cleared local storage by treating the high score as 0.

## 7. Non-Goals for v1.0

Anything not listed as in scope is deferred.

Explicit v1.0 non-goals:

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
- Bundlers or build tooling.

## 8. File Structure

The v1.0 game must consist of these files:

- `index.html` - the browser entry point, canvas element, and static UI text.
- `styles.css` - page layout, canvas presentation, and visual styling.
- `game.js` - game state, input handling, AI behavior, physics, scoring, rendering, and local high-score persistence.
- `docs/requirements.md` - this requirements document.

No image, audio, font, or generated build files are required for v1.0.

## 9. v1.0 Acceptance Criteria

### 9.1 Startup and Local Execution

- Opening `index.html` directly in a desktop browser shows the Not Started state.
- The game runs without a server.
- The game runs without network access.
- The browser console has no uncaught errors during startup.

### 9.2 Mode Selection

- Pressing `1` selects Two Players.
- Pressing `2` selects Vs AI.
- Pressing `3` selects First to 10 mode.
- Pressing `4` selects 3 Lives mode only when Vs AI is selected.
- Pressing `Enter` with a valid configuration enters Ready to Serve.

### 9.3 Two Players First to 10

- In Two Players First to 10 mode, `W` and `S` move the left paddle.
- In Two Players First to 10 mode, `ArrowUp` and `ArrowDown` move the right paddle.
- Pressing `Space` starts the serve.
- The ball bounces off the top and bottom playfield boundaries.
- The ball bounces off both paddles.
- A ball exiting the left edge awards 1 point to the right player.
- A ball exiting the right edge awards 1 point to the left player.
- The match ends when either player reaches 10 points.
- The Game Over state identifies the winning player.

### 9.4 Vs AI First to 10

- In Vs AI First to 10 mode, `W` and `S` move the human paddle.
- The AI controls the right paddle without arrow-key input.
- The AI tracks the ball and can return the ball during normal play.
- The human can score against the AI.
- The AI can score against the human.
- The match ends when either side reaches 10 points.

### 9.5 Vs AI 3 Lives High Score

- In 3 Lives mode, the human starts with exactly 3 lives.
- The display shows current score, saved high score, and remaining lives.
- Each successful human paddle return increases the current score by exactly 1.
- Each ball exit through the left edge reduces lives by exactly 1.
- The game ends when lives reach 0.
- If the final current score is higher than the saved high score, the saved high score updates.
- The saved high score persists after reloading the page in the same browser when local storage is available.

### 9.6 Restart

- Pressing `R` from Game Over returns to the Not Started state.
- Restarting clears current match score, current run score, and remaining lives.
- Restarting does not clear the saved high score.

### 9.7 Scope Verification

- No sound plays in v1.0.
- No mobile or touch controls are present in v1.0.
- No online multiplayer or server calls are present in v1.0.
- No third-party game library is loaded in v1.0.
- No build output is required to run the game.
