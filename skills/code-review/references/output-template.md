# Review Output Template

Use this structure. Omit a section only when it genuinely does not apply, and
never invent a refactoring merely to populate the template.

## 📋 PR Summary
[Explain in plain language what the PR changes and the behavior it introduces
or modifies. Distinguish the observed change from the stated intent. State
whether a ticket reference was found in the source branch name or PR
description; summarize its relevant goal or acceptance criteria if accessible,
or state if it could not be accessed. For non-PR inputs, summarize only the
provided change.]

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