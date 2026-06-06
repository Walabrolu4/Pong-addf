# RISKS.md - `[YOUR PROJECT NAME]`

Record risks that could affect project correctness, safety, scope, or continuity. Update this file during Research Mode or Design Mode when new risks appear.

## Risk 001 - Terminology Drift

**Risk:** Project-specific terms are used inconsistently across files and AI sessions.  
**Severity:** Medium  
**Probability:** `[High / Medium / Low]`  
**Status:** `[Open / Mitigated / Closed]`  
**Mitigation:** Update `DOMAIN.md` terminology table. Run consistency audit before sprint close.

## Risk 002 - Secrets Exposure

**Risk:** A protected file is loaded into an AI session accidentally.  
**Severity:** High  
**Probability:** `[High / Medium / Low]`  
**Status:** `[Open / Mitigated / Closed]`  
**Mitigation:** Check `SECURITY.md` before every session. Keep `SECURITY.md` current.

## Risk 003 - Scope Creep

**Risk:** `[YOUR PROJECT NAME]` expands beyond the approved release, feature, or sprint scope before core behavior is stable.  
**Severity:** `[High / Medium / Low]`  
**Probability:** `[High / Medium / Low]`  
**Status:** `[Open / Mitigated / Closed]`  
**Mitigation:** Keep out-of-scope items in `DOMAIN.md`, release scope files, and sprint requirements. Convert major scope changes into decisions.
