# RISKS.md - PongTest

Record risks that could affect project correctness, safety, scope, or continuity.

## Risk 001 - Collision Detection Bugs

**Risk:** Ball/paddle collision can miss at high speed, double-count a hit, or leave the ball stuck in a paddle or wall.  
**Severity:** High  
**Probability:** Medium  
**Status:** Open  
**Mitigation:** Keep ball speed capped, use elapsed-time movement carefully, resolve overlaps after collision, and test top wall, bottom wall, left paddle, right paddle, and corner cases.

## Risk 002 - Game Loop Timing Differences

**Risk:** Gameplay speed may vary across displays if movement is tied to frame count instead of elapsed time.  
**Severity:** High  
**Probability:** Medium  
**Status:** Open  
**Mitigation:** Use `requestAnimationFrame()` timestamps and delta time for ball and paddle movement, as required by `docs/requirements.md`.

## Risk 003 - Local File Browser Differences

**Risk:** Opening `index.html` with `file://` may behave differently across browsers, especially for local storage and script loading.  
**Severity:** Medium  
**Probability:** Medium  
**Status:** Open  
**Mitigation:** Use classic non-module script loading, relative file paths, no fetch-based loading, and validate in the supported browser list once selected.

## Risk 004 - Local High Score Persistence

**Risk:** Browser-local storage may be unavailable, blocked, cleared, or inconsistent for local files.  
**Severity:** Medium  
**Probability:** Medium  
**Status:** Open  
**Mitigation:** Treat missing or cleared storage as high score 0, avoid global leaderboard claims, and define supported browser expectations before acceptance.

## Risk 005 - Keyboard Input and Page Scrolling

**Risk:** Arrow keys or `Space` may scroll the page or conflict with browser behavior instead of controlling the game.  
**Severity:** Medium  
**Probability:** Medium  
**Status:** Open  
**Mitigation:** Capture gameplay keys while the game is focused and verify that page scroll does not occur during acceptance testing.

## Risk 006 - Keyboard Ghosting

**Risk:** Some keyboards may not register multiple simultaneous keys for two-player local play.  
**Severity:** Medium  
**Probability:** Medium  
**Status:** Open  
**Mitigation:** Use conventional separated controls (`W`/`S` and arrows), document the limitation, and consider remappable controls only in a later release.

## Risk 007 - AI Tuning Feels Unfair

**Risk:** Basic AI may feel too weak, too perfect, or inconsistent because "playable" and "beatable" are not yet fully measurable.  
**Severity:** Medium  
**Probability:** Medium  
**Status:** Open  
**Mitigation:** Keep AI simple, use a lower paddle speed than the human, and resolve the AI acceptance baseline question before implementation.

## Risk 008 - Scope Creep

**Risk:** Non-goal features such as sound, mobile controls, pause, settings, online play, or global leaderboards may slip into v1.0.  
**Severity:** High  
**Probability:** Medium  
**Status:** Open  
**Mitigation:** Treat `docs/requirements.md` non-goals as binding. Add new features only through Design Mode decisions and updated sprint scope.

## Risk 009 - Requirements Ambiguity

**Risk:** Open validation questions could cause developers to invent behavior during Develop Mode.  
**Severity:** High  
**Probability:** Medium  
**Status:** Open  
**Mitigation:** Resolve `QUESTIONS.md` open items or explicitly accept them as implementation-defined before Sprint 001 dry run approval.

## Risk 010 - Project Memory Drift

**Risk:** `docs/requirements.md`, `DECISIONS.md`, `QUESTIONS.md`, sprint packs, and implementation may diverge.  
**Severity:** Medium  
**Probability:** Medium  
**Status:** Open  
**Mitigation:** Load project brain files at session start, run a consistency audit before Develop Mode, and update `STATE.md` after durable changes.

## Risk 011 - Secret Exposure

**Risk:** Credentials or local secrets could be loaded into an AI session or committed accidentally.  
**Severity:** High  
**Probability:** Low  
**Status:** Open  
**Mitigation:** Follow `SECURITY.md`. Do not load `.env`, keys, credentials, secrets, or other protected files.
