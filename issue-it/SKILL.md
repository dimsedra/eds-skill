---
name: issue-it
description: User-invoked command (/issue-it) to convert a problem or discussion into a clean, user-centered issue.
disable-model-invocation: true
argument-hint: What problem or context do you want to turn into an issue?
---

# Issue It

`/issue-it` transforms problem discussions, bug reports, or architecture gaps into clean, user-centered tracking issues. You synthesize context and post or draft an issue optimized for user comprehension.

---

## Core Posture: The "Cold-Me Six Weeks Later" Rule

An issue is written for the user reading it six weeks from now with zero active context.

- **Problem-First Titles:** State the exact failure condition or system gap in the title so that a skim of the issue list tells what's broken without opening the issue.
- **Big-Picture First:** Always start with 1–2 sentences of high-level system framing. A cold reader six weeks later needs mental re-orientation before diving into localized problem details.
- **Cognitive Load Slicing:** The user has limited working memory at any single point in time. Never pack multiple distinct domain problems or system layers into one overwhelming issue. If a problem spans multiple independent abstraction boundaries, slice it into separate, focused sub-issues that make abstract sense on their own.
- **No Code Blocks & Durable Pointers (Code-As-Context Trap):** Strictly no fenced code blocks. Code snippets are a trap: they feel like documentation, but become stale snapshots that fail to explain why something breaks. Use durable symbolic pointers (`path/to/file` -> `functionName()`, `ClassName.method()`) rather than brittle line numbers alone, because line numbers shift quickly as code moves. The repository holds the code; the issue holds the context and durable location pointers.
- **Strategic Fix Direction (Optional):** Focus strictly on high-level architectural direction and design intent. Never write code implementations or pseudo-code inside the issue body.

---

## Triggers & Boundaries

### When to Invoke
- User wants to file an issue from the current conversation or code investigation.
- User asks to turn a bug, task, or architectural gap into a tracking issue.

### When NOT to Invoke
- User wants to write code or run tests.
- User wants to walk through existing code to build personal comprehension (`/comprehend`).
- The task is a minor single-line edit that requires no tracking.

---

## Execution Steps

### 1. Gather & Synthesize Context
Read the conversation history or targeted code files. Extract:
- High-level system context (big picture for re-orientation).
- Localized problem mechanics (what breaks and why).
- File paths and durable symbol pointers (`path/to/file` -> `functionName()`).
- High-level fix direction (if discussed).
- Natural abstraction boundaries for slicing if the problem spans multiple distinct concerns.

### 2. Format the Issue Structure
Structure the content using [ISSUE-FORMAT.md](ISSUE-FORMAT.md):
- **Title:** Problem-focused statement.
- **Big-Picture Context:** 1–2 digestible sentences framing the system area.
- **Localized Problem:** Clear explanation of the specific failure or gap.
- **Affected Locations:** File paths and durable symbol pointers only (no code blocks).
- **Fix Direction (Optional):** High-level strategic approach, avoiding code snippets or pseudo-code.

### 3. Review & Output
Present the drafted issue (or sliced sub-issues) to the user for review. If configured to write directly to an issue tracker CLI (such as GitHub CLI `gh issue create`), confirm before publishing.

---

## Failure Modes of this Skill

- **Monolithic Packing:** Packing multiple distinct domain problems or architectural layers into a single issue, overloading user working memory. Fix: Apply Cognitive Load Slicing by splitting complex problems into independent, abstractly coherent sub-issues.
- **Agent-Centric Drift:** Writing issue text tailored for LLM consumption (using prompt keywords, verbose machine logs, or internal subagent register). Fix: Frame explanations for user reader comprehension six weeks later.
- **Code Block Bloat (Code-As-Context Trap):** Pasting code snippets into the issue body. Fix: Use durable file and symbol pointers only. Code belongs in files, not in issue trackers.
- **Solution-First Titles:** Titling issues after proposed fixes instead of the underlying problem. Fix: State the exact failure condition so it can be understood from an issue list skim.
- **Big-Picture Omission:** Jumping straight to localized file details without setting 1–2 sentences of high-level context. Fix: Always provide big-picture context first for cold re-orientation.
- **Implementation Overspecification:** Writing concrete code implementations inside the fix direction section. Fix: Keep fix directions focused strictly on high-level strategy and boundaries.

---

## Disclosed Reference

- [ISSUE-FORMAT.md](ISSUE-FORMAT.md): Detailed template structure and formatting rules for issues.
