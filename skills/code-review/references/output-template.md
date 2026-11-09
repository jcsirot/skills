# Review Output Template

Use this structure. Omit a section only when it genuinely does not apply, and
never invent a refactoring merely to populate the template.

## 📋 PR Summary
[Plain-language summary of the behavior the change introduces or modifies,
separating observed behavior from stated intent. Include ticket context as
required by Step 1 of SKILL.md. For non-PR inputs, summarize only the provided
change.]
- **Reviewed commit:** `<head-sha>` (base: `<base-sha or PR base>`; incremental
  from `<previous-sha>` when applicable). Include this line for every PR review.
- **Mode proportionné** (quick / standard / deep selon la taille du diff)

## 🎯 Executive Summary
[Summarize overall merge readiness and the main validation limit in 1-2
sentences; do not repeat the PR summary.]

## 🚨 Review Findings

### 🛑 Blockers
- None, or:
- **[BLOCKER] Issue title**
  - **Location:** `path/to/file.ext:42-45`
  - **Evidence:** Concrete behavior or code path proving the issue.
  - **Impact:** What can break, leak, or be exploited.
  - **Fix:** Minimal corrective change or implementation direction.
  - **Confidence:** `high`, `medium`, or `low`.

### ⚠️ Important Issues
- None, or use the same finding format with `[IMPORTANT]`.

### 💡 Suggestions & Nits
- None, or use the same finding format with `[NIT]`.

### ✨ Positive Findings
- Optional concrete observations using `[PRAISE]`.

## 💬 Existing PR Discussions
[For PRs, link relevant review threads or discussions and summarize which
concerns remain actionable, are addressed or stale, or cannot be determined.
Reference findings above for supported outstanding issues and their proposed
corrections. State if discussion history could not be fully accessed. Omit for
inputs without PR discussion.]

## 🔐 Security Review
- **Controls reviewed:** [Applicable areas from `rules/security.md`: inputs/injection, authentication/session, authorization/abuse, secrets/cryptography, errors/logging, and dependencies/configuration. If no security-relevant behavior changed, say so rather than implying every control was verified.]
- **Assessment:** [No actionable security findings, or reference the relevant findings above. State material assumptions or controls that could not be verified; do not repeat finding details or claim unchecked controls passed.]

## 🧪 Test Coverage
- **Existing coverage:** [Tests that exercise the changed and affected behavior.]
- **Gaps:** [Missing or insufficient scenarios, or `None identified`.]
- **Proposed unit tests:** [Specific test names/scenarios and expected assertions.
  Omit when coverage is sufficient.]

## ✅ Validation
- **Checks run:** [Commands or inspections performed.]
- **Checks not run:** [Relevant checks that were unavailable or intentionally omitted.]

## ✨ Refactored Code
Include this section only when a small, concrete code example makes the fix
clear. Prefer a minimal patch over a full-file rewrite.

```[language]
// Minimal corrected example
```