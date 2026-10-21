# Git governance reference

Use this reference in both workflow modes (`large_feature` and `small_change`) whenever branch strategy, commit standards, branch safety checks, or PR creation rules apply.

## Permissions

Respect repository instructions and the host's tool and permission rules. Keep these actions distinct:

| Action | Required authorization |
| --- | --- |
| Modify implementation files | Implementation request, confirmed mode, and applicable phase approvals. |
| Create or switch a branch | Explicit approval for that branch operation; approving a proposed name in a plan is not enough. |
| Commit | Explicit authorization to commit the agreed changes. |
| Push | Explicit authorization for the target branch and remote. |
| Create or edit a PR, post replies, resolve threads, or update tickets | Explicit authorization covering the relevant external action and target. |

A user may authorize several actions or a bounded follow-up cycle together. Reuse that authorization while its scope remains valid; do not ask repeatedly for unchanged permissions. A plan approval, supplied ticket, PR creation approval alone, or reviewer comment does not implicitly grant the other permissions. When publication is not authorized, keep the changes local, describe what remains unpublished, and request the missing permission when needed.

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

## Branch safety protocol (before implementation writes)

Read-only exploration does not require a new branch. Before implementation writes, inspect the repository and existing work:

```bash
git rev-parse --is-inside-work-tree
git branch --show-current
git status --short
```

1. If the directory is not a Git repository, stop implementation writes and ask for the intended repository; do not initialize one automatically.
2. Identify the relevant remote and default branch from established repository context, its remote HEAD, or repository metadata through an available read-only tool. Do not assume the remote is `origin` or infer the default solely from `main`/`master`. If required information remains unknown or ambiguous, ask.
3. An empty branch name can indicate detached HEAD. Stop implementation writes and ask which existing or new branch to use; do not silently switch or create one.
4. If on `main`, `master`, or the repository default branch, stop implementation writes and ask using the actual branch name:
   > "You are currently on `<current-branch>`. I need a dedicated branch before making changes. May I create `<proposed-branch-name>`?"
   If the user declines, leave the workspace unchanged and offer read-only planning or an appropriate existing branch. Do not treat refusal as permission to implement on the default branch.
5. If a dedicated branch is active, verify that its purpose and existing work fit this task. If unrelated or unclear, ask before proceeding rather than mixing changes.
6. Inspect pre-existing changes before touching affected files. Preserve them; continue with unrelated dirty files left alone, but stop for guidance if they conflict with the task. Do not stash, reset, discard, switch branches, or stage unrelated changes without appropriate authorization. Avoid blanket staging such as `git add .`.

Only after explicit branch-creation approval, and after checking that existing changes can be preserved, create the agreed branch:

```bash
git switch -c <confirmed-branch-name>
```

Never implement directly on the default branch. Recheck Git state on resumption, after a branch/workspace change, and before committing or publishing, rather than before every file edit.

## PR creation policy

1. PR title must start with a Conventional Commit style prefix (`feat:`, `fix:`, `chore:`, etc.).
2. Check repository instructions and templates in `.github/`, the repository root, and `docs/`, including `PULL_REQUEST_TEMPLATE.md` / `pull_request_template.md` and template directories. If several apply and the repository does not select one, ask.
3. If a template exists, preserve its headings, sections, and comments. Answer every section; use `N/A` where appropriate rather than silently dropping it.
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

5. Ask the user to confirm the justification content before creating the PR: `Rationale` in the fallback, or the corresponding content in the repository template even if it has a different heading. Do not impose a conflicting heading on an existing template.
6. Only create the PR after explicit user confirmation. Reuse an approval that already covers the presented content. Verify repository, head and base branches, publication permissions, and absence of a duplicate PR; do not guess the target branch.
7. Distinguish implementation validation from PR publication. Report checks truthfully in the body, including failures and checks not run.

## PR feedback monitoring and follow-up

After a PR is created, or when resuming an existing PR, keep track of it while it remains open. Check for new feedback and required-check results whenever the workflow resumes, a review/check notification arrives, or the user asks for an update. Do not claim to monitor continuously between those opportunities.

Before each remote write, verify that the PR is still open and the action is authorized. If it is closed or merged, stop the follow-up cycle; do not reopen it or publish more changes without a new request.

For each new item, inspect the current diff and relevant code before deciding what to do. Consider review summaries, inline comments and unresolved threads, general PR comments, and required-check failures. Deduplicate repeated feedback and verify whether a comment is still relevant or has already been addressed.

Classify each item and follow through:

- **Actionable and within the agreed scope:** make the smallest correct change under the existing implementation authorization, add or update tests where appropriate, and run relevant checks. Commit and push only within the granted permissions; otherwise report the correction as local and unpublished.
- **Incorrect, stale, already resolved, or outside the agreed scope:** do not make a change just to satisfy the comment. Explain the evidence and rationale in a reply when appropriate.
- **Ambiguous, conflicting with requirements, or requiring a material scope or design change:** explain the trade-off and ask the user before changing direction.
- **Failed checks:** investigate the failure. Fix failures caused by the PR within scope; report unrelated or infrastructure failures without disguising them as passing.

Under the granted publication permissions, reply in each addressed review thread, not as an unrelated top-level comment, with what changed or why no change is warranted. Resolve a thread only after its concern is fully addressed: if it required a code change, that change must be verified and published to the PR, not merely present locally. When disagreeing or deferring, explain why and leave it open for reviewer confirmation.

Continue until there is no actionable feedback or failed required check left, the PR is merged/closed, or the user asks to stop. If blocked by permissions, unavailable validation, or external failures, report the blocker and pause rather than looping or claiming success.
