# GIT_STRATEGY.md - PongTest

## 1. Branch Model

| Branch | Purpose | Rule |
|---|---|---|
| `main` | Stable reviewed project history | Only reviewed work lands here. |
| `dev` | Integration branch | Sprint branches merge here before release. |
| `docs/*` | Documentation and project brain work | Use for Design Mode documentation changes. |
| `sprint/NNN-*` | Approved sprint implementation | Use only after sprint pack and dry run approval. |
| `fix/NNN-*` | Focused approved fixes | Use for small corrections tied to a sprint or review. |

## 2. Branch Naming

| Type | Pattern | Example |
|---|---|---|
| Docs | `docs/short-name` | `docs/project-brain` |
| Sprint | `sprint/NNN-short-name` | `sprint/001-core-pong` |
| Fix | `fix/NNN-short-name` | `fix/001-collision-reset` |
| Release | `release/vN.N.N` | `release/v1.0.0` |

## 3. Commit Convention

Use Conventional Commits:

```text
type(scope): short description
```

| Type | Use |
|---|---|
| `docs` | Documentation, project brain, research, requirements, sprint packs. |
| `feat` | User-facing game feature. |
| `fix` | Bug fix. |
| `test` | Test additions or verification support. |
| `refactor` | Internal code change without behavior change. |
| `chore` | Maintenance. |
| `release` | Version and changelog release updates. |

Examples:

```text
docs(brain): generate project brain files
feat(game): add two-player paddle controls
fix(game): prevent ball sticking inside paddle
```

## 4. ADDF Gate Rules

1. Design Mode may update Markdown project memory.
2. Develop Mode starts at Permission Level 0.
3. Runtime files must not be created or modified until `dry_run.md` is approved.
4. Do not commit implementation that was produced outside approved sprint scope.
5. Do not merge a sprint until acceptance checks have been reviewed by the human.

## 5. PR Requirements

- [ ] Summary of change is present.
- [ ] Mode used is identified: Research Mode, Design Mode, or Develop Mode.
- [ ] Sprint or project brain reference is present.
- [ ] Relevant requirements or decisions are linked.
- [ ] Verification steps are listed.
- [ ] Scope boundaries are confirmed.
- [ ] No v1.0 non-goals were added.

## 6. Release Process

1. Confirm `docs/requirements.md` is current.
2. Confirm `DECISIONS.md` matches requirements.
3. Confirm all sprint acceptance criteria passed.
4. Confirm `human_review.md` is signed by the human.
5. Update `VERSION.md`.
6. Update `CHANGELOG.md`.
7. Verify local static file execution by opening `index.html`.
8. Merge reviewed release work to `main`.
9. Tag the release, for example `v1.0.0`.

## 7. Merge Strategy

1. Squash noisy sprint work when individual commits do not add review value.
2. Use merge commits for release branches when release history should remain visible.
3. Keep project brain changes reviewable as documentation changes.
4. Never use destructive git commands to discard user work without explicit instruction.

## 8. .gitignore Minimums

The repository should ignore:

- `.env`
- `.env.*`
- `*.env`
- `*.key`
- `*.pem`
- `secrets/`
- `node_modules/`
- `.DS_Store`
- `dist/`
- `build/`
- `*.log`

`node_modules/`, `dist/`, and `build/` are not expected for v1.0, but they remain ignored as a safety default.
