# AGENTS.md - PongTest

This file defines how AI sessions operate for PongTest, a browser-based Pong game built with vanilla JavaScript and the HTML5 Canvas API under the Autonomous Duck Deployment Framework.

## 1. Session Contract

PongTest uses three modes: Research Mode, Design Mode, and Develop Mode. Stay within the active mode. Do not cross from planning into implementation without the dry run approval sequence.

Project truth lives in the Markdown project brain:

- `AGENTS.md`
- `DOMAIN.md`
- `STATE.md`
- `DECISIONS.md`
- `COMMANDS.md`
- `QUESTIONS.md`
- `RISKS.md`
- `STYLE_GUIDE.md`
- `GIT_STRATEGY.md`
- `START_HERE.md`
- `VERSION.md`
- `CHANGELOG.md`
- `docs/requirements.md`
- `research/`

## 2. Research Mode

### Purpose

Investigate and synthesize information before requirements, decisions, or implementation changes are made.

### Allowed Actions

- Read safe-to-load project files.
- Read `docs/`, `research/`, and planning files.
- Search approved external sources when current facts are needed.
- Produce research notes and validation reports.
- Update `research/`, `QUESTIONS.md`, and `RISKS.md` when new unknowns or risks are found.

### Forbidden Actions

- Do not write game implementation files.
- Do not write `index.html`, `styles.css`, or `game.js`.
- Do not write sprint packs unless the session is explicitly in Design Mode.
- Do not record accepted decisions in `DECISIONS.md`.
- Do not modify build, test, or release files.

## 3. Design Mode

### Purpose

Convert research, requirements, and human choices into durable project memory.

### Allowed Actions

- Create and update project brain files.
- Create and update documentation in `docs/`.
- Create and update sprint packs: `requirements.md`, `blueprint.md`, and `acceptance.md`.
- Record accepted decisions in `DECISIONS.md`.
- Update `STATE.md`.
- Create validation reports, dry-run reviews, release plans, feature briefs, retrospectives, and handoff notes.

### Forbidden Actions

- Do not write game code.
- Do not create or modify `index.html`, `styles.css`, or `game.js`.
- Do not modify implementation logs.
- Do not run implementation commands that change source files.
- Do not add features outside the v1.0 scope in `docs/requirements.md`.

## 4. Develop Mode

### Purpose

Modify implementation files after a dry run has been approved by the human.

### Allowed Actions

- At Permission Level 0: produce `dry_run.md` only.
- At Permission Level 1 or higher: modify only files listed in both the approved sprint blueprint and approved dry run.
- Write and run tests within the approved sprint scope.
- Update `implementation_log.md` after implementation changes.
- Produce `handoff_summary.md` when needed.

### Forbidden Actions

- Do not modify game logic without an approved dry run.
- Do not modify files outside the approved sprint scope.
- Do not add third-party libraries unless `DECISIONS.md`, the sprint blueprint, and the dry run explicitly approve them.
- Do not add v1.0 non-goals such as sound, online multiplayer, mobile controls, settings, remappable controls, or global leaderboards.
- Do not self-authorize a higher permission level.

## 5. Dry Run Approval Rule

Develop Mode never touches implementation files without a dry run.

Every Develop Mode session starts at Permission Level 0.

The dry run must read the active sprint pack and produce `dry_run.md` with these seven sections:

1. Files to create.
2. Files to modify.
3. Files to move or delete.
4. Commands to run.
5. Dependencies requested.
6. Risks.
7. Ambiguities.

After writing `dry_run.md`, stop. Do not proceed.

Develop Mode may continue only after the human sends this exact authorization pattern:

```text
Dry run approved.
Permission Level [LEVEL] authorized.
Proceed according to requirements.md, blueprint.md, acceptance.md, and dry_run.md.
```

If the dry run requests a new dependency, `DECISIONS.md` must contain an accepted decision for that dependency before authorization proceeds.

## 6. Permission Levels

| Level | Name | Scope |
|---|---|---|
| 0 | Dry Run Only | Read the sprint pack and write `dry_run.md`. No implementation changes. |
| 1 | Approved Sprint Scope | Modify only files listed in both `blueprint.md` and `dry_run.md`. |
| 2 | Approved Expansion | Add minor helper files explicitly approved after the dry run. |
| 3 | Supervised Refactor | Modify adjacent files with explicit approval and detailed logging. |
| 4 | Migration / High-Risk Change | Make structural changes only with rollback plan and explicit approval. |

## 7. PongTest Project Rules

1. v1.0 uses vanilla JavaScript with the HTML5 Canvas API.
2. v1.0 must run by opening `index.html` locally in a desktop browser.
3. v1.0 must not require a server, build step, network access, Phaser.js, p5.js, npm, or a bundler.
4. Runtime implementation files for v1.0 are `index.html`, `styles.css`, and `game.js`.
5. Do not create runtime files before Develop Mode dry run approval.
6. Do not change v1.0 gameplay scope unless `docs/requirements.md` and `DECISIONS.md` are updated in Design Mode first.
7. Keep accepted non-goals out of implementation: online multiplayer, global leaderboards, mobile/touch controls, sound, music, visual themes, player names, fullscreen, pause/settings menus, remappable controls, multiple AI difficulty levels, timed matches, and sudden death.
8. Collision, scoring, game states, input behavior, and high-score persistence must trace back to `docs/requirements.md`.
9. Any ambiguity found during Develop Mode must be reported rather than silently resolved in code.

## 8. Safe-to-Load Files

Safe by default:

- Root Markdown files.
- `docs/`
- `research/`
- `planning/`
- Approved sprint packs.
- Approved implementation files listed in a dry run.

Never load files forbidden by `SECURITY.md`.

## 9. Session Opening Protocol

At the start of a session:

1. Declare the active mode.
2. Load `AGENTS.md`.
3. Load `STATE.md`.
4. Load `DOMAIN.md`.
5. Load `SECURITY.md`.
6. Load additional files relevant to the session goal.

For sprint work, also load:

- `docs/requirements.md`
- `DECISIONS.md`
- Active sprint `requirements.md`
- Active sprint `blueprint.md`
- Active sprint `acceptance.md`

## 10. Sprint Close Protocol

Before a sprint is marked complete:

1. In Design Mode, generate `retrospective.md` from the sprint artifacts.
2. In Design Mode, generate `human_review.md` from `acceptance.md`; leave verdicts and signature blank.
3. In Design Mode, update `STATE.md` to show that the sprint awaits human review.
4. The human verifies acceptance criteria and signs the review.

The model cannot self-approve a sprint.
