# QUESTIONS.md - PongTest

Record unknowns that matter to project direction, sprint scope, safety, or implementation correctness. Keep open questions visible until they are answered or converted into requirements or decisions.

## Open Questions

These questions come from the current requirements validation work and should be reviewed before Sprint 001 implementation planning.

### Q001 - Ball Shape

**Status:** Open  
**Blocking:** Collision implementation and visual acceptance.  
**Raised:** 2026-06-06  
**Source:** `research/requirements-validation.md`, `docs/requirements.md`

**Question:** Should the v1.0 ball be a 10 pixel square, or a circle with a 10 pixel diameter?

**Notes:** `docs/requirements.md` currently allows either "white square or circle," which leaves collision assumptions open.

### Q002 - Initial Serve Angle

**Status:** Open  
**Blocking:** Ball movement tuning.  
**Raised:** 2026-06-06  
**Source:** `research/requirements-validation.md`, `docs/requirements.md`

**Question:** What vertical component or angle range should the first serve use?

**Notes:** Requirements specify random horizontal direction and both horizontal and vertical velocity, but not the initial angle.

### Q003 - Reset-to-Serve Transition

**Status:** Open  
**Blocking:** Game state implementation.  
**Raised:** 2026-06-06  
**Source:** `research/requirements-validation.md`, `docs/requirements.md`

**Question:** After a point, life loss, or AI miss, should the game wait for `Space` before the next serve?

**Notes:** Requirements define Point Reset and Ready to Serve but do not define the transition timing.

### Q004 - 3 Lives Reset Details

**Status:** Open  
**Blocking:** 3 Lives mode implementation.  
**Raised:** 2026-06-06  
**Source:** `research/requirements-validation.md`, `docs/requirements.md`

**Question:** In 3 Lives mode, do paddles reset after human misses and AI misses, or does only the ball reset?

**Notes:** First to 10 explicitly resets ball and paddles after points. 3 Lives only explicitly resets the ball.

### Q005 - Invalid Menu Inputs

**Status:** Open  
**Blocking:** Menu implementation and acceptance checks.  
**Raised:** 2026-06-06  
**Source:** `research/requirements-validation.md`, `docs/requirements.md`

**Question:** What should happen if the player presses `4` while Two Players is selected, presses `Enter` before valid choices exist, or changes from Vs AI 3 Lives to Two Players?

**Notes:** Requirements define valid paths but not invalid input behavior.

### Q006 - Paddle Bounce Formula

**Status:** Open  
**Blocking:** Ball physics implementation.  
**Raised:** 2026-06-06  
**Source:** `research/requirements-validation.md`, `docs/requirements.md`

**Question:** What exact formula or angle values should map paddle contact position to ball bounce angle?

**Notes:** Requirements say center hits are shallow and edge hits are steeper, with a 60 degree maximum.

### Q007 - AI Acceptance Baseline

**Status:** Open  
**Blocking:** AI implementation and testing.  
**Raised:** 2026-06-06  
**Source:** `research/requirements-validation.md`, `docs/requirements.md`

**Question:** What measurable test proves the basic AI is playable and beatable?

**Notes:** Current terms such as "beatable" and "normal play" are subjective.

### Q008 - 3 Lives Scoring Event

**Status:** Open  
**Blocking:** High-score mode scoring.  
**Raised:** 2026-06-06  
**Source:** `research/requirements-validation.md`, `docs/requirements.md`

**Question:** Should a successful human paddle return be counted at paddle collision, after the ball leaves the paddle, after the ball crosses midline, or by another event?

**Notes:** This must be precise so a collision does not count more than once.

### Q009 - Supported Browsers

**Status:** Open  
**Blocking:** Acceptance testing.  
**Raised:** 2026-06-06  
**Source:** `research/requirements-validation.md`, `docs/requirements.md`

**Question:** Which desktop browsers must v1.0 support when opened as a local file?

**Notes:** Requirements say "modern desktop browser," but local storage and file loading can vary across browsers.

### Q010 - Visual Color Values

**Status:** Open  
**Blocking:** Visual implementation and acceptance.  
**Raised:** 2026-06-06  
**Source:** `research/requirements-validation.md`, `docs/requirements.md`

**Question:** What exact colors or contrast rule should define the black background, white elements, muted grey divider, and high-contrast text?

**Notes:** Current visual terms are understandable but not fully testable.

## Resolved Questions

### R001 - Technology Stack

**Answer:** Vanilla JavaScript with the HTML5 Canvas API.  
**Recorded in:** `DECISIONS.md`

### R002 - Player Configuration

**Answer:** Support both Two Players and Vs AI at game start.  
**Recorded in:** `DECISIONS.md`

### R003 - Win Modes

**Answer:** Support First to 10 and 3 Lives high-score mode for v1.0.  
**Recorded in:** `DECISIONS.md`

### R004 - Deployment Approach

**Answer:** Local static files opened directly in the browser.  
**Recorded in:** `DECISIONS.md`

### R005 - File Structure

**Answer:** Use `index.html`, `styles.css`, `game.js`, and `docs/requirements.md`.  
**Recorded in:** `DECISIONS.md`
