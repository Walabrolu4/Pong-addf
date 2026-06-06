# Audit: ADDF_Tutorial_Pong_Game.md
### Audited Against: Autonomous-Duck-Development-Framework (ADDF v3.5)

**Audit Date:** 2026-06-05  
**Files Reviewed:**  
- `PongTest/starter-kit-blank-v0.1/todos/ADDF_Tutorial_Pong_Game.md`  
- `Autonomous-Duck-Development-Framework/AGENTS.md`  
- `starter-kit/blank/AGENTS.md` (the template students receive)  
- `starter-kit/blank/PROMPTS.md`  
- `docs/sprint-loop.md`  
- `docs/project-brain.md`  
- `docs/permission-levels.md`  
- `docs/lifecycle/index.md`  
- `docs/glossary.md`  
- `docs/initial-setup.md`  
- `docs/file-reference.md`  
- `PongTest/starter-kit-blank-v0.1/` (the actual kit students open)  

**Note:** The tutorial file in the ADDF main repo (`Autonomous-Duck-Development-Framework/todos/`) is byte-for-byte identical to the one in PongTest. Both are the same document.

---

## Overall Assessment

The tutorial is **well-structured and pedagogically sound**. The core ADDF concepts — three modes, permission levels, dry run gate, sprint loop, human as decision-maker — are all correctly represented and well-explained. The Pong project is an excellent choice for teaching the framework.

However, there are **several specific inaccuracies and gaps** where the tutorial drifts from the current framework spec. Some are naming mismatches, some are structural gaps, and one is a significant missing resource (PROMPTS.md). None of them break the teaching experience, but they should be corrected before students run into confusion.

---

## FINDINGS

---

### ISSUE 1 — BLOCKER: PROMPTS.md is never mentioned

**Where:** Entire tutorial  
**Framework source:** `starter-kit/blank/PROMPTS.md`

The starter kit that students open already contains a `PROMPTS.md` file with 10 ready-to-use prompts covering every major ADDF operation: Research Mode, Design Mode, sprint pack generation, dry run, authorization, consistency audit, sprint close, and handoff. This is one of the most valuable resources in the starter kit.

The tutorial never mentions it exists. Instead, Appendix B provides its own custom prompt templates. Students will be working with a file that overlaps Appendix B without knowing it.

**Required fix:** Add a note early in the tutorial (ideally in the Introduction or Phase 0 setup) that says:

> "Your starter kit includes `PROMPTS.md` — a ready-to-use prompt reference for every ADDF operation. Appendix B in this tutorial contains adapted versions for the Pong project. Both are useful; `PROMPTS.md` is your general-purpose reference for future projects."

---

### ISSUE 2 — CORRECTION: Sprint 001 brain file list includes wrong and missing files

**Where:** Section 4, Sprint 001, Step 1 — the brain generation prompt

The tutorial asks students to generate these brain files:

```
AGENTS.md, DOMAIN.md, COMMANDS.md, QUESTIONS.md, RISKS.md,
STYLE_GUIDE.md, GIT_STRATEGY.md, START_HERE.md, VERSION.md, CHANGELOG.md
```

**Problems:**

1. `VERSION.md` — **not in the starter kit template** and not listed in `docs/project-brain.md` as a standard brain file. The ADDF main repo has a VERSION.md for the framework itself, but it is not part of the standard project brain. Generating it will create a file with no defined template or purpose for students.

2. `CHANGELOG.md` — **not in the starter kit template**. The correct file is `PROMPT_CHANGELOG.md`, which tracks changes to AI prompts used in the project. CHANGELOG.md exists in the ADDF main repo as a framework version history, not as a student project brain file.

3. `PROMPTS.md` — **missing from the list**. The starter kit template includes `PROMPTS.md` and students already have it. The brain generation step should instruct the AI to populate it (or at minimum acknowledge it exists and explain it doesn't need to be generated because it came with the starter kit).

**The canonical project brain file list** (from `docs/project-brain.md`):

```
AGENTS.md, DOMAIN.md, STATE.md, DECISIONS.md, COMMANDS.md,
STYLE_GUIDE.md, SECURITY.md, QUESTIONS.md, RISKS.md,
GIT_STRATEGY.md, PROMPT_CHANGELOG.md
```

**Required fix:** Remove `VERSION.md` and `CHANGELOG.md` from the Sprint 001 brain generation prompt. Replace `CHANGELOG.md` with `PROMPT_CHANGELOG.md`. Add a line about `PROMPTS.md` already existing in the starter kit.

---

### ISSUE 3 — CORRECTION: Sprint planning structure uses v1.0 but starter kit has v0.1

**Where:** Section 4, Sprint 001, Step 2 — planning structure prompt

The tutorial asks students to generate:
```
planning/releases/v1.0/release_plan.md
planning/releases/v1.0/scope.md
```

But the PongTest starter kit already contains:
```
planning/releases/v0.1/release_notes.md
planning/releases/v0.1/release_plan.md
planning/releases/v0.1/retrospective.md
planning/releases/v0.1/scope.md
```

The pre-existing `v0.1` folder conflicts with generating a new `v1.0` folder. Students will either create a duplicate release folder or be confused about which to use.

**Required fix:** Either instruct students to delete/ignore the pre-existing v0.1 folder and replace it with v1.0 (which is what the tutorial expects), or update the tutorial to use v0.1 as the release target (which aligns with the starter kit). The v0.1 naming in the starter kit is a generic placeholder — it should probably be updated to v1.0 for the Pong project before the tutorial begins.

---

### ISSUE 4 — GAP: blueprint_feedback.md and rollback_log.md are never explained

**Where:** All sprint sections  
**Framework source:** `PongTest/starter-kit-blank-v0.1/planning/sprints/sprint_001/`

The starter kit includes two sprint files the tutorial never mentions:

**`blueprint_feedback.md`** — This is the artifact for the Sprint Loop's "Human blueprint review" step (Step 3 in the official 11-step Sprint Loop). It's where the human records their review of the blueprint before Develop Mode opens. The tutorial describes blueprint review as part of "review the blueprint for:" bullets in each sprint section, but never tells students to fill in this file.

**`rollback_log.md`** — This is a sprint close artifact (listed in `docs/project-brain.md` under sprint files). The tutorial never mentions it. For a beginner game project, rollbacks are rare, but students should know the file exists and when to use it (if they need to undo implementation work).

**Required fix:**  
- In each sprint's "review the blueprint" step, add a line instructing students to fill in `blueprint_feedback.md`.  
- In each sprint close section, add a one-line note: "If any implementation work was rolled back, fill in `rollback_log.md`. Otherwise leave it blank."

---

### ISSUE 5 — GAP: Sprint Close Protocol is incomplete

**Where:** Sprint 001 Step 4, Sprint 002 Step 6, Sprint 003 Step 4  
**Framework source:** `starter-kit/blank/AGENTS.md`, Section 6 — Sprint Close Protocol

The AGENTS.md in the starter kit defines a formal Sprint Close Protocol where the AI generates `human_review.md` as a blank template (with verdict fields the human fills in), before the human touches it. The protocol is:

1. Design Mode generates `retrospective.md`  
2. Design Mode generates `human_review.md` (blank template, verdict fields unfilled)  
3. AI updates `STATE.md`  
4. Human opens `human_review.md`, runs acceptance checks, fills in verdicts, signs off  

The tutorial says "Fill in `planning/sprints/sprint_001/human_review.md` yourself" without the prior step of Design Mode generating the blank template. Students will either create the file from scratch (not knowing the expected format) or skip it.

**Required fix:** Add a Design Mode prompt step before "Fill in human_review.md yourself" that generates the blank template:

```
You are operating in Design Mode.

Generate planning/sprints/sprint_001/human_review.md.

Read acceptance.md for this sprint. Produce one section per
acceptance group, each with a Pass/Fail/Partial verdict field
and an issues field. Do not fill in verdicts. Do not fill in
the approval signature. Stop.
```

Then instruct students to fill it in after the AI stops.

---

### ISSUE 6 — SIMPLIFICATION: The Sprint Loop is compressed

**Where:** Entire tutorial  
**Framework source:** `docs/sprint-loop.md`

The official ADDF Sprint Loop has 11 steps. The tutorial compresses this for readability, which is appropriate for a beginner course. However, two compressed steps are worth naming explicitly because students will encounter them in real projects:

**Missing: Step 6 — Dependency Approval Gate**  
When a dry run requests an external dependency (e.g., a CDN link for Phaser.js or p5.js), the framework requires a DECISIONS.md entry before implementation proceeds. The tutorial handles technology decisions in Phase 0-B, which mostly covers this — but if a student's dry run surfaces a CDN dependency that wasn't in DECISIONS.md, the tutorial doesn't tell them to pause and record it. This is a real scenario for students who choose Phaser or p5.js.

**Missing: Step 9 — Design Review of Output**  
After implementation, the Sprint Loop includes a Design Mode review of the implementation against the sprint pack. The tutorial goes directly from implementation to playtest without a Design Mode review step. For a code project where the AI generated the game code, this review is valuable.

**Required fix:** These don't need to become full tutorial steps, but a teacher note is appropriate:

> "The ADDF Sprint Loop has two additional steps we've simplified here. If a student's dry run requests a new CDN dependency that isn't in DECISIONS.md, pause and add a DECISIONS.md entry before authorizing. After implementation, you can optionally run a Design Mode review of the output against the sprint pack before the playtest."

---

### ISSUE 7 — OUTDATED REFERENCE: "ADDF Public Project tutorial"

**Where:** Introduction, Section 1 (Quick Reference), Phase 0-A Exercise  
**Framework source:** Not found in any ADDF framework file

The tutorial repeatedly references a "ADDF Public Project tutorial" and "Lessons 1 and 2 from the main tutorial" as prerequisites. No such tutorial exists in the current ADDF framework. The framework has documentation pages (`docs/getting-started.md`, `docs/initial-setup.md`, etc.) but no structured lesson-based tutorial.

This reference will confuse teachers who look for it.

**Required fix:** Either link to the specific ADDF documentation pages that cover the prerequisite material, or update the prerequisite to say:

> "Students should have read the ADDF framework documentation — specifically `getting-started.md` and the modes documentation — before this tutorial begins. Alternatively, begin this tutorial from scratch and use Section 1 (Quick Reference) as the foundation session."

---

### ISSUE 8 — MINOR: The "full 8-step lifecycle" claim is unmapped

**Where:** Introduction ("It covers the full 8-step lifecycle from the beginning")  
**Framework source:** `docs/lifecycle/index.md`

The ADDF 8-step lifecycle has specific names:
1. Research
2. Design & Feasibility
3. Validation Gate
4. Architecture
5. Sprint Planning
6. Build & Test
7. Review & Reflection
8. Deploy, Maintain, or Resume

The tutorial covers all of these (Phase 0-A = Step 1, Phase 0-B = Steps 2–4, Sprint 001 = Step 5, Sprint 002–003 = Steps 6–7, Section 7 = Step 8). But it never names the 8 steps, so a student who has read the framework docs won't know how the tutorial maps to the lifecycle they learned.

**Recommended fix:** Add a small mapping table to the Introduction:

```
Phase 0-A: Research                → Lifecycle Steps 1 (Research)
Phase 0-B: Design & Requirements   → Steps 2–3 (Design & Feasibility, Validation Gate)
Sprint 001: Project Brain          → Step 4 (Architecture)
Sprint 002–003: Build              → Steps 5–6 (Sprint Planning, Build & Test)
Closing reflection                 → Steps 7–8 (Review & Reflection, Deploy)
```

---

### ISSUE 9 — MINOR: Dry run content areas omit "files to move or delete"

**Where:** Sprint 002 Step 2 (dry run prompt), Appendix B (Develop Mode — Code Dry Run template)  
**Framework source:** `starter-kit/blank/AGENTS.md`, Section 3

The canonical 7 content areas for `dry_run.md` are:
1. Files to create
2. Files to modify
3. **Files to move or delete** ← missing from the tutorial's dry run prompts
4. Commands to run
5. Dependencies requested
6. Risks
7. Ambiguities

The tutorial's dry run prompt replaces item 3 with game-specific sections (game loop description, collision detection approach, input handling approach) — which are valuable additions. But item 3 is quietly dropped from both the main prompt and the Appendix B template.

For new projects this rarely matters (nothing to move or delete), but students who use the tutorial as their ADDF dry run reference for future projects will have a gap in their understanding of what a dry run must contain.

**Required fix:** Add "3. Files to move or delete — none expected for this sprint" to the dry run prompt. This reinforces the 7-area structure without adding overhead, since the answer will always be "none" for Sprint 002.

---

### ISSUE 10 — MINOR: Authorization format in Sprint 002 Step 4 is embedded in the prompt

**Where:** Sprint 002, Step 4 — Develop Mode Level 1  
**Framework source:** `docs/sprint-loop.md`, Step 7

The framework's authorization message is a separate, human-sent message with a specific format:

```
Dry run approved.
Permission Level [LEVEL] authorized.
Proceed according to requirements.md, blueprint.md, acceptance.md, and dry_run.md.
```

The tutorial's Sprint 002 Step 4 prompt embeds "Permission Level: 1 — Approved Sprint Scope" inside the main implementation prompt, as if it's a field the AI reads. This conflates the authorization message with the implementation prompt.

The correct flow is: (a) student writes `dry_run_review.md` marking the dry run as approved, then (b) student sends the short authorization message separately. The tutorial's Appendix B shows the correct authorization message format, but the main body doesn't match it.

**Required fix:** In Sprint 002 Step 4, split the prompt into two parts. First, the student sends:
```
Dry run approved.
Permission Level 1 authorized.
Proceed according to requirements.md, blueprint.md, acceptance.md, and dry_run.md.
```
Then the implementation prompt follows as the AI's instruction set. Or, add a teacher note explaining that the Appendix B authorization format is the one to use for future projects.

---

## WHAT WORKS WELL

These elements of the tutorial are correct, current, and pedagogically strong:

- **Mode names are exact and consistent throughout.** Research Mode, Design Mode, Develop Mode — correctly capitalized, never abbreviated, never mixed with old names (Architect Mode, Builder Mode).

- **Permission levels 0–4 are correct.** The table in Section 1 matches the framework exactly.

- **The dry run gate is correctly framed.** The tutorial's explanation — "the model describes the architecture before writing a single line of code, and you decide whether it makes sense" — is one of the clearest explanations of the dry run concept in any ADDF material.

- **"The model cannot self-authorize"** is present and emphasized. This is one of the most important rules in ADDF and the tutorial states it clearly.

- **The consistency audit step (Sprint 001, Step 3) is excellent.** Checking brain files against requirements and DECISIONS.md immediately after generation is exactly the right workflow and maps directly to the framework's Design Mode audit prompts.

- **The sprint close artifacts are mostly correct.** implementation_log.md, retrospective.md, STATE.md update, and git commit are all present and in the right order.

- **SECURITY.md is seeded before anything else.** The tutorial creates SECURITY.md before the first AI session, which matches the framework rule: "Fill SECURITY.md before loading files into an AI session."

- **The "One Risk I Am Watching" field is a strong teaching addition.** Not in the canonical framework artifacts but directly reinforces the risk assessment skill. Keep it.

- **The scoped bug fix pattern in Sprint 002 Step 5 is correct.** "Fix only [specific component]. Do not change any other behaviour. Log the change in implementation_log.md." This is exactly how the framework expects targeted corrections to work.

- **The Sprint 003 exercise** (distinguishing bugs from requirements gaps) teaches one of the most important real-world skills in ADDF. This is excellent material that doesn't appear in the framework docs — it's original to this tutorial and should stay.

- **The "Framework Viability Question" in Section 7** is excellent for closing reflection and maps directly to ADDF's stated purposes (resumability, decision record, dry run gate, acceptance criteria discipline).

---

## PRIORITY SUMMARY

| # | Issue | Severity | Action |
|---|---|---|---|
| 1 | PROMPTS.md never mentioned | High | Add reference in setup section |
| 2 | VERSION.md and CHANGELOG.md in brain list; PROMPT_CHANGELOG.md missing | High | Correct the file list |
| 3 | v1.0 vs v0.1 release folder conflict | High | Align naming with starter kit or update starter kit |
| 4 | blueprint_feedback.md and rollback_log.md unexplained | Medium | Add usage notes per sprint |
| 5 | Sprint Close Protocol missing AI generation of human_review.md | Medium | Add Design Mode step before human review |
| 6 | Dependency approval gate and Design review of output missing | Low | Add teacher notes |
| 7 | "ADDF Public Project tutorial" reference doesn't exist | High | Update prerequisites to point to real docs |
| 8 | 8-step lifecycle claim unmapped | Low | Add mapping table to introduction |
| 9 | Dry run missing "files to move or delete" | Low | Add it as "none expected" |
| 10 | Authorization format embedded in implementation prompt | Low | Split into separate authorization message |

---

*Audit complete. Quack.*
