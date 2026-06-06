# Learning ADDF by Building a Browser Pong Game
### A Teacher's Guide

**Tutorial version:** 1.0  
**Project:** Browser-based Pong game  
**Format:** Teacher-led workshop with student exercises  
**Teaching goal:** Run the full ADDF lifecycle on a real code project — from research through working software  
**Primary principle:** The files are the project.  

---

## How to Use This Guide

This is a teacher-facing document.

Each section contains:

- **Teacher context** — what to explain before students act
- **Student steps** — exact actions with copy-paste prompts
- **Expected output** — what good looks like so you can spot problems
- **Exercise** — a task students complete independently
- **Checkpoint** — a gate students must pass before moving on

This tutorial is designed to be used after students have read the ADDF framework documentation — specifically `getting-started.md` and the modes documentation (`docs/modes/`). It covers the full 8-step ADDF lifecycle from the beginning — students generate their own requirements document, make real technology decisions, and build working software.

**How this tutorial maps to the ADDF 8-step lifecycle:**

| Tutorial phase | ADDF Lifecycle step |
|---|---|
| Phase 0-A: Research | Step 1 — Research |
| Phase 0-B: Design & Requirements | Steps 2–3 — Design & Feasibility, Validation Gate |
| Sprint 001: Project Brain | Step 4 — Architecture |
| Sprint 002–003: Build | Steps 5–6 — Sprint Planning, Build & Test |
| Sprint close + reflection | Steps 7–8 — Review & Reflection, Deploy/Maintain/Resume |

---

## Why Pong

Pong is small enough to build in a few sessions but complex enough to require real decisions:

- What technology stack should we use?
- One player or two?
- What are the win conditions?
- How do collisions work?
- Where does the game run and how is it deployed?

These are genuine questions with multiple defensible answers. Different students may research them and arrive at different conclusions. ADDF handles this — the decisions go into `DECISIONS.md`, the reasoning is preserved, and the project can be resumed by anyone who reads the files.

Pong also has a concrete verification step that most documentation projects lack: **you open the browser and play the game.** The output is immediately checkable.

---

## What Students Learn

By the end of this tutorial, students will be able to:

- Run Research Mode on a real open question with no pre-determined answer
- Generate a requirements document from scratch using Design Mode
- Make and record technology decisions before writing any code
- Direct an AI in Develop Mode to write working code
- Review a code dry run without being the author of the code
- Verify implementation by testing the actual software
- Keep a code project resumable from files alone

---

## What is Different About a Code Project

The ADDF documentation examples involve mostly Markdown files. Pong involves real code. This changes two things:

**Develop Mode matters more.** Every file the AI writes is a code file. Code that is wrong does not just look wrong — the game breaks. The dry run is not a formality. It is the only point where the human can catch an architectural mistake before it is committed.

**Verification is physical.** When Sprint 002 is complete, students open `index.html` in a browser. The ball either moves or it does not. This is one of the clearest demonstrations of what ADDF acceptance criteria are for.

---

## Prerequisites

Students should have:

- Read the ADDF framework documentation: `getting-started.md`, `docs/modes/index.md`, and `docs/sprint-loop.md`
- A text editor
- A web browser
- Access to an AI tool (Claude, ChatGPT, Gemini, or similar)
- Basic familiarity with HTML, CSS, and JavaScript (enough to read it — not enough to write it from scratch)
- Git for version control

---

## The Project

```txt
Project: Pong Game
Scale: Project → Release → Sprint
Target: A two-player Pong game that runs in a web browser with no installation required.
v1.0 goal: Playable game with two paddles, a bouncing ball, score tracking, and a win condition.
```

The exact technology stack is not defined here. That is the output of the research phase. Students will research the options and make the decision themselves.

---

## Contents

1. [Quick Reference — The ADDF Roles](#1-quick-reference--the-addf-roles)
2. [Phase 0 — Research](#2-phase-0--research)
3. [Phase 0 — Design and Requirements](#3-phase-0--design-and-requirements)
4. [Sprint 001 — Project Brain](#4-sprint-001--project-brain)
5. [Sprint 002 — Core Game Mechanics](#5-sprint-002--core-game-mechanics)
6. [Sprint 003 — Scoring and Game States](#6-sprint-003--scoring-and-game-states)
7. [The Path to v1.0](#7-the-path-to-v10)
8. [Appendix A — Seed File Templates](#8-appendix-a--seed-file-templates)
9. [Appendix B — Standard Prompts Reference](#9-appendix-b--standard-prompts-reference)
10. [Appendix C — Review Checklists](#10-appendix-c--review-checklists)

---

# 1. Quick Reference — The ADDF Roles

**Teacher context:**

Students who have completed the main tutorial know this. Use this as a 2-minute reminder before starting. For students who are new, spend 10 minutes here.

```txt
HUMAN OPERATOR                    AI MODEL
─────────────────                 ──────────────────
Seeds the project                 Reads the files
Declares the mode                 Operates within that mode
Reviews the output                Produces output
Approves or rejects               Stops and waits
Records decisions                 Does not decide
Commits the work                  Does not commit
```

```txt
Research Mode   — investigate, compare, summarize. No decisions. No files modified.
Design Mode     — write Markdown project memory. No implementation files.
Develop Mode    — write implementation files only after dry run approval.
```

The lifecycle for this project:

```txt
Phase 0-A: Research → understand the options
Phase 0-B: Design → write requirements, make decisions, plan architecture
Sprint 001: Design → create the project brain
Sprint 002: Develop → build core mechanics (with dry run)
Sprint 003: Develop → add scoring and game states (with dry run)
```

---

# 2. Phase 0 — Research

## Lesson Objectives

By the end of Phase 0-Research, students can:

- Write a Research Mode prompt that investigates a real technical question
- Evaluate AI research output for completeness and bias
- Identify when research is done and design can begin

## Teacher Context

This is the first time in ADDF that students have a genuinely open question to research. The main tutorial handed them a pre-made requirements document. Here, nothing is decided. Students must figure out what kind of Pong game they are building and what technology they will use.

There is no single correct answer. A student who chooses Vanilla JavaScript + Canvas and a student who chooses Phaser.js are both making defensible choices. ADDF does not dictate the answer — it dictates the process for making and recording the decision.

Two research areas must be investigated before requirements can be written:

```txt
1. Technology stack — what tools will power the game?
2. Game design decisions — what exactly are we building?
```

---

## Step 1 — Technology Stack Research

**Teacher context:**

Walk students through the options briefly before they run the research prompt. The goal is not to tell them the answer — it is to make sure they know enough to evaluate the AI's research output intelligently.

Brief overview to give students:

```txt
Vanilla JS + Canvas API
   Pros: No dependencies, runs anywhere, fast, small file size
   Cons: More code to write manually

Phaser.js
   Pros: Built-in game loop, physics, input handling, lots of examples
   Cons: Larger download, more to learn, may be overkill for Pong

p5.js
   Pros: Beginner-friendly creative coding library, great for simple games
   Cons: Not a game engine, less structured for projects with multiple files

Three.js / WebGL
   Pros: Powerful 3D rendering
   Cons: Entirely overkill for Pong — do not choose this
```

**Files to create first (manually — this is the seed for research):**

Create a folder for the project and one seed file:

```bash
mkdir pong-game
cd pong-game
git init
```

Create `STATE.md`:

```md
# STATE.md

## Project

Pong Game — Browser-based two-player game

## Current Goal

Research technology options and game design decisions before writing requirements.

## Active Lifecycle Stage

Research

## Current Status

Research phase beginning. No requirements written. No technology decided.

## Next Step

Complete technology stack research and game design research,
then move to Design Mode to write requirements.
```

Create `SECURITY.md`:

```md
# SECURITY.md

## Files That Must Never Be Loaded Into AI Tools

- Any file containing API keys or credentials
- Any .env file

## Repository Rules

- Do not commit secrets or tokens.
- This is a client-side game with no backend — secrets are unlikely but still possible.
```

Commit the seeds:

```bash
git add .
git commit -m "Initialize project with seed files"
```

**Teacher note — PROMPTS.md:**

The starter kit already contains a `PROMPTS.md` file with ready-to-use prompts for every major ADDF operation (Research Mode, Design Mode, sprint pack generation, dry run, authorization, consistency audit, sprint close, and handoff). Point students to it now.

> "Your starter kit includes `PROMPTS.md` — keep it open throughout the project. Appendix B in this tutorial contains versions adapted for Pong. `PROMPTS.md` is your general-purpose reference for any future ADDF project."

**Student action — paste this research prompt:**

```txt
You are operating in Research Mode.

I am building a browser-based Pong game using the Autonomous Duck Deployment 
Framework. Before I write requirements, I need to understand my technology options.

Investigate the following:

1. Technology stack options for a browser Pong game
   Compare these options:
   a. Vanilla JavaScript with the HTML5 Canvas API
   b. Phaser.js (game framework)
   c. p5.js (creative coding library)

   For each option, return:
   - What it provides out of the box for a Pong game
   - Dependencies required (file size, CDN availability)
   - Complexity for a developer with basic JavaScript knowledge
   - Suitability for a small, self-contained browser game
   - Whether it requires a build step or runs as a plain HTML file

2. Deployment options for a browser game
   Compare:
   a. A single self-contained HTML file (no server needed)
   b. Multiple files (HTML, CSS, JS) opened locally
   c. Hosted on GitHub Pages
   d. Hosted on a simple static file host (Netlify, Vercel)

   For each, return: requirements, tradeoffs, and what it means for development workflow.

Rules:
- Do not recommend a final choice.
- Do not write any game code.
- Do not write requirements.
- Flag any areas where the answer depends on project priorities.
- Return structured findings organized by question.

Save output to: research/technology-options.md
```

**Expected output:**

A structured research document in `research/technology-options.md`. It should compare options with real tradeoffs, not just list features. Signs of good output:

```txt
Canvas API section explains the game loop concept and why it matters for Pong
Phaser.js section mentions bundle size and whether a CDN link is available
p5.js section is honest that it is not a game engine
Deployment section explains what "no server" means for a local HTML file workflow
```

Signs of bad output:

```txt
The model recommends a choice (Research Mode does not decide)
The comparisons are generic and not specific to a Pong game
Deployment section omits the "single HTML file" option
Code snippets appear in the research output
```

If the output recommends a choice, send it back:

```txt
You are still in Research Mode. You made a recommendation in your output.
Research Mode does not make final decisions — that belongs to Design Mode.
Remove the recommendation and present the tradeoffs neutrally.
```

---

## Step 2 — Game Design Research

**Teacher context:**

The technology question is only half the research. The game design question is equally important. "Pong" is not a single specification — there are meaningful decisions about rules, controls, and scope.

**Student action — paste this research prompt:**

```txt
You are operating in Research Mode.

I am building a browser-based Pong game. Before writing requirements, 
I need to understand the design decisions involved.

Investigate the following:

1. Player configuration options
   a. Two human players on the same keyboard
   b. One human player vs an AI opponent
   c. Both options selectable at game start

   For each: what inputs are needed, what complexity is added?

2. Controls
   What keyboard controls are conventional for a two-player browser Pong game?
   What are the accessibility considerations?

3. Ball physics
   What are the minimum physics behaviours needed for a playable Pong game?
   (Speed, angle after bounce, acceleration over time — what is essential vs optional?)

4. Win conditions
   What are common win conditions in Pong?
   (First to N points, timed game, sudden death?)

5. Minimum viable scope
   What is the smallest version of Pong that is genuinely playable and satisfying?
   What features are commonly added that are not necessary for v1.0?

Rules:
- Do not write requirements.
- Do not write code.
- Do not recommend final choices.
- Return structured findings.

Save output to: research/game-design-research.md
```

**Expected output:**

`research/game-design-research.md` covering all five areas. It should help students make informed decisions, not make the decisions for them.

---

## Phase 0-A Exercise

> Read `research/technology-options.md` and `research/game-design-research.md`.
>
> Without consulting the AI, write down:
> 1. Which technology stack you will choose and your one-sentence reason
> 2. Whether the game will be one player vs AI or two players on the same keyboard
> 3. The win condition you will use
> 4. One thing the research left unclear that you would want to investigate further
>
> You will use these decisions in Phase 0-B to write the requirements document.

This exercise forces students to engage with the research output rather than hand it back to the AI. The decisions they make here drive the entire rest of the project.

---

## Phase 0-A Checkpoint

```txt
- [ ] research/technology-options.md exists with real comparisons
- [ ] research/game-design-research.md exists with game design analysis
- [ ] Research output does not contain recommendations (Research Mode does not decide)
- [ ] Research output does not contain code
- [ ] Student has made their three personal decisions (tech, players, win condition)
- [ ] STATE.md is still accurate (research stage, no requirements yet)
```

**Common mistakes:**

```txt
The AI wrote code in Research Mode.
→ Research Mode does not write implementation. Send it back.

The student accepted the first research output without reading it.
→ Ask them to find one specific tradeoff from each comparison.
   If they cannot, they did not read it.

The student cannot make the three decisions in the exercise.
→ This is fine — have them pick the simplest option in each case.
   Vanilla JS + Canvas, two players, first to 7. Move forward.
   Indecision is not a reason to stay in research forever.
```

---

# 3. Phase 0 — Design and Requirements

## Lesson Objectives

By the end of Phase 0-Design, students can:

- Generate a requirements document from scratch using Design Mode
- Record technology decisions with context and reasoning in `DECISIONS.md`
- Validate requirements are complete enough to sprint against

## Teacher Context

Research is done. Students have their three decisions. Now Design Mode takes those decisions and the research findings and produces two things:

```txt
1. A requirements document for the Pong game
2. A decisions record for the choices made
```

These two artifacts are what Sprint 001 will use to set up the project brain. Without them, the AI in Sprint 001 has nothing to work from.

---

## Step 1 — Generate the Requirements Document

**Files to load into the AI:**

```txt
STATE.md
research/technology-options.md
research/game-design-research.md
```

**Student action — fill in their decisions, then paste this prompt:**

```txt
You are operating in Design Mode.

I have completed the research phase. Here are my decisions:

Technology stack: [student fills in their choice]
Player configuration: [student fills in: two players OR one player vs AI]
Win condition: [student fills in: e.g., first to 7 points]

Using the research documents provided and these decisions, produce a 
requirements document for the Pong game.

Save output to: docs/requirements.md

The requirements document must cover:

1. Project overview — what this game is and what it runs on
2. Technology decision — what was chosen and why (reference research findings)
3. Gameplay requirements
   - Ball behaviour (starting position, speed, direction, bounce rules)
   - Paddle behaviour (size, speed, movement constraints)
   - Scoring rules
   - Win condition
   - Game states (not started, playing, paused if applicable, game over)
4. Input requirements — exact keyboard keys for each player and action
5. Visual requirements — what the player sees (canvas size, colours, score display)
6. Technical requirements
   - Must run in a browser without installation
   - Must work as a local file (no server required for v1.0)
   - No external dependencies that require a build step (unless student chose Phaser/p5)
7. Non-goals for v1.0 — what is explicitly excluded
   (e.g., sound, mobile controls, online multiplayer, AI opponent if not chosen)
8. File structure — what files the game will consist of
9. v1.0 acceptance criteria — how we know the game is done

Rules:
- Write specific, testable requirements.
- Do not write code.
- Do not invent features not discussed in research or decided above.
- Non-goals must be explicit — anything not listed as in-scope is deferred.
```

**Expected output:**

`docs/requirements.md` — a specific, testable requirements document for this student's Pong game. Key things to check:

```txt
Gameplay requirements are specific — not "the ball bounces" but
"the ball reverses its horizontal direction when it contacts a paddle"

Win condition matches what the student decided

File structure is listed (e.g., index.html, game.js, style.css — or
index.html alone if using a single-file approach)

Non-goals are explicit — the requirements doc should list at least 3 things
that are NOT being built in v1.0

Acceptance criteria are things a human can verify by playing the game
```

**Signs of bad output:**

```txt
Requirements are vague ("the game should feel good to play")
→ Ask for specific, measurable requirements.

The AI added features the student did not choose (sound effects, AI opponent)
→ This is scope creep. Remove them. Add to non-goals.

Acceptance criteria include things like "the code is clean"
→ Acceptance criteria must be verifiable by playing the game, not reading the code.
```

---

## Step 2 — Record the Decisions

**Student action — paste this prompt:**

```txt
You are operating in Design Mode.

Based on the requirements document and research findings, record the 
technology and design decisions for this project.

Save output to: DECISIONS.md

Format each decision as:

## Decision [number]: [short title]

**Status:** Accepted
**Type:** [Technology / Design / Architecture]

### Context
[Why this decision needed to be made]

### Options Considered
[The alternatives from the research]

### Decision
[What was chosen]

### Reasoning
[Why this option was chosen over the alternatives]

### Consequences
[What this means for the project — trade-offs accepted]

---

Record decisions for:
1. Technology stack choice
2. Player configuration (two players vs AI)
3. Win condition
4. Deployment approach for v1.0
5. Single-file vs multi-file structure

Use the research documents and requirements document as source material.
Do not invent reasoning that was not part of the research.
```

**Expected output:**

`DECISIONS.md` with 5 decisions, each with real context and reasoning. The reasoning must trace back to the research documents — not generic statements like "this is simpler."

---

## Step 3 — Validate the Requirements

**Teacher context:**

Before sprinting, students validate that the requirements are complete enough. This is the Validation Gate step from the ADDF 8-step lifecycle — Design Mode reads the requirements and produces a validation report.

**Student action — paste this prompt:**

```txt
You are operating in Design Mode.

Read docs/requirements.md.

Produce a validation report saved to: research/requirements-validation.md

Check for:
1. Any gameplay requirement that is vague or untestable
2. Any gap — something a developer would need to know that is not specified
   (e.g., what happens when the ball reaches the top or bottom edge?)
3. Any contradiction
4. Any feature mentioned in scope that does not have a requirement written for it
5. Whether the file structure in the requirements aligns with the technology choice

Return specific issues, not general feedback.
Do not rewrite the requirements. Flag the problems for human review.
```

Students read the validation report and correct any issues in `docs/requirements.md` before moving forward. They can either edit the file directly or ask Design Mode to make specific corrections.

---

## Phase 0-B Checkpoint

```txt
- [ ] docs/requirements.md exists with specific, testable requirements
- [ ] DECISIONS.md exists with at least 5 decisions and real reasoning
- [ ] research/requirements-validation.md exists
- [ ] Any issues from validation are resolved in the requirements document
- [ ] Requirements are specific enough that a developer could build from them
     without asking any clarifying questions
- [ ] Non-goals section is present
- [ ] Acceptance criteria are playtest-verifiable
```

**Common mistakes:**

```txt
DECISIONS.md says "we chose Canvas because it is simple" with no further reasoning.
→ The reasoning must reference the research. What specifically made it more suitable?

Requirements say "the ball should bounce realistically."
→ This is not testable. What does "realistic" mean? 
   Ask for a specific rule: angle in equals angle out? Speed increase on hit?

The student skipped validation.
→ Have them run the validation prompt and fix at least one issue before continuing.
   The validation step exists because humans miss things on first read.
```

---

# 4. Sprint 001 — Project Brain

## Lesson Objectives

By the end of Sprint 001, students can:

- Use the requirements and decisions documents as input to Design Mode
- Generate a complete project brain for a code project
- Understand how brain files differ for a code project vs a documentation project

## Teacher Context

Sprint 001 for the Pong game follows the standard ADDF Architecture step — Design Mode generates the project brain files. The difference from generic examples is the content.

Where the ADDF repo brain said things like "do not build the website before v0.1 is stable," the Pong brain says things like "do not add sound before core mechanics are verified." The structure is the same. The project-specific rules are different.

This sprint also introduces `COMMANDS.md` in a more meaningful way than the ADDF repo tutorial. Pong has real commands:

```txt
How to open the game in the browser
How to run any tests (if applicable)
```

---

## Step 1 — Generate the Project Brain

**Files to load into the AI:**

```txt
STATE.md (seed)
SECURITY.md (seed)
docs/requirements.md
DECISIONS.md
research/technology-options.md
research/game-design-research.md
```

**Student action — paste this prompt:**

```txt
You are operating in Design Mode.

I am building a browser Pong game using the Autonomous Duck Deployment Framework.

The research and requirements phases are complete. Generate the project brain 
files for this repository.

Produce these files with complete, project-specific content:

- AGENTS.md
- DOMAIN.md
- COMMANDS.md
- QUESTIONS.md
- RISKS.md
- STYLE_GUIDE.md
- GIT_STRATEGY.md
- START_HERE.md
- PROMPT_CHANGELOG.md

Note: `PROMPTS.md` already exists in the starter kit — do not regenerate it. `STATE.md`, `SECURITY.md`, and `DECISIONS.md` were created in earlier phases — update them rather than overwriting.

Reference docs/requirements.md and DECISIONS.md for all project-specific content.

Rules for each file:

AGENTS.md must:
- Define Research Mode, Design Mode, Develop Mode by correct name
- State the dry run approval rule for Develop Mode
- Include rules specific to this project
  (e.g., do not add features outside v1.0 scope, do not modify game logic without a dry run)

DOMAIN.md must:
- Describe the game accurately
- State what is in scope for v1.0 (from requirements)
- State what is out of scope (from the non-goals section)

COMMANDS.md must:
- Explain how to open the game in a browser
- Include any test or build commands relevant to the technology chosen

RISKS.md must:
- Include risks specific to a Pong game built with this technology stack
  (e.g., browser compatibility, collision detection bugs, game loop timing)

START_HERE.md must:
- Tell a new developer how to open and run the game immediately
- Tell a new developer where to find the requirements and sprint files

Do not write game code.
Do not write the HTML, CSS, or JavaScript files yet.
```

**Expected output:**

Ten project brain files. The key difference from the ADDF repo tutorial is that these should be obviously about a game project — `DOMAIN.md` should describe Pong, `RISKS.md` should mention browser timing and collision bugs, `COMMANDS.md` should say "open index.html in a browser."

---

## Step 2 — Generate the Planning Structure and Sprint 001 Pack

**Student action — paste this prompt:**

```txt
You are operating in Design Mode.

Generate the planning structure and Sprint 001 sprint pack for the Pong game.

Produce:
- planning/backlog.md
- planning/releases/v1.0/release_plan.md
- planning/releases/v1.0/scope.md
- planning/sprints/sprint_001/requirements.md
- planning/sprints/sprint_001/blueprint.md
- planning/sprints/sprint_001/acceptance.md

**Teacher note:** The starter kit contains a placeholder `planning/releases/v0.1/` folder. Before running this prompt, have students rename it to `v1.0/` (the Pong game's first release target) or simply delete the placeholder files — the AI will generate the correct content.

Sprint 001 goal: Add the ADDF project brain and planning structure.

The backlog.md must list the sprint order for reaching v0.1:
- Sprint 001: Project brain
- Sprint 002: Core game mechanics (ball, paddles, physics)
- Sprint 003: Scoring and game states
- Any additional sprints required for v1.0 based on the requirements document

Blueprint must list every file this sprint creates.
Acceptance criteria must be checkable by a human.
```

---

## Step 2b — Fill in blueprint_feedback.md

After reviewing the generated brain files in Step 2, fill in the pre-existing `planning/sprints/sprint_001/blueprint_feedback.md` in your starter kit. This is the formal record of your blueprint review.

```md
## Section Results
| Section | Verdict | Issues |
|---|---|---|
| AGENTS.md | Approved / Changes needed | [any issues] |
| DOMAIN.md | Approved / Changes needed | [any issues] |
| ... etc. | | |

## Overall Verdict
[ ] Approved  [ ] Changes needed
```

If changes are needed, correct the files before moving to the consistency audit.

---

## Step 3 — Run the Consistency Audit

**Teacher context:**

Before closing the sprint, run a consistency audit on the generated brain files. The AI checks its own output against `docs/requirements.md` and `DECISIONS.md` for correctness, scope accuracy, and terminology.

This step is a standard part of any sprint that produces project brain files. See `docs/modes/design-mode.md` for the full Design Mode consistency audit workflow.

**Files to load into the AI:**

```txt
All generated brain files (AGENTS.md, DOMAIN.md, COMMANDS.md, etc.)
docs/requirements.md
DECISIONS.md
```

**Student action — paste this prompt:**

```txt
You are operating in Design Mode.

Perform a consistency audit on the project brain files just generated
for the Pong game.

You have been provided:
- All generated brain files
- docs/requirements.md
- DECISIONS.md

Produce the audit report at:
planning/sprints/sprint_001/consistency_audit.md

For each file, check and report:

AGENTS.md
- Do the three mode names exactly match: Research Mode, Design Mode, Develop Mode?
- Is the dry run rule present and specific?
- Are the permission levels (0–4) defined?

DOMAIN.md
- Does the v0.1 scope match docs/requirements.md exactly?
- Does the out-of-scope list match the non-goals in requirements?
- Does the project description match the game as defined?

COMMANDS.md
- Does it explain how to open the game in a browser?
- Is it accurate for the technology stack in DECISIONS.md?

DECISIONS.md
- Are all five decisions from Phase 0 present?
- Does each decision include context, options considered, decision, reasoning,
  and consequences?

All files
- Flag any terminology not present in docs/requirements.md.
- Flag any mode name other than Research Mode, Design Mode, or Develop Mode.
- Flag any file that is too generic — content that could apply to any project
  rather than specifically to this Pong game.

Format each file as:

## [Filename]
Status: PASS / FAIL / WARNING
Issues:
- [specific issue]
Recommendation:
- [exact correction needed]

---

End with a summary of files that passed, files that need correction,
and any terminology violations.
```

After the audit, correct each FAIL using a targeted Design Mode correction before closing the sprint.

---

## Step 4 — Review, Save, Close Sprint

Review the corrected output against the Phase 0-B checkpoint requirements. Then close the sprint:

**Student action — generate closing files:**

```txt
You are operating in Design Mode.

Sprint 001 is complete. Generate the closing files:

- planning/sprints/sprint_001/implementation_log.md
- planning/sprints/sprint_001/retrospective.md

The implementation_log must list every file created.
The retrospective must note what the project brain covers and 
what still needs to be decided before the game can be built.

Also:

1. Generate planning/sprints/sprint_001/human_review.md.
   Read acceptance.md for this sprint. Produce one section per
   acceptance group, each with a Pass/Fail/Partial verdict field
   and an issues field. Do not fill in verdicts. Do not fill in
   the approval signature. Stop after this file is written.

2. Update STATE.md:
   - Sprint 001 complete
   - Active sprint: Sprint 002 — Core Game Mechanics
```

**Student action — fill in human_review.md yourself:**

Open `planning/sprints/sprint_001/human_review.md`. Work through each acceptance criterion from `acceptance.md`, fill in the Pass/Fail/Partial verdicts, and sign the approval signature. Only you can mark the sprint approved.

**Student action — rollback_log.md:**

If any files were reverted or redone during this sprint, record them in `planning/sprints/sprint_001/rollback_log.md`. If nothing was rolled back, leave the file blank.

Commit:

```bash
git add .
git commit -m "Sprint 001 complete — project brain"
```

---

## Sprint 001 Checkpoint

```txt
- [ ] All project brain files exist with game-specific content (not generic placeholders)
- [ ] PROMPT_CHANGELOG.md exists (not CHANGELOG.md or VERSION.md)
- [ ] COMMANDS.md explains how to open the game
- [ ] DOMAIN.md describes the game and states v0.1 scope correctly
- [ ] AGENTS.md includes the dry run rule for Develop Mode
- [ ] consistency_audit.md exists and all FAILs have been corrected
- [ ] blueprint_feedback.md is filled in with a verdict
- [ ] human_review.md is filled in and signed by the student
- [ ] rollback_log.md is filled in or left blank (not missing)
- [ ] planning/sprints/sprint_001/ contains all required artifacts
- [ ] STATE.md shows Sprint 002 as next
- [ ] Committed
```

---

# 5. Sprint 002 — Core Game Mechanics

## Lesson Objectives

By the end of Sprint 002, students can:

- Run the full ADDF sprint loop on a code project
- Read a code architecture dry run and evaluate it intelligently
- Authorize implementation without being the code's author
- Verify working software against written acceptance criteria

## Teacher Context

This is the sprint where code gets written. It is the most important sprint in this tutorial because it demonstrates the central ADDF proposition for code projects: **you do not need to write the code yourself to be responsible for it.**

The student directed the research. The student wrote the requirements. The student approved the dry run. The student owns the decisions. The AI wrote the code. All of that is coherent within ADDF.

Walk students through this idea before Sprint 002 begins. The question "but how do I know if the code is right if I didn't write it?" is answered by: the acceptance criteria. If the ball moves, bounces off the top wall, bounces off the paddle, and scores a point when it passes the paddle — the code is right. The student verifies that by playing the game.

---

## Step 1 — Generate the Sprint Pack

**Files to load into the AI:**

```txt
AGENTS.md
DOMAIN.md
STATE.md
DECISIONS.md
docs/requirements.md
planning/backlog.md
```

**Student action — paste this prompt:**

```txt
You are operating in Design Mode.

Generate the sprint pack for Sprint 002 — Core Game Mechanics.

Sprint 002 goal: Build the playable core of the Pong game.
This sprint delivers: ball movement, paddle control, wall bouncing, 
and paddle-ball collision. The game does not need scoring or game states yet.
That comes in Sprint 003.

Produce:
- planning/sprints/sprint_002/requirements.md
- planning/sprints/sprint_002/blueprint.md
- planning/sprints/sprint_002/acceptance.md

Requirements must specify:
- Exact files to be created (e.g., index.html, game.js, style.css)
- Ball starting position and direction
- Ball speed
- Paddle dimensions and speed
- Wall bounce behaviour (top and bottom)
- Paddle collision behaviour
- What "out of bounds" means (ball passes left or right edge)
- What the sprint does NOT include (scoring, win state — deferred to Sprint 003)

Blueprint must:
- List each file with its exact path
- Describe the key functions or components each file will contain
- Specify the order of implementation
- Note any dependency between files (e.g., game.js must be loaded after the canvas exists)

Acceptance criteria must be verifiable by opening the game in a browser:
- Ball appears on screen
- Ball moves continuously
- Ball bounces off top and bottom walls
- Left paddle responds to [key] and [key] inputs
- Right paddle responds to [key] and [key] inputs
- Ball bounces off each paddle
- Ball disappears or resets when it passes the left or right edge
- No JavaScript console errors on load

Do not write game code yet.
```

**Expected output:**

Three sprint pack files. The blueprint is critical — review it carefully.

**Review the blueprint for:**

```txt
Does it specify the canvas size? (A number, not "an appropriate size")
Does it describe the game loop? (requestAnimationFrame or setInterval)
Does it say what happens when the ball goes out of bounds?
Does the file structure match what was decided in DECISIONS.md?
Are the keyboard keys specified? (W/S for left, Up/Down for right — or whatever was decided)
Is there any scope creep? (Scoring appearing when it should wait for Sprint 003)
```

If the blueprint is vague, reject it:

```txt
You are still in Design Mode.

The blueprint does not specify the canvas dimensions or keyboard controls.
These are required before the dry run can be meaningful.

Add:
- Canvas dimensions (exact pixels)
- Left paddle controls (exact keys)
- Right paddle controls (exact keys)
- Game loop method to be used

Regenerate blueprint.md with these additions.
```

**Student action — fill in blueprint_feedback.md:**

After the blueprint passes review, fill in `planning/sprints/sprint_002/blueprint_feedback.md` with your verdict and any issues noted. This is your formal sign-off before Develop Mode opens.

---

## Step 2 — Develop Mode Level 0: Dry Run

**Teacher context:**

This is the first code dry run students have done. Explain what it looks like before they run it:

> "The dry run for a code project is different from a Markdown dry run. The model will describe the architecture — what files it will create, what functions will be in each file, what each function does. It will not write the actual code yet. Your job is to read the description and decide whether this architecture makes sense before a single line of code is written."

**Files to load into the AI (fresh session):**

```txt
AGENTS.md
STATE.md
COMMANDS.md
planning/sprints/sprint_002/requirements.md
planning/sprints/sprint_002/blueprint.md
planning/sprints/sprint_002/acceptance.md
```

**Student action — paste this prompt:**

```txt
You are operating in Develop Mode.

Permission Level: 0 — Dry Run Only.

Read the sprint pack provided. Do not write any game code.

Produce: planning/sprints/sprint_002/dry_run.md

The dry run must include:

1. Files to create — exact path and description of contents
   For each JavaScript file, list the key functions or objects it will contain
   and what each one does in one sentence.

2. Game loop description — describe how the game loop will work step by step
   (What runs on each frame? In what order?)

3. Collision detection approach — describe how ball-paddle and ball-wall
   collisions will be detected (bounding box? radius? exact method?)

4. Input handling approach — describe how keyboard input will be captured

5. Files to modify — none expected for this sprint

6. Files to move or delete — none expected for this sprint

7. Commands to verify — how will the student confirm the game runs?

8. Dependencies — any CDN links or external files required
   Note: if any CDN dependency is listed here that does not already appear
   in DECISIONS.md, stop after this dry run. Add a DECISIONS.md entry for
   the dependency before authorizing implementation.

9. Risks — what could go wrong in this sprint?
   (Be specific: "collision detection at high ball speeds may miss paddle edge")

10. Ambiguities — anything in the blueprint that is unclear

Stop after producing dry_run.md.
Do not write index.html.
Do not write game.js.
Do not write style.css.
```

**Expected output:**

`dry_run.md` with a clear description of the game architecture. Students should be able to read this and understand:

- What files will exist after Sprint 002
- How the game loop works conceptually
- How collisions will be detected
- What the keyboard mapping will be

---

## Step 3 — Review the Code Dry Run

**Teacher context:**

Students are reviewing an architecture plan for code they did not write. This is uncomfortable for developers who are used to writing everything themselves. Normalize it.

The question is not "is this code I would have written?" The question is "does this architecture satisfy the requirements?"

Give students 15 minutes. Walk around and help those who are stuck.

**Student action — review against these questions:**

```txt
Architecture check:
- [ ] The game loop approach (requestAnimationFrame/setInterval) is specified
- [ ] The collision detection method is described specifically enough to evaluate
- [ ] Each file's purpose is clear
- [ ] The keyboard mapping matches the requirements document

Scope check:
- [ ] No scoring appears in the dry run (deferred to Sprint 003)
- [ ] No game state logic appears (deferred to Sprint 003)
- [ ] No sound effects (non-goal)
- [ ] No AI opponent (unless chosen — non-goal for most students)

Risk assessment:
- [ ] Collision detection risk is acknowledged
- [ ] The student can articulate one specific risk they would watch for
```

Write `planning/sprints/sprint_002/dry_run_review.md`:

```md
# Sprint 002 Dry Run Review

## Decision

[Approved / Not Approved]

## Architecture Assessment

[Your assessment of whether the described architecture will work]

## Issues Found

[Specific problems or questions]

## Corrections Required Before Proceeding

[If not approved — exact changes needed]

## One Risk I Am Watching

[The specific thing you will check most carefully during the playtest]

## Authorized Permission Level

1 — Approved Sprint Scope

## Reviewer

[Your name]

## Date

[Date]
```

**Teacher note on the "One Risk I Am Watching" field:**

This field is intentional. Require students to fill it in. The most common risk for Pong is collision detection — at high ball speeds, the ball may pass through the paddle in a single frame. If a student writes "collision at high speed may not register," they are likely to catch it during the playtest. If they write "I'm not sure," have them go back to the dry run and find the collision detection section.

---

## Step 4 — Develop Mode Level 1: Implement

**Teacher context:**

Authorization is a two-step process. First, students have filled in `dry_run_review.md` approving the dry run. Now they send the authorization message separately — a short, specific message that upgrades the permission level. The AI does not proceed until it receives this message.

**Student action — send the authorization message first:**

```txt
Dry run approved.
Permission Level 1 authorized.
Proceed according to requirements.md, blueprint.md, acceptance.md, and dry_run.md.
```

**Then send the implementation rules (same session):**

```txt
You are operating in Develop Mode at Permission Level 1 — Approved Sprint Scope.

Rules:
- Implement only what is in the dry run.
- Do not add scoring or game states (Sprint 003).
- Do not add sound (non-goal).
- Do not add an AI opponent unless it was in the requirements.
- Log every file created in planning/sprints/sprint_002/implementation_log.md.
- If an ambiguity appears that requires a decision, stop and describe it.
  Do not guess.
```

**Expected output:**

The game files (index.html, game.js, style.css — or as defined in the blueprint) plus `implementation_log.md`.

---

## Step 5 — Verify by Playing the Game

**Teacher context:**

This is the most important step. Students open the game in their browser and play it.

Do not let students skip straight to closing the sprint. Require a real playtest.

**Student action:**

Open `index.html` in a browser.

Go through each acceptance criterion in `planning/sprints/sprint_002/acceptance.md` and mark it pass or fail.

```txt
- [ ] Ball appears on screen
- [ ] Ball moves continuously without stopping
- [ ] Ball bounces off the top wall
- [ ] Ball bounces off the bottom wall
- [ ] Left paddle moves up with [W key]
- [ ] Left paddle moves down with [S key]
- [ ] Right paddle moves up with [Up arrow]
- [ ] Right paddle moves down with [Down arrow]
- [ ] Ball bounces off the left paddle
- [ ] Ball bounces off the right paddle
- [ ] Ball resets when it passes the left edge
- [ ] Ball resets when it passes the right edge
- [ ] No JavaScript console errors on load
```

**If a criterion fails:**

Ask the AI for a targeted fix using a scoped Develop Mode correction:

```txt
You are operating in Develop Mode.

Permission Level: 1 — Bug fix, approved.

The ball is not bouncing off the left paddle correctly. 
It passes through the paddle instead of bouncing.

The issue is in the collision detection between the ball and the left paddle.

Fix only the collision detection for the left paddle.
Do not change any other game behaviour.
Log the change in implementation_log.md and describe what was wrong.
```

**Teacher note:**

Paddle collision bugs are extremely common in AI-generated Pong code. The most frequent issue is that the collision check uses the wrong coordinate system or misses the case where the ball moves faster than the paddle width in a single frame.

If multiple students hit the same collision bug, use it as a teaching moment: this is exactly what the risk section of the dry run was supposed to flag. If the dry run mentioned this risk and students approved it anyway, they accepted the risk and now they are managing it. That is correct ADDF operation.

---

## Step 6 — Close Sprint 002

**Student action — generate closing files:**

```txt
You are operating in Design Mode.

Sprint 002 is complete. The core game mechanics are implemented and verified.

Generate:
- planning/sprints/sprint_002/retrospective.md

Include:
- What the sprint produced (describe the working game state)
- What worked well in the AI-generated code
- What required correction and why
- What the playtest revealed
- What risk from the dry run actually materialized (if any)
- What carries forward to Sprint 003

Then generate planning/sprints/sprint_002/human_review.md.
Read acceptance.md for this sprint. Produce one section per
acceptance criterion group, each with a Pass/Fail/Partial verdict field
and an issues field. Do not fill in verdicts. Do not fill in the
approval signature. Stop after this file is written.

Update STATE.md:
- Sprint 002 complete
- Active sprint: Sprint 003 — Scoring and Game States
```

**Student action — fill in human_review.md yourself:**

Open `planning/sprints/sprint_002/human_review.md`. Work through the playtest results from Step 5 and fill in the verdicts. Your playtest notes from `human_review.md` should be your honest experience — not just "looks good."

**Student action — rollback_log.md:**

If any game code was reverted or rewritten during this sprint (e.g., collision detection was scrapped and redone), record it in `planning/sprints/sprint_002/rollback_log.md`. Otherwise leave it blank.

Commit:

```bash
git add .
git commit -m "Sprint 002 complete — core game mechanics"
```

---

## Sprint 002 Exercise

> The ball currently resets when it passes the edge. But where does it reset to?
> Does it go back to the center? Does it go to the side that scored? 
> Does it launch in a random direction or always the same direction?
>
> Open docs/requirements.md.
>
> Find the section that describes ball reset behaviour after scoring.
> If it is not there, that is a gap in the requirements.
>
> Write a one-paragraph addition to docs/requirements.md that specifies 
> exactly what happens when the ball goes out of bounds.
> Then check whether the implementation matches your specification.
> If it does not, write a scoped Develop Mode fix.

This exercise teaches students that incomplete requirements produce incomplete or arbitrary behaviour. The reset behaviour is a genuine gap that AI-generated Pong often leaves underspecified.

---

## Sprint 002 Checkpoint

```txt
- [ ] Game files exist (index.html and associated files)
- [ ] Game opens in a browser without errors
- [ ] Ball moves continuously
- [ ] Ball bounces off all four walls (or top/bottom + paddles)
- [ ] Both paddles respond to correct keyboard controls
- [ ] Ball resets when it passes left or right edge
- [ ] blueprint_feedback.md is filled in with a verdict
- [ ] dry_run_review.md contains a written decision with reasoning
- [ ] human_review.md is filled in and signed by the student
- [ ] rollback_log.md is filled in or left blank (not missing)
- [ ] Any bugs found were fixed with scoped Develop Mode corrections
- [ ] implementation_log.md records all files created and any corrections
- [ ] retrospective.md exists
- [ ] STATE.md updated
- [ ] Committed
```

---

# 6. Sprint 003 — Scoring and Game States

## Lesson Objectives

By the end of Sprint 003, students can:

- Run the sprint loop with less teacher guidance
- Manage the transition between game states in requirements
- Recognize when implementation behaviour contradicts requirements

## Teacher Context

Sprint 003 adds the remaining gameplay layer: scoring and game states. The game currently runs forever. Sprint 003 makes it a complete game with a start state, a playing state, a win condition, and a game-over state.

Students should run more of this sprint independently. Intervene only when they are stuck or when you see a systematic problem.

The new complexity is game states. Walk through this concept briefly before students start:

```txt
State: Not Started
   What the player sees: title screen or instructions
   What happens: game waits for input to begin

State: Playing
   What the player sees: paddles, ball, current score
   What happens: game loop runs

State: Game Over
   What the player sees: winner announcement, final score
   What happens: game waits for input to restart
```

Students should define these states in the sprint requirements before asking the AI to implement them.

---

## Step 1 — Sprint Pack (More Independent)

Students should attempt the sprint pack prompt without a pre-written template. Give them this brief:

> "Generate the Sprint 003 sprint pack. Sprint 003 adds scoring and game states to the working game core from Sprint 002. Use docs/requirements.md for the scoring rules and win condition. The blueprint must specify exactly how game state will be managed in the code — not just that it will exist."

After they generate the sprint pack, review the blueprints together. Ask:

- Does the blueprint describe how state is tracked? (A variable? An object? A string?)
- Does it describe what triggers the transition between states?
- Does it specify what the win screen shows?
- Does it handle the case where score reaches the win condition mid-rally?

After the blueprint passes review, students fill in `planning/sprints/sprint_003/blueprint_feedback.md` before opening any Develop Mode session.

---

## Step 2 — Dry Run and Review

Students run the dry run independently.

After they write `dry_run_review.md`, compare as a group:

- What risks did everyone find?
- Did anyone approve a dry run that had a state transition problem?
- Did the collision detection from Sprint 002 create any implications for scoring?
  (What if the ball clips through the paddle at the moment of scoring?)

---

## Step 3 — Implement and Full Playtest

After implementation, require a complete game playtest — not just checking that the score appears. Students must play to the win condition.

**Required playtest scenario:**

```txt
1. Open the game. Confirm the start state appears.
2. Start the game. Confirm the playing state begins.
3. Allow a point to be scored. Confirm the score updates correctly.
4. Play until one player reaches the win condition.
5. Confirm the game-over state appears with the correct winner.
6. Restart the game. Confirm it returns to the start or playing state.
7. Check that the score resets on restart.
```

Any failure in this sequence is a bug. Use a scoped Develop Mode correction to fix it.

---

## Step 4 — Close Sprint 003 Independently

Students close the sprint using the same pattern as Sprint 002:

```txt
1. Design Mode generates retrospective.md
2. Design Mode generates human_review.md (blank template with verdict fields — do not fill in verdicts)
3. Student fills in human_review.md and signs it
4. Student fills in rollback_log.md or leaves it blank
5. STATE.md update (Design Mode)
6. Commit
```

---

## Sprint 003 Exercise

> The game is now playable from start to game over.
>
> Play a full game yourself — both sides.
>
> Write a one-paragraph "player experience" note in human_review.md that 
> answers these questions from a player's perspective (not a developer's):
>
> 1. Does the game feel fair? Does either player have an advantage?
> 2. Is the ball speed appropriate — too fast, too slow, or right?
> 3. Is the paddle responsive, or does it feel laggy?
> 4. Is there anything confusing about the game rules as presented?
>
> Then decide: are any of these problems bugs (wrong implementation),
> or are they design gaps (the requirements did not specify well enough)?
> Record your conclusion in QUESTIONS.md.

This exercise teaches students to distinguish implementation bugs from requirements gaps. Both are real problems, but they are fixed differently — a bug is a Develop Mode correction, a gap is a requirements update followed by a new sprint.

---

## Sprint 003 Checkpoint

```txt
- [ ] Score displays on screen and updates when a point is scored
- [ ] Points are awarded to the correct player
- [ ] Win condition triggers when the threshold is reached
- [ ] Game-over state shows the winner
- [ ] Game can be restarted
- [ ] Score resets on restart
- [ ] Full playtest completed (start → win condition → restart)
- [ ] blueprint_feedback.md is filled in with a verdict
- [ ] human_review.md is filled in and signed by the student
- [ ] Player experience note exists in human_review.md
- [ ] rollback_log.md is filled in or left blank (not missing)
- [ ] retrospective.md exists
- [ ] STATE.md updated
- [ ] Committed
```

---

# 7. The Path to v1.0

After Sprint 003, students have a complete and playable Pong game. The core loop works, scoring works, game states work.

v1.0 still needs:

```txt
Sprint 004 — Polish and visual design
Sprint 005 — v1.0 Release (packaging and deployment)
```

## Hints for Sprint 004 — Polish

Sprint 004 is where the game goes from functional to presentable. Common items:

```txt
Visual design: background colour, paddle colour, ball colour, score font and placement
Start screen: title, player labels, how-to-play instructions
Game-over screen: winner announcement, restart prompt
Pause functionality (if in requirements)
Ball speed progression (if in requirements — ball accelerates over time)
```

**Teaching hint:**

Sprint 004 should be student-directed. Give them the sprint pack brief and step back. This is the sprint where students have enough ADDF experience to run the loop independently.

One thing to watch: students often want to redesign the entire visual identity of the game in Sprint 004. Keep them focused. The sprint should improve what exists, not rethink the architecture. Anything that requires architectural changes goes back to requirements.

**Sprint pack brief to give students:**

> "Generate the Sprint 004 sprint pack. Sprint 004 polishes the visual design and presentation of the Pong game. It does not change game mechanics or scoring rules. The blueprint must list every specific visual change — exact colours, font sizes, and screen layouts."

## Hints for Sprint 005 — Release

Sprint 005 packages the game for v1.0.

For a browser game, release means:

```txt
The game works from a single clean file download or GitHub Pages URL.
The README explains what the game is and how to play it.
The v1.0 tag exists in Git.
VERSION.md is updated.
CHANGELOG.md records what shipped.
```

**Teaching hint:**

If students chose a technology that requires a build step (Phaser.js from npm, p5.js from npm), Sprint 005 is also where that build process gets set up. If they used CDN links or vanilla JS, no build step is needed — the release is just the files.

The release acceptance criteria should include:

```txt
- [ ] A stranger can download or clone the repo and play the game immediately
- [ ] The README explains controls and win condition
- [ ] No setup steps beyond opening the HTML file are required (for CDN/vanilla builds)
- [ ] v1.0 is tagged in Git
```

## Two Sprint Loop Steps This Tutorial Simplified

The official ADDF Sprint Loop has 11 steps. This tutorial compresses two of them worth naming explicitly for teachers:

**Dependency Approval Gate (Sprint Loop Step 6):** If a student's dry run lists a CDN dependency (e.g., a Phaser.js CDN link) that does not already appear in DECISIONS.md, implementation must pause. The student adds a DECISIONS.md entry for that dependency before sending the authorization message. Students who chose Phaser or p5.js in Phase 0-B should already have this covered — but check their dry run to be sure.

**Design Review of Output (Sprint Loop Step 9):** After implementation, the full Sprint Loop includes a Design Mode review of the built files against the sprint pack — before the human playtest. This tutorial goes directly to playtest, which works well for a game (the ball either moves or it doesn't). For future projects where output is harder to verify visually, students should know this step exists. From the framework docs: Design Mode compares `implementation_log.md` and the changed files against `requirements.md`, `blueprint.md`, and `acceptance.md`, and returns an assessment before the human approval gate.

---

## The Framework Viability Question

At the end of Sprint 003, ask students to reflect on the process:

```txt
1. Would you have been able to build this game without ADDF?
   (Probably yes — Pong is small)

2. What did ADDF add?
   - A record of why each decision was made
   - A point where you could catch a bad architecture before writing code
   - A project that another person could pick up from the files alone
   - Acceptance criteria that forced you to test specifically

3. Where did ADDF feel like too much process?
   - If somewhere felt heavy, note it. That is useful framework feedback.

4. What would break down at larger scale without this structure?
   - A 10-sprint project with 3 developers
   - A 6-month pause and then resumption
   - Handing the project to a different AI model
```

Record student answers in `QUESTIONS.md` and `RISKS.md`. These feed back into the framework's evolution.

---

# 8. Appendix A — Seed File Templates

## `STATE.md` (seed version — Phase 0 start)

```md
# STATE.md

## Project

Pong Game — Browser-based two-player game

## Current Goal

Research technology options and game design decisions before writing requirements.

## Active Lifecycle Stage

Research

## Current Status

Research phase beginning. No requirements written. No technology decided.

## Next Step

Complete technology stack research and game design research,
then move to Design Mode to write requirements.
```

## `SECURITY.md` (seed version)

```md
# SECURITY.md

## Files That Must Never Be Loaded Into AI Tools

- Any file containing API keys or credentials
- Any .env file

## Repository Rules

- Do not commit secrets or tokens.
- This is a client-side game with no backend — secrets are unlikely
  but still possible if API integrations are added later.
```

---

# 9. Appendix B — Standard Prompts Reference

## Research Mode — Technology Investigation

```txt
You are operating in Research Mode.

Investigate [specific technical question].

For each option, return:
- What it provides
- What it requires
- Tradeoffs specific to [project type]
- Suitability for [specific constraint]

Rules:
- Do not recommend a final choice.
- Do not write code.
- Return structured findings.

Save output to: research/[filename].md
```

## Design Mode — Requirements Generation

```txt
You are operating in Design Mode.

Using [research documents and decisions], produce a requirements document 
for [project].

Save output to: docs/requirements.md

The requirements must cover:
[list sections]

Rules:
- Write specific, testable requirements.
- Do not write code.
- Non-goals must be explicit.
```

## Design Mode — Sprint Pack

```txt
You are operating in Design Mode.

Generate the sprint pack for Sprint 00X — [Sprint Name].

Sprint goal: [one sentence]

Produce:
- planning/sprints/sprint_00X/requirements.md
- planning/sprints/sprint_00X/blueprint.md
- planning/sprints/sprint_00X/acceptance.md

Blueprint must list exact file paths.
Acceptance criteria must be verifiable without the model's help.
Do not begin implementation.
```

## Develop Mode — Code Dry Run

```txt
You are operating in Develop Mode.

Permission Level: 0 — Dry Run Only.

Load:
- AGENTS.md
- STATE.md
- COMMANDS.md
- planning/sprints/sprint_00X/requirements.md
- planning/sprints/sprint_00X/blueprint.md
- planning/sprints/sprint_00X/acceptance.md

Produce: planning/sprints/sprint_00X/dry_run.md

Include all seven required areas:
1. Files to create — exact paths and key functions/components each contains
2. Files to modify
3. Files to move or delete
4. Commands to verify the implementation
5. Dependencies (if any CDN or external dependency is new, flag it — 
   a DECISIONS.md entry is required before authorization proceeds)
6. Risks (be specific — name the failure mode, not just the category)
7. Ambiguities

You may also include:
- Architecture description — how the pieces connect
- Implementation approach for the most complex requirement

Stop after dry_run.md. Do not write implementation files.
```

## Develop Mode — Authorization

Send this as a standalone message after reviewing and approving the dry run. This is the gate — the model does not proceed without it.

```txt
Dry run approved.
Permission Level 1 authorized.
Proceed according to requirements.md, blueprint.md, acceptance.md, and dry_run.md.
```

Then follow immediately with implementation rules:

```txt
Implement only what is in the dry run.
Log every file created in implementation_log.md.
Stop if ambiguity appears. Record it in QUESTIONS.md and wait.
```

## Develop Mode — Scoped Bug Fix

```txt
You are operating in Develop Mode.

Permission Level: 1 — Bug fix, approved.

The following behaviour is incorrect: [describe specific bug]

Fix only [specific component or function].
Do not change any other behaviour.
Log the fix in implementation_log.md and describe what was wrong.
```

## Design Mode — Sprint Close (retrospective + human_review template)

Run this at the end of every sprint's Develop Mode, before human review.

**Load first:** `AGENTS.md`, full sprint folder (`requirements.md`, `blueprint.md`, `acceptance.md`, `dry_run.md`, `implementation_log.md`)

```txt
You are operating in Design Mode. This sprint's implementation is complete.

Perform the sprint close sequence:

Step 1 — Generate planning/sprints/sprint_00X/retrospective.md.
Record what was planned, what was built, any variances from the blueprint,
and lessons learned.

Step 2 — Generate planning/sprints/sprint_00X/human_review.md.
Read acceptance.md and produce one section per acceptance group, each with
a Pass/Fail/Partial verdict field and an issues field.
Do not fill in verdicts. Do not fill in the approval signature. Stop.

Step 3 — Update STATE.md: set Active Sprint to [NUMBER], Current Status to
"Sprint [NUMBER] complete — awaiting human review", and Next Step to
"Human reviews human_review.md against acceptance.md."

Do not mark the sprint approved. That is the human's decision.
```

After the AI stops, open `human_review.md`, fill in verdicts from your playtest or review results, and sign the approval signature.

---

## Design Mode — Consistency Audit

```txt
You are operating in Design Mode.

Perform a consistency audit on the files listed below.
Check them against [source documents — requirements, docs/, DECISIONS.md].

Produce the audit report at: planning/sprints/sprint_00X/consistency_audit.md

For each file:
## [Filename]
Status: PASS / FAIL / WARNING
Issues:
- [specific issue]
Recommendation:
- [exact correction needed]

Check for:
- Terminology that does not appear in the source documents
- Mode names other than Research Mode, Design Mode, Develop Mode
- Scope that contradicts the requirements document
- Missing required sections
- Generic content that should be project-specific

End with a summary of passes, failures, and any terminology violations.
```

## Session Start Confirmation

```txt
You are operating in [MODE].

Load:
- AGENTS.md
- DOMAIN.md
- STATE.md
- [any sprint files]

Confirm you have loaded these files and state:
1. Current project goal
2. Your mode and what you are allowed to do
3. What you must not do
4. Active sprint

Wait for my task instruction.
```

---

# 10. Appendix C — Review Checklists

## Research Output Review

```txt
- [ ] Output does not contain code
- [ ] Output does not make a recommendation (Research Mode does not decide)
- [ ] Each option is compared on the same criteria
- [ ] At least one risk or tradeoff is specific to this project, not generic
- [ ] Output is organized enough to be useful input for Design Mode
```

## Requirements Review

```txt
- [ ] Requirements are specific and testable
- [ ] No requirement is vague ("should feel smooth", "should look good")
- [ ] Non-goals section exists
- [ ] File structure is defined
- [ ] Acceptance criteria are verifiable by using the software
- [ ] Win condition is explicitly stated
- [ ] All gameplay rules are covered (what happens at edges, on collision, on reset)
```

## Blueprint Review (Code Sprint)

```txt
- [ ] Every file is listed with its exact path
- [ ] Key functions or components are named and described for each file
- [ ] No file is described vaguely ("handles game logic")
- [ ] Architecture is coherent (dependencies flow in one direction)
- [ ] Nothing in the blueprint is outside sprint scope
- [ ] Implementation order makes sense (HTML before JS that references it)
```

## Code Dry Run Review

```txt
- [ ] Game loop approach is specified
- [ ] Collision detection method is described concretely
- [ ] Keyboard input handling is described
- [ ] Every file in the dry run was in the blueprint
- [ ] No file in the dry run was absent from the blueprint
- [ ] Risks section identifies at least one specific failure mode
- [ ] Ambiguities section is honest
```

## Playtest Review

```txt
- [ ] All acceptance criteria marked pass or fail
- [ ] Every fail has a logged correction or a documented decision to defer
- [ ] Ball movement looks correct
- [ ] Both paddles respond
- [ ] Scoring is accurate
- [ ] Game states transition correctly
- [ ] No console errors
- [ ] Player experience note written (is the game fair? is the speed right?)
```

## Sprint Close

```txt
- [ ] implementation_log.md lists all files created and all corrections made
- [ ] human_review.md includes playtest results (not just "looks good")
- [ ] retrospective.md exists and is honest
- [ ] STATE.md updated
- [ ] Committed
```

---

*Quack!*
