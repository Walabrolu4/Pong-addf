# AGENTS.md - `[YOUR PROJECT NAME]`

## 1. Session Contract

This file defines how AI sessions operate for `[YOUR PROJECT NAME]`. Replace bracketed placeholders with your project-specific rules, but keep the mode boundaries, dry run rule, permission levels, and authorization message intact.

## 2. Three Modes

### Research Mode

**Purpose:** Investigate and synthesize information before project memory or implementation changes are made.

**Allowed actions:**
- Read safe-to-load files.
- Search documentation, specifications, and approved external sources.
- Produce research notes, source summaries, tool comparisons, and open questions.
- Update research notes, `QUESTIONS.md`, and `RISKS.md` when new unknowns or risks are found.

**Forbidden actions:**
- Modify source code, implementation files, website files, scripts, or tests.
- Modify sprint plan files unless explicitly listed as Research Mode outputs for this project.
- Record architectural decisions.
- Produce final designs or implementation specifications.

**Reads from:** `[SAFE PROJECT FILES]`, `docs/`, `research/`, `planning/`.

**Writes to:** `research/`, `QUESTIONS.md`, `RISKS.md`.

**Must not write to:** Implementation files, sprint pack files, project decisions, release plans, or files outside the approved research scope.

### Design Mode

**Purpose:** Write the project memory. Convert research, intent, and human feedback into durable Markdown artifacts.

**Allowed actions:**
- Create and update project brain files.
- Create and update sprint packs: `requirements.md`, `blueprint.md`, and `acceptance.md`.
- Create release plans, feature briefs, retrospectives, handoff notes, and dry run reviews.
- Record decisions in `DECISIONS.md`.
- Update `STATE.md`.
- Create documentation Markdown files.

**Forbidden actions:**
- Write source code.
- Write or modify implementation files, website source, tool scripts, tests, or build files.
- Modify `implementation_log.md`; that file belongs to Develop Mode.

**Reads from:** Safe project files, research notes, project brain files, docs, planning files.

**Writes to:** Project brain files, `docs/`, `planning/`, `research/` summaries, prompts, examples, and starter content approved for `[YOUR PROJECT NAME]`.

**Must not write to:** Source code, scripts, generated build output, credentials, or files outside the approved design scope.

### Develop Mode

**Purpose:** Modify implementation files after dry run approval.

**Allowed actions:**
- At Permission Level 0: produce `dry_run.md` only.
- At Permission Level 1 or higher: modify only files approved in `blueprint.md` and `dry_run.md`.
- Update `implementation_log.md` with changes made.
- Write and run tests within the approved scope.
- Produce `handoff_summary.md` when needed.

**Forbidden actions:**
- Implement without a dry run at Permission Level 0 first.
- Modify files outside the approved blueprint and dry run.
- Escalate permission level without explicit human authorization.
- Invent project rules or constraints not present in the project brain.

**Reads from:** Safe project files, active sprint pack, approved dry run, relevant implementation files.

**Writes to:** `dry_run.md`, `implementation_log.md`, `handoff_summary.md`, approved implementation files, and approved tests.

**Must not write to:** Files outside the approved sprint scope, credentials, unrelated project brain files, or generated artifacts not named in the dry run.

## 3. Dry Run Approval Rule

Develop Mode never touches an implementation file without a dry run.

Every `dry_run.md` must list these seven content areas:

1. Files to create.
2. Files to modify.
3. Files to move or delete.
4. Commands to run.
5. Dependencies requested.
6. Risks.
7. Ambiguities.

Approval sequence:

1. Start every Develop Mode session at Permission Level 0.
2. Read the active sprint pack: `requirements.md`, `blueprint.md`, and `acceptance.md`.
3. Produce `dry_run.md` with the seven content areas above.
4. Stop. Do not proceed.
5. The human or Design Mode reviews the dry run against the sprint pack.
5a. If `dry_run.md` names any new dependency, a `DECISIONS.md` entry for that dependency is required before authorization proceeds.
6. The human sends the authorization message:

```text
Dry run approved.
Permission Level [LEVEL] authorized.
Proceed according to requirements.md, blueprint.md, acceptance.md, and dry_run.md.
```

7. Develop Mode proceeds only after receiving that authorization.

The model cannot self-authorize. If a higher permission level is needed, the model stops and reports the need. The human decides.

## 4. Permission Levels

| Level | Name | Scope |
|---|---|---|
| 0 | Dry Run Only | Read the sprint pack and write `dry_run.md`. No implementation changes. |
| 1 | Approved Sprint Scope | Modify only files listed in both `blueprint.md` and `dry_run.md`. |
| 2 | Approved Expansion | Add minor helper files explicitly approved after the dry run. |
| 3 | Supervised Refactor | Modify adjacent files with explicit approval and detailed logging. |
| 4 | Migration / High-Risk Change | Make structural changes only with a rollback plan and explicit approval. |

## 5. Safe-to-load Files

Always update this list for `[YOUR PROJECT NAME]` before using an AI tool.

Safe by default:

- `AGENTS.md`
- `DOMAIN.md`
- `STATE.md`
- `DECISIONS.md`
- `COMMANDS.md`
- `STYLE_GUIDE.md`
- `SECURITY.md`
- `QUESTIONS.md`
- `RISKS.md`
- `GIT_STRATEGY.md`
- `PROMPT_CHANGELOG.md`
- `[PATH/TO/FILE]`
- `[PATH/TO/DIRECTORY/]`
- `[PATH/TO/SPRINT_PACK/]`
- `[PATH/TO/DOCS/]`
- `[PATH/TO/RESEARCH/]`

Never load files listed in `SECURITY.md`.

## 6. Sprint Close Protocol

Before a sprint is marked complete, the following steps must happen in order. The AI performs steps 1–3 in Design Mode. The human performs step 4.

1. **Generate `retrospective.md`** — Enter Design Mode, load all sprint artifacts (`requirements.md`, `blueprint.md`, `acceptance.md`, `dry_run.md`, `implementation_log.md`), and produce `planning/sprints/sprint_[NUMBER]/retrospective.md`. Record what was planned, what was built, variances, and lessons learned.

2. **Generate `human_review.md`** — Still in Design Mode, read `acceptance.md` for this sprint and produce `planning/sprints/sprint_[NUMBER]/human_review.md` with one section per acceptance group, each containing a Pass/Fail/Partial verdict field and an issues field. Do not fill in verdicts. Do not fill in the approval signature. Stop.

3. **Update `STATE.md`** — Update the Active Sprint, Current Status, and Next Step fields to reflect sprint closure.

4. **Human review** — The human opens `acceptance.md`, works through each check directly, records verdicts in `human_review.md`, and signs the approval signature. Only the human can mark a sprint approved.

The model cannot self-approve a sprint. If a sprint is approved with conditions, the conditions must be resolved before the next sprint's Develop Mode begins.

---

## 7. Session Opening Protocol

1. Declare the active mode for `[YOUR PROJECT NAME]`.
2. Load `AGENTS.md`.
3. Load `STATE.md`.
4. Load `DOMAIN.md`.
5. Load additional safe-to-load files relevant to the session goal.

For sprint work, also load the active sprint pack: `requirements.md`, `blueprint.md`, and `acceptance.md`.

## 8. Mode Boundaries Summary

| Mode | Can read | Can write | Cannot write |
|---|---|---|---|
| Research Mode | Safe project files and approved sources | Research notes, `QUESTIONS.md`, `RISKS.md` | Code, sprint packs, decisions |
| Design Mode | Safe project files and research | Project brain files, docs, sprint packs, release and feature plans | Code, scripts, tests, implementation logs |
| Develop Mode | Safe files, sprint pack, approved dry run, approved implementation files | Approved implementation files, tests, `dry_run.md`, `implementation_log.md`, `handoff_summary.md` | Files outside scope, project brain files not approved for change |

---

`[YOUR PROJECT NAME]` - AGENTS.md - ADDF 3.5
