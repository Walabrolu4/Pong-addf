# Requirements Validation Report

Design Mode validation output for `docs/requirements.md`.

## Scope

Checked against:

- `docs/requirements.md`
- `research/technology-options.md`
- `research/game-design-research.md`
- `DECISIONS.md`

This report flags problems for human review. It does not rewrite requirements.

## Summary

Verdict: human review needed before sprint planning.

The requirements are mostly specific enough to guide a first build, and the file structure generally aligns with the Vanilla JavaScript plus HTML5 Canvas choice. The main problems are missing behavior for reset transitions, incomplete menu edge cases, a few vague gameplay terms, and local-storage testing risk for direct `file://` execution.

## Specific Issues

### VAL-001 - Ball visual shape is left open

**Category:** Vague or untestable gameplay requirement  
**Location:** `docs/requirements.md:56`

**Issue:** The ball may be "a white square or circle with a 10 pixel visual size." This leaves the final shape open and makes collision expectations unclear, especially because a 10 pixel circle could mean radius or diameter.

**Why it matters:** A developer needs to know whether collision math should treat the ball as a square, circle, or generic bounding box. Acceptance checks cannot verify a single expected visual shape.

**Human review needed:** Choose one ball shape and define whether 10 pixels means square side length or circle diameter.

### VAL-002 - Initial serve angle is underspecified

**Category:** Gap  
**Location:** `docs/requirements.md:60`

**Issue:** The first serve must choose a horizontal direction randomly, but the vertical direction or initial angle is not specified.

**Why it matters:** The ball must move with both horizontal and vertical velocity, but a developer must guess the starting vertical component. Different guesses could produce flat, repetitive, or too-steep serves.

**Human review needed:** Define the initial serve angle behavior, such as fixed diagonal angle, random angle range, or a small set of allowed serve angles.

### VAL-003 - Reset-to-serve transition is not defined

**Category:** Gap  
**Location:** `docs/requirements.md:58`, `docs/requirements.md:125`, `docs/requirements.md:138`

**Issue:** The ball returns to center after a point, life loss, or AI miss, and `Space` starts the serve from Ready to Serve. The requirements do not state whether Point Reset automatically moves to Ready to Serve, how long Point Reset lasts, or whether the player must press `Space` after every reset.

**Why it matters:** A developer must decide whether the next serve starts automatically or waits for input. This affects pacing, state handling, and acceptance testing.

**Human review needed:** Define the exact transition after each point, life loss, and AI miss.

### VAL-004 - 3 Lives reset behavior is incomplete

**Category:** Gap  
**Location:** `docs/requirements.md:58`, `docs/requirements.md:81`, `docs/requirements.md:114`

**Issue:** In 3 Lives mode, the ball resets after a life loss or AI miss, but the requirements do not say whether paddles also reset, whether the next serve direction changes, or whether the same Ready to Serve state is used.

**Why it matters:** First to 10 explicitly resets ball and paddles after a point, but 3 Lives only mentions ball reset. This creates different possible implementations.

**Human review needed:** Define paddle reset and next-serve behavior for both human misses and AI misses in 3 Lives mode.

### VAL-005 - Menu invalid-selection behavior is missing

**Category:** Gap  
**Location:** `docs/requirements.md:51`, `docs/requirements.md:52`, `docs/requirements.md:137`, `docs/requirements.md:242`

**Issue:** 3 Lives is valid only for Vs AI, and `Enter` confirms valid selections. The requirements do not define what happens when the player presses `4` while Two Players is selected, presses `Enter` before a valid selection exists, or switches from Vs AI plus 3 Lives back to Two Players.

**Why it matters:** A developer must invent invalid-selection behavior. Acceptance criteria only cover valid selection paths.

**Human review needed:** Define invalid input handling for menu selections.

### VAL-006 - Paddle bounce angle mapping is qualitative

**Category:** Vague or untestable gameplay requirement  
**Location:** `docs/requirements.md:68`

**Issue:** Center hits must produce a "shallow return" and edge hits a "steeper return," with a maximum outgoing angle of 60 degrees. The exact mapping from contact point to bounce angle is not specified.

**Why it matters:** The research says contact-position bounce can improve play feel, but the current wording leaves multiple valid implementations. Acceptance tests cannot check shallow versus steep without thresholds.

**Human review needed:** Define the minimum angle, center-hit angle, edge-hit angle, or formula.

### VAL-007 - AI playability requirement is not testable

**Category:** Vague or untestable gameplay requirement  
**Location:** `docs/requirements.md:95`, `docs/requirements.md:260`

**Issue:** The AI must be "beatable" and must return the ball during "normal play." These terms are subjective and do not define a measurable test.

**Why it matters:** A developer can implement many AI behaviors that appear to satisfy the text but feel very different. Manual acceptance may be inconsistent.

**Human review needed:** Define a testable AI baseline, such as max paddle speed only, tracking logic, no prediction, and expected behavior in fixed scenarios.

### VAL-008 - "Successful human paddle return" is undefined

**Category:** Gap  
**Location:** `docs/requirements.md:112`, `docs/requirements.md:269`

**Issue:** The 3 Lives score increases after each successful human paddle return, but the requirement does not define whether a return is counted on paddle collision, after the ball crosses a position, after the AI fails, or once per rally.

**Why it matters:** A collision that overlaps for more than one frame could accidentally count more than once unless the definition is precise. Different scoring definitions produce different high scores.

**Human review needed:** Define the exact scoring event for 3 Lives mode.

### VAL-009 - Local storage persistence may conflict with local-file execution

**Category:** Contradiction or testability risk  
**Location:** `docs/requirements.md:174`, `docs/requirements.md:182`, `docs/requirements.md:273`; `research/game-design-research.md` notes local `file://` caveats

**Issue:** Requirements say the game must work by opening `index.html` locally and that high scores persist after reload when local storage is available. Research notes that local `file://` storage behavior may vary by browser.

**Why it matters:** The acceptance criterion may pass in one browser and fail in another even if the implementation is correct.

**Human review needed:** Define supported desktop browsers for local-file testing or allow a fallback expectation when `localStorage` is unavailable or blocked.

### VAL-010 - Browser target is too broad

**Category:** Gap  
**Location:** `docs/requirements.md:174`

**Issue:** The requirement says "modern desktop browser" but does not list supported browsers or minimum versions.

**Why it matters:** Browser differences matter for local files, keyboard behavior, Canvas rendering, and local storage. Acceptance cannot clearly say which environments must pass.

**Human review needed:** Define supported browser targets for v1.0 validation.

### VAL-011 - Visual requirements include vague terms

**Category:** Vague or untestable visual requirement  
**Location:** `docs/requirements.md:161`, `docs/requirements.md:162`

**Issue:** The center divider must be "muted grey" and text must use "high contrast," but no color values or contrast threshold are specified.

**Why it matters:** A developer must choose visual values, and reviewers may disagree about whether the result is muted or high contrast.

**Human review needed:** Define color values or a minimum contrast rule.

### VAL-012 - High-score storage key is not specified

**Category:** Gap  
**Location:** `docs/requirements.md:183`

**Issue:** The local high-score storage key must be documented in the implementation, but the requirements do not specify the key.

**Why it matters:** The developer can choose a key, but acceptance cannot verify a known storage contract. A future implementation could accidentally change the key and reset user scores.

**Human review needed:** Decide whether the key belongs in requirements or may remain implementation-defined.

### VAL-013 - File structure mostly aligns, but runtime package wording is ambiguous

**Category:** File structure alignment  
**Location:** `docs/requirements.md:218`

**Issue:** The file structure aligns with Vanilla JavaScript and local static files: `index.html`, `styles.css`, and `game.js` are appropriate. However, the requirement says "The v1.0 game must consist of these files" and includes `docs/requirements.md`.

**Why it matters:** It is unclear whether `docs/requirements.md` is part of the runtime deliverable or only project documentation. A developer planning the game package may interpret this differently.

**Human review needed:** Clarify whether the runtime game consists only of `index.html`, `styles.css`, and `game.js`, with `docs/requirements.md` as project documentation.

### VAL-014 - `index.html` loading responsibilities are implicit

**Category:** Gap  
**Location:** `docs/requirements.md:219`, `docs/requirements.md:220`, `docs/requirements.md:221`

**Issue:** The file structure names `styles.css` and `game.js`, but does not explicitly require `index.html` to load both files using relative paths and classic script loading.

**Why it matters:** The technical requirements prohibit modules and build tools, so the loading relationship is important for local-file execution.

**Human review needed:** Decide whether to explicitly require `index.html` to link `styles.css` and load `game.js` with a non-module script tag.

## Contradiction Check

No direct internal contradiction was found between the selected technology stack and the file structure. The main risk is the combination of local `file://` execution and high-score persistence, because research notes browser-local storage caveats for local files.

## Feature Coverage Check

Features in v1.0 scope generally have matching requirement sections:

- Selectable player configuration: covered, but invalid menu behavior is missing.
- Two Players mode: covered.
- Vs AI mode: covered, but AI testability is weak.
- First to 10 mode: covered.
- 3 Lives high-score mode: covered, but reset and scoring event details are incomplete.
- Local high-score persistence: covered, but browser support and storage-key details are incomplete.
- Multi-file local Vanilla JavaScript structure: covered, with minor package/loading ambiguity.
