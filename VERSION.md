# VERSION.md - PongTest

## Current Version

| Field | Value |
|---|---|
| Product version | `0.1.0-planning` |
| Target release | `v1.0.0` |
| Lifecycle stage | Design |
| ADDF version | 3.5 |
| Last updated | 2026-06-06 |

## Version Meaning

`0.1.0-planning` means the project brain, research, decisions, and requirements exist, but the runtime game files have not yet been implemented.

`v1.0.0` should be used only after:

1. Sprint implementation is complete.
2. Acceptance criteria pass.
3. Human review is signed.
4. `index.html` runs locally without a server.
5. `CHANGELOG.md` is updated.

## Runtime Files Expected for v1.0.0

- `index.html`
- `styles.css`
- `game.js`

## Versioning Rules

| Change type | Version impact |
|---|---|
| Documentation or project brain only | Keep planning version unless release status changes. |
| First playable local game | Move toward `1.0.0` after acceptance. |
| Bug fix after `1.0.0` | Patch version, for example `1.0.1`. |
| New gameplay mode after `1.0.0` | Minor version, for example `1.1.0`. |
| Breaking scope or architecture change | Major version review required. |
