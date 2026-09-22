# Review Output Template

Use this structure. Omit a section only when it genuinely does not apply, and
never invent a refactoring merely to populate the template.

## 🎯 Executive Summary
[Summarize the reviewed scope, overall readiness, and the main validation limit
in 1-2 sentences.]

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

## ✅ Validation
- **Checks run:** [Commands or inspections performed.]
- **Checks not run:** [Relevant checks that were unavailable or intentionally omitted.]

## ✨ Refactored Code
Include this section only when a small, concrete code example makes the fix
clear. Prefer a minimal patch over a full-file rewrite.

```[language]
// Minimal corrected example
```