# Light workflow (small_change mode)

Use this reference after the user has confirmed `small_change` through `SKILL.md`.

This path is for simple fixes, localized refactors, and low-risk small enhancements. It deliberately avoids heavy 4-phase ceremony.

## Flow

1. Clarify quickly
   - Reuse the initial reconnaissance and source collection. Consult supplied documents or tickets only as needed for this change; do not ask for them again.
   - State the goal, affected area, and an observable expected outcome in a short summary.
   - Ask only the minimum clarifying questions needed to avoid incorrect implementation.
   - Do not add another routine approval gate when the mode and requirements are already clear and confirmed.
2. Implement directly
   - After the Git safety checks, proceed with focused code changes using existing project patterns.
   - Keep scope tight and avoid opportunistic unrelated refactors.
3. Validate and report
   - Use the smallest relevant checks for the expected outcome. Add or update automated tests for behavior changes where appropriate; use documented manual or documentation checks when automation is not suitable.
   - Distinguish passing, failing, and unexecuted checks. Explain unavailable tools or infrastructure without presenting them as success.
   - Report what changed and why, relevant validation evidence, and remaining limitations or blockers. Do not call the work complete while a mandatory acceptance criterion is unverified.

## Guardrails

1. Always apply `references/git-governance.md` for branch safety, naming, commit style, and PR policy.
2. If scope expands or architectural uncertainty appears, pause implementation and explain what changed. Request confirmation of `large_feature` using the mode-approval gate in `SKILL.md`; do not switch silently. Once confirmed, use `references/workflow-4-phases.md`, carrying forward still-valid approved work and completing any missing phases. Do not discard existing changes or repeat approved work just to satisfy the phase sequence.
3. Even in light mode, preserve code quality: clear logic, maintainability, and tests appropriate to the change.
4. Supplied references do not authorize ticket updates, commits, pushes, or PR publication.
