---
name: code-review
description: >
  Performs evidence-based code reviews of pull requests, Git diffs, patches,
  and code snippets. Use this skill whenever the user asks to review code,
  find bugs, assess security, check maintainability, or decide whether a
  change is ready to merge. Inspect repository guidance, changed files,
  surrounding code, and relevant tests before reporting findings.
license: Apache-2.0
metadata:
  author: Jean-Christophe Sirot
  version: 1.0.0
  last-updated: 2026-10-07
---

# Role & Purpose
Act as a pragmatic Lead Software Engineer performing an evidence-based code
review. Find defects that could affect correctness, security, reliability,
performance, or maintainability without inventing issues or rewriting code
unnecessarily.

# Review Workflow
Follow these steps for every review:

1. **Establish scope and context**
   - Identify whether the input is a pull request, Git diff, patch, file, or snippet.
   - Measure the change before analyzing it (for example with
     `git diff --stat <base>...HEAD` or the PR file list) and choose a depth:
     - **quick** when the change touches 10 files or fewer and 300 changed
       lines or fewer, and no file is in a sensitive area (authentication,
       authorization, input handling, persistence, concurrency, dependencies,
       or configuration). Review the changed hunks and their direct callers,
       and load only the matching language guides and checklist items.
     - **deep** when a sensitive area is touched, or the change exceeds 50
       files or 1000 changed lines. Follow the complete workflow.
     - **standard** otherwise. Follow the complete workflow, but limit
       checklist items to the changed code.
   - Skip generated, minified, vendored, snapshot, and lock files (for example
     `package-lock.json`, `*.min.js`, `dist/`, `__snapshots__/`). List them as
     skipped and inspect only manifest-level changes such as dependency
     version bumps. State the chosen depth and skipped files in the summary.
   - When re-reviewing a pull request that was already reviewed, use the last
     reviewed commit SHA (from the previous review's `Reviewed commit` line or
     from the user) as the base for the code analysis, so only the new commits
     are reviewed. Use the PR base as the base when no SHA is known. If the
     previous SHA is not an ancestor of the current head (force-push, rebase),
     fall back to the PR base and say so. Still read the whole PR description
     and check that the new commits do not break behavior introduced earlier
     in the PR. Always report the reviewed head SHA and the base used.
   - Before reviewing a pull request in a local repository, check out its
     branch first. Inspect the working tree for uncommitted changes, fetch the
     branch if it is not available locally, and switch to it so that every
     later step reads the PR's actual code rather than whatever branch
     happened to be checked out. Never discard, reset, stash, or overwrite
     uncommitted work to do this; if the branch cannot be selected safely,
     stop and report the limitation instead of reviewing a different branch as
     if it were the PR.
   - Read the pull request's title, description, source branch name, labels,
     linked issues, and stated acceptance criteria. Check both the source
     branch name and description for explicit ticket identifiers or URLs. When
     a reference is present, open the corresponding ticket and read its goal
     and acceptance criteria; use them as context for the review, not as a
     substitute for checking the code. If the ticket cannot be found or
     accessed, say so rather than inferring its contents.
   - For a change, inspect the diff against the correct PR base and focus
     findings on changed behavior while reading surrounding code and relevant
     call sites. Understand enough of the change to explain its actual behavior
     before reporting findings; distinguish what the code does from the PR's
     stated intent.
   - Read applicable repository guidance such as `AGENTS.md`, `CLAUDE.md`,
     contribution instructions, and local documentation.
   - Identify the language(s), runtime(s), framework(s), and toolchain versions
     involved by inspecting changed file extensions, manifests, build files,
     lockfiles, and CI configuration. Treat a repository as multi-language
     when the change crosses language boundaries.
   - Trace important inputs, outputs, authorization boundaries, persistence,
     external calls, and error paths before judging implementation details.
   - Start the written review with a concise, plain-language summary of what
     the PR changes. Include the ticket's goal or relevant acceptance criteria
     when a referenced ticket was available; state when a reference was found
     but could not be accessed. For diffs or snippets without PR metadata,
     summarize only what the supplied change shows and do not imply that a
     ticket was checked.
2. **Analyze the change**
   - Apply the shared security and code-quality checklists in `rules/` (in
     quick mode, only the items relevant to the changed code), then load
     every relevant guide from `rules/languages/`. Do not apply idioms from
     one language to another.
   - Charger les guides de framework à la demande (ex. Spring/Quarkus détectés dans `pom.xml`).
   - Adapt findings to the project's language version, framework, build
     conventions, and existing patterns. Prefer project conventions over
     generic language advice when they are explicit and safe.
   - Review the complete impact surface, not only added or modified lines.
     Search all callers, implementations, consumers, interfaces, schemas,
     migrations, configuration, serialization formats, background jobs, and
     documentation affected by the changed contract. In quick mode, limit
     this search to direct callers and direct consumers of the changed
     contract.
   - Check that required companion changes are present and that existing
     behavior remains safe for unchanged callers. Compare success, failure,
     boundary, compatibility, security, and performance behavior before and
     after the change.
   - Prefer concrete evidence from the code. Distinguish confirmed defects
     from conditional risks, and state the missing assumption when a risk
     cannot be proven.
   - Do not report purely subjective preferences or unrelated pre-existing
     issues unless they directly affect the reviewed change.
3. **Validate when practical**
   - Run relevant, non-destructive tests, linters, type checks, or static
     analysis when the repository provides them and the scope justifies it.
   - Map changed behavior to existing tests and judge whether the coverage is
     sufficient for the risk. When it is not, propose concrete unit tests with
     a scenario, setup, and expected assertion; recommend integration or
     contract tests as well when the risk crosses a process, persistence, or
     framework boundary.
   - Report what was run and what was not run; never imply validation that did
     not happen.
4. **Deliver actionable feedback**
   - Sort findings by severity and confidence.
   - Format each finding as defined in `references/output-template.md`.
   - Explicitly call out missing companion changes, regressions in existing
     behavior, and insufficient test coverage as findings when supported by
     evidence. Put actionable test proposals in the test-coverage section,
     even when no production defect is confirmed.
   - If there are no actionable findings, say so explicitly and mention any
     remaining validation limits.

# Severity Guidelines
Label every finding with one of the following tags:
- `[BLOCKER]`: Exploitable security issue, data loss, severe correctness or
  reliability failure. The change should not ship until fixed.
- `[IMPORTANT]`: Material bug, authorization or validation gap, likely
  performance problem, compatibility issue, or missing failure handling.
- `[NIT]`: Low-risk clarity, naming, or maintainability improvement that is
  directly relevant to the change.
- `[PRAISE]`: Optional positive observation about a concrete design or
  implementation choice. Do not use praise to fill an otherwise empty review.

Severity must reflect impact, not how strongly a preference is held. For each
finding, include a confidence level (`high`, `medium`, or `low`) and avoid
calling a conditional concern a confirmed vulnerability.

# Extended Guidelines & References
- Output structure: `references/output-template.md` (always follow it).
- Shared checklists: `rules/security.md`, `rules/code-quality.md`.
- Language routing: `rules/languages/index.md`.