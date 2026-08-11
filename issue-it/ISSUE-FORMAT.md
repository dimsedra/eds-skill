# ISSUE Format

Reference template for structuring human-centered GitHub issues produced by `/issue-it`.

---

## Structure Guidelines

### 1. Title
Problem-focused statement clearly describing the failure condition or system gap.
- **Correct:** Auth token expiration bypasses database check during high-load requests
- **Avoid:** Fix session token bug in session.ts

### 2. Big-Picture Context
1–2 concise sentences framing where this problem fits into the broader system architecture. Keep it digestible at a glance.

### 3. Localized Problem & Impact
Detailed explanation of the specific issue:
- What is breaking or missing.
- Why it manifests and under what conditions.
- Operational or system impact.

### 4. Affected Code Locations
List relevant file paths, function signatures, or line ranges.
- **Allowed:** `src/auth/session-store.ts:L42-L58`, `validateSessionToken()`
- **Strict Prohibition:** Do NOT include fenced code blocks or code snippets. The codebase holds the code; the issue holds the location pointers.

### 5. Fix Direction (Optional)
If a resolution approach is requested or discussed, outline high-level strategic direction and architectural approach:
- Focus on design intent, seams, and boundary changes.
- Do NOT write code implementations or pseudo-code snippets.

---

## Markdown Template

```markdown
## Context
[1-2 sentences explaining the high-level system context]

## Problem Description
[Clear explanation of the specific bug, gap, or failure condition]

## Affected Locations
- `path/to/file.ext:L10-L20` (`FunctionName`)

## Proposed Direction (Optional)
[High-level architectural approach or resolution strategy]
```
