# Game Design Research for Browser Pong

Research Mode output. This note identifies design decisions for a browser-based Pong game before requirements are written. It does not recommend a final choice, write requirements, or include game code.

## Sources Checked

- MDN KeyboardEvent docs: keyboard events report low-level key interactions; `KeyboardEvent.key` accounts for keyboard layout and modifier state. Source: https://developer.mozilla.org/en-US/docs/Web/API/KeyboardEvent
- MDN `requestAnimationFrame()` docs: browser animation timing should account for callback timestamps rather than assuming a fixed 60 FPS. Source: https://developer.mozilla.org/en-US/docs/Web/API/Window/requestAnimationFrame
- MDN Web Storage API docs: `localStorage` stores key/value pairs by origin and persists after browser close/reopen; private browsing and local `file://` behavior have caveats. Source: https://developer.mozilla.org/en-US/docs/Web/API/Web_Storage_API
- MDN `localStorage` docs: `localStorage` has no expiration time but behavior for files opened directly from local filesystem is undefined and may vary by browser. Source: https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage
- W3C WAI keyboard accessibility guidance: functionality should be operable through a keyboard interface, and keyboard access should not trap the user. Source: https://www.w3.org/WAI/WCAG21/Understanding/keyboard.html
- Pong historical gameplay references: Pong is commonly described as two players controlling vertical paddles, scoring when the opponent misses, with the goal of reaching 11 points. Sources: https://en.wikipedia.org/wiki/Pong and https://atari.fandom.com/wiki/Atari_Pong

## 1. Player Configuration Options

### A. Two Human Players on the Same Keyboard

Inputs needed:

- Player 1 up.
- Player 1 down.
- Player 2 up.
- Player 2 down.
- Shared start/pause/restart controls if the game has menus or rounds.
- Optional confirm/select controls for menu navigation.

Complexity added:

- Must track simultaneous key states, not only individual key presses.
- Must avoid key conflicts where two players need nearby or overlapping keys.
- Must consider keyboard ghosting, where some physical keyboards fail to register certain multi-key combinations.
- Must prevent browser defaults from interfering with play, especially arrow-key page scrolling.
- Requires clear on-screen control labels or a control-selection screen.

Design implications:

- This is closest to classic local Pong.
- It assumes two people can share one keyboard comfortably.
- It makes no AI behavior necessary.
- It depends on the keyboard layout and physical keyboard quality more than mouse/touch controls would.

Priority-dependent areas:

- If local multiplayer is central, this mode carries the main social feel.
- If accessibility or compact laptops matter, cramped shared-keyboard play may be a usability issue.
- If the project targets classrooms or casual sharing, visible controls and quick restart matter more.

### B. One Human Player vs an AI Opponent

Inputs needed:

- Human player up.
- Human player down.
- Start/pause/restart controls.
- Optional difficulty selection.

Complexity added:

- Requires AI paddle behavior.
- Requires tuning so the AI is neither perfect nor useless.
- Requires deciding what information the AI can use: current ball position, predicted intercept point, reaction delay, speed cap, error margin, or a mix.
- Requires handling AI behavior after serve, after score, and when the ball moves away from the AI.
- May need difficulty scaling or separate easy/medium/hard behaviors.

Common AI behavior patterns:

- Tracking AI: opponent paddle moves toward the ball's current y-position.
- Predictive AI: opponent estimates where the ball will cross its side.
- Imperfect AI: opponent has limited paddle speed, reaction delay, random error, or deliberately poor positioning.
- State-based AI: opponent recenters when the ball is moving away and tracks/predicts only when threatened.

Design implications:

- Makes the game playable alone.
- Adds design burden because the AI's "feel" becomes part of the game quality.
- Can make difficulty progression easier to support.
- May reduce the pure two-player arcade feel unless local multiplayer remains available.

Priority-dependent areas:

- If single-player accessibility is important, AI matters.
- If the goal is the smallest local arcade game, AI is extra scope.
- If player satisfaction matters more than realism, imperfect/predictable AI may feel better than optimal AI.

### C. Both Options Selectable at Game Start

Inputs needed:

- Menu navigation.
- Mode selection.
- Human controls for two-player mode.
- Human controls plus AI settings for single-player mode.
- Start/back/restart controls.

Complexity added:

- Requires at least one pre-game state or menu.
- Requires game state management: title/menu, active play, paused, scored, game over, restart.
- Requires mode-specific setup and reset behavior.
- Requires communicating which controls apply in the selected mode.
- Requires testing both modes so shared systems behave consistently.

Design implications:

- Increases flexibility.
- Increases the minimum user interface and state-management burden.
- May make the project feel more complete, but it is not necessary for the smallest playable Pong.

Priority-dependent areas:

- If broad playability matters, selectable modes help.
- If v1.0 needs to stay very small, a mode menu is additional scope.
- If AI and two-player controls both exist, future requirements must decide which one is the default path.

## 2. Controls

### Conventional Keyboard Controls

Common two-player browser Pong mappings:

- Left player: `W` for up and `S` for down.
- Right player: `ArrowUp` for up and `ArrowDown` for down.
- Start/restart: often `Space`, `Enter`, or a visible button.
- Pause: often `P`, `Escape`, or a visible button.

Why these are common:

- `W`/`S` and arrow keys map naturally to vertical movement.
- They separate players onto opposite sides of the keyboard.
- They are familiar from many browser and PC games.

Known browser-control concerns:

- Arrow keys can scroll the page unless the game handles focus and default behavior carefully.
- Single-character shortcuts can conflict with assistive technology or browser/user shortcuts.
- Keyboard layout differences can affect character-based controls. `KeyboardEvent.key` reflects the user's layout; physical-position control may need `KeyboardEvent.code`, but that has its own accessibility and layout tradeoffs.

### Accessibility Considerations

Keyboard access:

- Game menus and controls should be operable by keyboard.
- Focus should be visible when interacting with menu buttons or settings.
- The user should not become trapped inside the game area with no way to tab or escape out.
- Pausing, restarting, or leaving the game should not require fast key timing.

Control remapping:

- Remappable controls help players who cannot comfortably use `W`/`S` and arrow keys.
- Remapping can also help with keyboard ghosting and non-US keyboard layouts.
- For a minimal version, remapping may be a larger feature, but it is an important design consideration.

Physical and cognitive accessibility:

- Avoid requiring rapid repeated tapping if holding a key can work.
- Provide a pause option.
- Use clear visual contrast between paddles, ball, scores, and background.
- Avoid relying on sound alone for score, bounce, or game-over feedback.
- Consider reduced-motion or slower-speed options if the game becomes visually intense.

Priority-dependent areas:

- If v1.0 targets casual local play, visible controls and avoiding page scroll may be enough for a baseline.
- If v1.0 has an accessibility goal, configurable controls, pause behavior, contrast, and focus handling should be considered earlier.
- If mobile/touch support enters scope, keyboard conventions no longer cover the full input design.

## 3. Ball Physics

### Minimum Behaviors Needed

Essential:

- Ball has horizontal and vertical velocity.
- Ball moves continuously each frame based on elapsed time or frame update.
- Ball bounces off the top and bottom boundaries.
- Ball bounces off paddles.
- A point is awarded when the ball passes beyond the left or right goal boundary.
- Ball resets after a point.
- Ball should not get stuck inside a paddle or wall after collision.
- Ball should not become perfectly vertical or perfectly horizontal in a way that makes rallies boring or unwinnable.

Strongly useful for satisfying play:

- Paddle hit position affects bounce angle. Hitting near the paddle center returns a shallower angle; hitting near the edge returns a steeper angle.
- Ball speed is capped so rallies do not become unreadable.
- Serve direction alternates or is randomized enough to avoid repetitive starts.

Optional:

- Ball acceleration after each paddle hit.
- Ball acceleration over time within a rally.
- Paddle movement affecting spin or bounce angle.
- Randomized serve angle.
- Dynamic paddle size.
- Advanced physics such as curved shots, spin, or non-rectangular collision.

### Speed

Essential role:

- The ball must move slowly enough for a new player to react, but fast enough that rallies have tension.
- A fixed speed can be playable for v1.0.

Optional enhancements:

- Increase speed after paddle hits.
- Increase speed after elapsed rally time.
- Reset speed after each point.
- Cap maximum speed to preserve readability.

Priority-dependent areas:

- If accessibility and beginner play matter, lower speed and a cap are more important.
- If arcade challenge matters, gradual speed increase becomes more valuable.

### Bounce Angle

Essential role:

- Some angle variation is important for a satisfying Pong feel.
- A simple fixed horizontal reflection is playable but can feel flat or repetitive.

Common approach:

- Use the ball's contact point relative to the paddle center to choose the outgoing vertical component.
- Edge hits produce sharper vertical angles; center hits produce flatter returns.

Optional enhancements:

- Add paddle velocity influence.
- Add tiny randomness to prevent endless repeat loops.
- Clamp minimum and maximum outgoing angles to avoid dead rallies.

Priority-dependent areas:

- If the project values predictable skill, bounce should be deterministic and readable.
- If the project values chaotic arcade feel, more variation can be added.

### Acceleration Over Time

Essential role:

- Not essential for a playable v1.0.
- Useful for increasing tension during long rallies.

Common patterns:

- Increase speed by a small percentage after each paddle hit.
- Increase speed after every N seconds of rally time.
- Increase speed after each score or round milestone.

Risks:

- If acceleration is too aggressive, rallies end because the game becomes unreadable rather than because of skill.
- If max speed is uncapped, collision detection and fairness can suffer.
- If speed increases but paddle speed does not, the game can become unwinnable.

Priority-dependent areas:

- If the game should be relaxing or accessible, acceleration may be reduced or optional.
- If the game should feel increasingly intense, acceleration is a useful lever.

## 4. Win Conditions

### First to N Points

Common pattern:

- Classic Pong is commonly described as first to 11 points.
- Browser remakes often use first to 5, 7, 10, or 11 depending on desired match length.

Requirements implied:

- Score display.
- Game-over state.
- Restart/new match action.
- Optional serve reset after each point.

Tradeoffs:

- Easy to understand.
- Works for local and AI modes.
- Match length depends on scoring target and player skill.

Priority-dependent areas:

- Short target scores fit quick demos.
- Higher target scores fit classic feel and longer matches.

### Timed Game

Common pattern:

- Highest score after a fixed duration wins.
- Tie can end as a draw or trigger overtime/sudden death.

Requirements implied:

- Match timer.
- Timer display.
- End-of-time handling.
- Tie handling.

Tradeoffs:

- Predictable session length.
- More UI and state complexity.
- Can feel less classic than first-to-score play.

Priority-dependent areas:

- Useful if the game is meant for short timed sessions.
- Less necessary if classic Pong rules are preferred.

### Sudden Death

Common patterns:

- First point after a tie wins.
- First point after time expires wins.
- First point after both players reach a threshold wins.

Requirements implied:

- Tie detection.
- Special state or label so players know sudden death is active.
- Clear game-over handling.

Tradeoffs:

- Adds drama.
- Adds state complexity.
- Can be frustrating if a single serve decides a long match too abruptly.

Priority-dependent areas:

- Useful if the game includes timed matches or tie rules.
- Not necessary for minimal classic Pong.

## 5. Minimum Viable Scope

### Smallest Genuinely Playable and Satisfying Version

The smallest playable Pong likely includes:

- One playfield.
- Two paddles.
- One ball.
- Continuous ball movement.
- Paddle movement controls.
- Ball collision with top/bottom boundaries.
- Ball collision with paddles.
- Scoring when the ball exits left or right.
- Visible score for both sides.
- Ball reset after a point.
- Match end when a score target is reached.
- Clear restart path after match end.
- At least minimal bounce-angle variation or tuned diagonal bounces.

Why these matter:

- Without scoring, the game is only a rally toy.
- Without reset, scoring breaks flow.
- Without match end, there is no complete play session.
- Without paddle-angle variation or careful bounce tuning, play can become repetitive.

### Common Additions Not Necessary for v1.0

Often added, but not required:

- Title screen.
- Mode selection.
- AI opponent.
- Multiple AI difficulty levels.
- High score table.
- Player names.
- Sound effects.
- Music.
- Visual effects or particles.
- Mobile/touch controls.
- Fullscreen mode.
- Pause menu.
- Settings menu.
- Control remapping.
- Theme selection.
- Power-ups.
- Obstacles.
- Local tournament/bracket mode.
- Online multiplayer.
- Persistent stats.
- Fancy animations.
- Asset-heavy art.

Priority-dependent areas:

- A satisfying v1.0 can still be small, but it needs a complete game loop: play, score, win, restart.
- If the project is a learning showcase, menus and polish may matter more.
- If the project is a design exercise, fewer features can make the core feel easier to tune.

## 6. Saving High Scores Without a Server

Short answer:

- Yes, high scores can be saved without a server by using browser-local storage such as `localStorage`.

What this provides:

- Stores small key/value data in the player's browser.
- Persists across browser sessions for the same origin.
- Requires no backend, database, login, or network request.
- Suitable for local best score, best rally length, fastest win, longest rally, or local match stats.

Important limitations:

- Scores are local to one browser and one origin.
- Scores are not shared across devices.
- Scores are not global or competitive.
- Users can clear them.
- Private/incognito browsing may delete them when the session ends.
- `file://` behavior is not guaranteed consistently across browsers.
- Local scores can be edited by the user, so they are not trustworthy for anti-cheat purposes.
- Storage operations are synchronous; this is fine for tiny high-score data but not for large datasets.

Alternatives without a server:

- `sessionStorage`: only for the current tab/session, not persistent enough for high scores.
- IndexedDB: better for larger structured data, likely overkill for simple Pong scores.
- Download/export file: possible, but awkward for casual play.
- URL/share code: possible for score sharing, but not a durable local leaderboard.

Priority-dependent areas:

- If "personal best on this device" is enough, local storage is viable.
- If "global leaderboard" or "cross-device profile" matters, a server or third-party backend becomes necessary.
- If the game is opened as a local file, high-score reliability depends on browser behavior and should be tested.

## 7. Increasing Difficulty Over Time

Difficulty levers:

- Ball speed.
- Ball bounce angle range.
- Paddle size.
- Paddle speed.
- AI reaction speed.
- AI prediction accuracy.
- AI error margin.
- Serve speed or serve angle.
- Win target or match duration.
- Visual distraction, though this can hurt accessibility.

Within a rally:

- Increase ball speed slightly after each paddle hit.
- Increase ball speed after every few seconds of continuous rally.
- Gradually widen possible bounce angles.
- Cap all increases so the game remains readable.

Across a match:

- Increase speed after each point.
- Increase speed when either player reaches score milestones.
- Reduce paddle size after score milestones.
- Increase AI speed or reduce AI error after score milestones.

In single-player AI mode:

- Start AI with a slower max paddle speed.
- Add reaction delay.
- Add prediction error.
- Reduce error or delay as the match progresses.
- Let the AI track only when the ball is moving toward it.

Risks:

- Difficulty can become unfair if the ball outruns paddle movement.
- Difficulty can become inaccessible if speed increases without an option to slow it down.
- Difficulty can feel arbitrary if changes are invisible or unexplained.
- In two-player mode, difficulty changes affect both players and may change fairness differently than in AI mode.

Priority-dependent areas:

- If the project wants classic local fairness, avoid asymmetrical difficulty changes in two-player mode.
- If the project wants single-player progression, AI tuning may be more important than ball speed.
- If the project wants accessibility, difficulty increase should be capped, optional, or paired with a slower mode.

## Cross-Cutting Open Design Questions

- Should v1.0 support one mode or multiple modes?
- Should the first playable version prioritize two-player classic Pong or solo play?
- Should controls be fixed, configurable, or fixed for v1.0 with remapping deferred?
- Should high scores mean local personal bests, match wins, longest rally, or something else?
- Should difficulty increase during every match, only in AI mode, or not at all for the first version?
- Should the match target follow classic 11-point Pong or use a shorter target for faster sessions?

## Research Boundary Notes

- No final game design choice is recommended here.
- No requirements are written here.
- No implementation code is included here.
