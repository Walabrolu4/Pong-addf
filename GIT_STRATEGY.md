# GIT_STRATEGY.md - `[YOUR PROJECT NAME]`

## 1. Branch Model

| Branch | Purpose | Rule |
|---|---|---|
| `main` | Stable release history | Only reviewed release work lands here. |
| `dev` | Integration branch | Sprint branches merge here before release. |
| `sprint/NNN-*` | Sprint work | Use for approved sprint implementation. |
| `fix/NNN-*` | Focused fixes | Use for small approved corrections. |

## 2. Branch Naming

| Type | Pattern | Example |
|---|---|---|
| Sprint | `sprint/NNN-short-name` | `sprint/001-project-brain` |
| Fix | `fix/NNN-short-name` | `fix/001-state-update` |
| Docs | `docs/short-name` | `docs/start-here` |
| Release | `release/vN.N` | `release/v0.1` |

## 3. Commit Convention

Use Conventional Commits:

```text
type(scope): short description
```

| Type | Use |
|---|---|
| `feat` | User-facing or framework feature |
| `fix` | Bug fix or correction |
| `docs` | Documentation-only change |
| `chore` | Maintenance change |
| `refactor` | Internal restructuring without behavior change |
| `test` | Test additions or updates |
| `release` | Release preparation |

## 4. PR Requirements

- [ ] Summary of change is present.
- [ ] Sprint or issue reference is present.
- [ ] Acceptance criteria are linked.
- [ ] Tests or verification steps are listed.
- [ ] Framework concepts changed: Yes/No.

## 5. Release Process

1. Create release branch - `[YOUR STEP DETAIL]`
2. Update version file - `[YOUR STEP DETAIL]`
3. Update changelog - `[YOUR STEP DETAIL]`
4. Run consistency audit - `[YOUR STEP DETAIL]`
5. Verify acceptance criteria - `[YOUR STEP DETAIL]`
6. Merge to `main` - `[YOUR STEP DETAIL]`
7. Tag release - `[YOUR STEP DETAIL]`
8. Publish release notes - `[YOUR STEP DETAIL]`

## 6. Merge Strategy

1. Squash noisy sprint work when individual commits do not add review value.
2. Use merge commits for release branches so release history remains visible.
3. Do not merge unreviewed Develop Mode output into `main`.

## 7. .gitignore Minimums

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
