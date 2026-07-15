# Git governance reference

Use this reference whenever the workflow needs branch strategy, commit standards, branch safety checks, or PR creation.

## Planning section (Phase 2)

1. **Golden rule:** `1 Feature = 1 PR`.
2. If the feature is too large for safe review, explicitly split it into sequential sub-features and multiple PRs.
3. Reuse the repository branch naming convention if documented. Otherwise, use:
   - `feat/<scope>-<short-description>`
   - `fix/<scope>-<short-description>`
   - `chore/<scope>-<short-description>`
   - `refactor/<scope>-<short-description>`
   - `docs/<scope>-<short-description>`
4. Keep branch names lowercase, kebab-case after the slash, concise, and aligned with intent.
5. If multiple PRs are needed, define one explicit branch name per PR.
6. Enforce Conventional Commits aligned with branch purpose:
   - `feat(scope): short summary`
   - `fix(scope): short summary`
   - `refactor(scope): short summary`
   - `test(scope): short summary`
   - `docs(scope): short summary`
   - `chore(scope): short summary`

## Branch safety protocol (Phase 4 precondition)

Before creating or modifying any file:

```bash
git branch --show-current
```

- If the branch is `main`, `master`, or the repository default branch, stop and ask:
  > "You are currently on `main`. I need to create a dedicated branch before making any changes. Shall I create `<proposed-branch-name>` now? (yes / no, or suggest another name)"
- Only proceed after user confirmation and branch creation:

  ```bash
  git checkout -b <confirmed-branch-name>
  ```

- If a dedicated branch is already active, continue.

Never implement directly on the default branch.

## PR creation policy

1. PR title must start with a Conventional Commit style prefix (`feat:`, `fix:`, `chore:`, etc.).
2. Check for a repository PR template before creating the PR.
3. If a template exists, use it.
4. If no template exists, use this fallback:

```markdown
## Rationale
<!-- Indicate the reason why this PR has been created. What problem does it solve, or what feature does it bring? -->
## Summary
<!-- List the changes done in this PR. Use bullet points for readability. -->
- change #1
- change #2
## Tests
<!-- List of acceptance tests to validate if the PR is ready to merge. -->
```

5. Ask the user to confirm the `Rationale` content before creating the PR.
6. Only create the PR after explicit user confirmation.
