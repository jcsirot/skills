# Light workflow (small_change mode)

Use this reference only when the orchestrator classified the request as `small_change`.

This path is for simple fixes, localized refactors, and low-risk small enhancements. It deliberately avoids heavy 4-phase ceremony.

## Flow

1. Clarify quickly
   - Confirm the goal, affected area, and expected outcome in a short summary.
   - Ask only the minimum clarifying questions needed to avoid incorrect implementation.
2. Implement directly
   - Proceed with focused code changes.
   - Keep scope tight and avoid opportunistic unrelated refactors.
3. Validate and report
   - Run relevant checks/tests for impacted areas.
   - Share what changed and why.

## Guardrails

1. Always apply `references/git-governance.md` for branch safety, naming, commit style, and PR policy.
2. If scope expands or architectural uncertainty appears during execution, switch to `large_feature` mode and continue with `references/workflow-4-phases.md`.
3. Even in light mode, preserve code quality: clear logic, maintainability, and tests appropriate to the change.
