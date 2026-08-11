# ISSUE Format

Reference template for structuring human-centered GitHub issues produced by `/issue-it`.

---

## Core Mental Model: The "Cold-Me Six Weeks Later" Rule

Every section in an issue exists for a specific cognitive reason — serving a human reading it six weeks later with zero active memory of the conversation.

---

## Structure Guidelines

### 1. Title (Problem-First)
*Rationale: A title skimmed in an issue list six weeks from now must immediately tell you what is wrong without forcing you to open the issue to reconstruct the moment.*
- State the exact failure condition or system gap.
- **Correct:** Auth token expiration bypasses database check during high-load requests
- **Avoid:** Fix session token bug in session.ts

### 2. Big-Picture Context (Re-Orientation First)
*Rationale: A cold reader six weeks later needs high-level system re-orientation before localized details make sense.*
- 1–2 concise sentences framing where this problem fits in the broader system architecture.
- Keep it digestible at a glance.

### 3. Localized Problem & Impact
*Rationale: Explains why the system fails and what impact it causes.*
- What is breaking or missing.
- Why it manifests and under what conditions.
- Operational or system impact.

### 4. Affected Code Locations (Pointers, Not Code)
*Rationale: Code-as-context is a trap. Code snippets feel like documentation, but become stale snapshots that do not explain why by themselves. The repository holds the code; the issue holds location pointers.*
- List relevant file paths, function signatures, or line ranges.
- **Allowed:** `src/auth/session-store.ts:L42-L58`, `validateSessionToken()`
- **Strict Prohibition:** Do NOT include fenced code blocks or code snippets.

### 5. Fix Direction (Strategy, Not Implementation - Optional)
*Rationale: Focuses on architectural direction and design intent, leaving code implementation to the pull request.*
- Outline high-level strategic direction and architectural approach.
- Focus on design intent, seams, and boundary changes.
- Do NOT write code implementations, pseudo-code, or patch snippets.

---

## Markdown Template

```markdown
## Context
[1-2 sentences framing high-level system context for cold re-orientation]

## Problem Description
[Clear explanation of the specific failure condition and why it manifests]

## Affected Locations
- `path/to/file.ext:L10-L20` (`FunctionName`)

## Proposed Direction (Optional)
[High-level architectural approach or resolution strategy]
```
