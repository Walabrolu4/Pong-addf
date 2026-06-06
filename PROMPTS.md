# PROMPTS.md — `[YOUR PROJECT NAME]`

Ready-to-use prompts for every moment in the ADDF workflow. Copy, fill in the bracketed parts, and send. Each prompt tells you which files to load first.

For the full ADDF prompt catalog, see `prompts/README.md` in the public ADDF repository. This starter-kit file contains the minimum prompts needed to start and operate a new project.

---

## 1. Session Start — Resume an existing project

Use this at the beginning of every session after the first.

**Load first:** `AGENTS.md`, `STATE.md`, `DOMAIN.md`  
**Also load:** The active sprint pack if you are in a sprint (`requirements.md`, `blueprint.md`, `acceptance.md`)

```
You are working on [YOUR PROJECT NAME].

Load and read the following files before doing anything else:
- AGENTS.md
- STATE.md
- DOMAIN.md
- [Add active sprint pack files if in a sprint]

Confirm you have read them. State the current mode, active sprint, and next step from STATE.md. Then wait for instructions.
```

---

## 2. Research Mode — Investigate a question or technology

Use this when you have unknowns before you can plan or build.

**Load first:** `AGENTS.md`, `STATE.md`, `DOMAIN.md`, `QUESTIONS.md`

```
You are in Research Mode for [YOUR PROJECT NAME].

Loaded files: AGENTS.md, STATE.md, DOMAIN.md, QUESTIONS.md.

Research question: [DESCRIBE WHAT YOU NEED TO KNOW]

Produce a research note in `research/notes.md` covering:
- What you found
- Key trade-offs or options
- Recommended direction
- Open questions that remain

Do not record any decisions. Do not modify any implementation files. Add any new unknowns to QUESTIONS.md. Stop when the research note is written.
```

---

## 3. Design Mode — Generate project brain files (first session)

Use this to create the core project brain files for a new project.

**Load first:** `AGENTS.md`, `DOMAIN.md` (after you have filled them in manually)  
**Also load:** Any research notes, requirements documents, or specification files you have

```
You are in Design Mode for [YOUR PROJECT NAME].

Loaded files: AGENTS.md, DOMAIN.md, [LIST ANY RESEARCH OR REQUIREMENTS FILES].

Generate the following project brain files with complete, realistic content for [YOUR PROJECT NAME]:
- DECISIONS.md
- COMMANDS.md
- QUESTIONS.md
- RISKS.md
- STYLE_GUIDE.md
- GIT_STRATEGY.md
- PROMPT_CHANGELOG.md
- STATE.md

Base all content on DOMAIN.md and the loaded files. Use placeholders only where a decision has not yet been made. Do not write source code. Stop when all files are written.
```

---

## 4. Design Mode — Generate a sprint pack

Use this to plan a sprint before building anything.

**Load first:** `AGENTS.md`, `STATE.md`, `DOMAIN.md`, `DECISIONS.md`, `planning/backlog.md`

```
You are in Design Mode for [YOUR PROJECT NAME].

Loaded files: AGENTS.md, STATE.md, DOMAIN.md, DECISIONS.md, planning/backlog.md.

Generate the sprint pack for Sprint [NUMBER] — [SPRINT TITLE]:
- planning/sprints/sprint_[NUMBER]/requirements.md
- planning/sprints/sprint_[NUMBER]/blueprint.md
- planning/sprints/sprint_[NUMBER]/acceptance.md

Base scope on the backlog entry for this sprint. Keep scope tight — only what can be completed and verified this sprint. Do not write source code. Stop when all three files are written.
```

---

## 5. Develop Mode — Dry run (Permission Level 0)

Use this to get a dry run before any implementation begins.

**Load first:** `AGENTS.md`, `STATE.md`, active sprint pack (`requirements.md`, `blueprint.md`, `acceptance.md`)

```
You are in Develop Mode for [YOUR PROJECT NAME] at Permission Level 0.

Loaded files: AGENTS.md, STATE.md, requirements.md, blueprint.md, acceptance.md.

Produce `planning/sprints/sprint_[NUMBER]/dry_run.md`. The dry run must list all seven content areas:
1. Files to create
2. Files to modify
3. Files to move or delete
4. Commands to run
5. Dependencies requested
6. Risks
7. Ambiguities

Do not create, modify, or delete any files other than dry_run.md.
Stop when dry_run.md is written. Do not proceed. Await human authorization.
```

---

## 6. Develop Mode — Authorization message

Send this exact message after reviewing and approving the dry run. Replace [LEVEL] with the permission level you are granting (usually 1).

```
Dry run approved.
Permission Level [LEVEL] authorized.
Proceed according to requirements.md, blueprint.md, acceptance.md, and dry_run.md.
```

---

## 7. Develop Mode — Resume after interruption

Use this when a session ended mid-sprint (context limit, crash, or manual stop).

**Load first:** `AGENTS.md`, `STATE.md`, active sprint pack, `implementation_log.md`

```
You are in Develop Mode for [YOUR PROJECT NAME] at Permission Level [LEVEL].

Loaded files: AGENTS.md, STATE.md, requirements.md, blueprint.md, acceptance.md, implementation_log.md.

This session is resuming after an interruption. Read implementation_log.md to identify what has already been completed. Cross-reference with blueprint.md to identify what remains.

List the remaining tasks before doing anything. Then continue from where the previous session stopped. Update implementation_log.md after each file you write or modify.
```

---

## 8. Design Mode — Run a consistency audit

Use this after generating files to verify they are internally consistent and match the docs.

**Load first:** `AGENTS.md`, `DOMAIN.md`, all generated files from the sprint, any relevant `docs/` files

```
You are in Design Mode for [YOUR PROJECT NAME].

Loaded files: AGENTS.md, DOMAIN.md, [LIST ALL FILES GENERATED THIS SPRINT], [LIST RELEVANT docs/ FILES].

Perform a consistency audit. Check every loaded file for:
- Incorrect mode names (only Research Mode, Design Mode, Develop Mode are valid)
- Content that contradicts DOMAIN.md scope
- Placeholder text that should have been replaced
- Missing required sections
- Terminology inconsistencies

Produce `planning/sprints/sprint_[NUMBER]/consistency_audit.md` with a verdict (PASS / FAIL / WARNING) for each file checked, a description of every issue found, and a recommended fix for each FAIL. Do not modify any files. Stop when the audit is written.
```

---

## 9. Design Mode — Sprint close: generate retrospective and human review

Use this at the end of a sprint's Develop Mode, before human review.

**Load first:** `AGENTS.md`, full sprint folder (`requirements.md`, `blueprint.md`, `acceptance.md`, `dry_run.md`, `implementation_log.md`)

```
You are in Design Mode for [YOUR PROJECT NAME]. This sprint's implementation is complete.

Loaded files: AGENTS.md, requirements.md, blueprint.md, acceptance.md, dry_run.md, implementation_log.md.

Perform the sprint close sequence:

Step 1 — Generate `planning/sprints/sprint_[NUMBER]/retrospective.md`. Record what was planned, what was built, any variances from the blueprint, and lessons learned.

Step 2 — Generate `planning/sprints/sprint_[NUMBER]/human_review.md`. Read acceptance.md and produce one section per acceptance group, each with a Pass/Fail/Partial verdict field and an issues field. Do not fill in verdicts. Do not fill in the approval signature. Stop after this file is written.

Step 3 — Update STATE.md: set Active Sprint to [NUMBER], Current Status to "Sprint [NUMBER] complete — awaiting human review", and Next Step to "Human reviews human_review.md against acceptance.md."

Do not mark the sprint approved. That is the human's decision.
```

---

## 10. Handoff — Pass work to a new model or new session

Use this when intentionally ending a session so another session can resume.

**Load first:** `AGENTS.md`, `STATE.md`, active sprint pack, `implementation_log.md`

```
You are in Design Mode for [YOUR PROJECT NAME]. This session is ending.

Loaded files: AGENTS.md, STATE.md, requirements.md, blueprint.md, acceptance.md, implementation_log.md.

Generate `handoff_summary.md` in the active sprint folder. It must include:
- What was completed this session (reference implementation_log.md)
- What was not completed and why
- Any decisions or open questions that arose
- The exact next action for the incoming session
- Which files the incoming session must load first

Write to `planning/sprints/sprint_[NUMBER]/handoff_summary.md`. Then update STATE.md to reflect session end. Stop.
```

---

*ADDF · `PROMPTS.md` · starter kit version 0.1.0*
