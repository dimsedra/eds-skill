---
name: issue-it
description: User-invoked command (/issue-it) to convert a problem or discussion into a clean, human-centered issue.
disable-model-invocation: true
argument-hint: What problem or context do you want to turn into an issue?
---

# Issue It

`/issue-it` transforms problem discussions, bug reports, or architecture gaps into clean, human-centered tracking issues. The agent synthesizes context and posts or drafts an issue optimized for human comprehension.

---

## Core Posture: Human-Centered Design

Issues are written for humans to read, triage, and understand — not for AI agents to talk to themselves.

- **Human Legibility First:** Write in clear, everyday technical language. Avoid agent-centric jargon, internal prompt references, or machine-oriented dump formats.
- **Strict Prohibition on Code Blocks:** Never include fenced code blocks or code snippets in the issue body. Agents inspect code in the repository; issues track context and location pointers (`file:line`).
- **Problem-Focused Titles:** Titles must describe the failure condition or system gap, never generic actions or solution guesses.

---

## Triggers & Boundaries

### When to Invoke
- User wants to file an issue from the current conversation or code investigation.
- User asks to turn a bug, task, or architectural gap into a tracking issue.

### When NOT to Invoke
- User wants to write code or run tests (`/implement` or TDD).
- User wants to walk through existing code to build personal comprehension (`/comprehend`).
- The task is a minor single-line edit that requires no tracking.

---

## Execution Steps

### 1. Gather & Synthesize Context
Read the conversation history or targeted code files. Extract:
- High-level system context (the big picture).
- Localized problem mechanics (what breaks and why).
- File paths and line numbers (`path/to/file:L10-L20`).
- High-level fix direction (if discussed).

### 2. Format the Issue Structure
Structure the content using [ISSUE-FORMAT.md](ISSUE-FORMAT.md):
- **Title:** Problem-focused statement.
- **Big-Picture Context:** 1–2 digestible sentences framing the system area.
- **Localized Problem:** Clear explanation of the specific failure or gap.
- **Affected Locations:** File paths and symbol pointers only (no code blocks).
- **Fix Direction (Optional):** High-level strategic approach, avoiding code snippets or pseudo-code.

### 3. Review & Output
Present the drafted issue to the user for review. If configured to write directly to an issue tracker CLI (such as GitHub CLI `gh issue create`), confirm before publishing.

---

## Failure Modes of this Skill

- **Agent-Centric Drift:** Writing issue text tailored for LLM consumption (using prompt keywords, verbose machine logs, or internal subagent register). Fix: Frame explanations for human reader comprehension.
- **Code Block Bloat:** Pasting code snippets into the issue body. Fix: Use file:line pointers only. Code belongs in files, not in issue trackers.
- **Solution-First Titles:** Titling issues after proposed fixes instead of the underlying problem. Fix: State the exact failure condition in the title.
- **Big-Picture Omission:** Jumping straight to localized file details without setting 1–2 sentences of high-level context. Fix: Always provide big-picture context first.
- **Implementation Overspecification:** Writing concrete code implementations inside the fix direction section. Fix: Keep fix directions focused strictly on high-level strategy and boundaries.

---

## Disclosed Reference

- [ISSUE-FORMAT.md](ISSUE-FORMAT.md) — Detailed template structure and formatting rules for issues.
