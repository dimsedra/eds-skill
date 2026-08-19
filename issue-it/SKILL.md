---
name: issue-it
description: User-invoked command (/issue-it) to convert a problem or discussion into a clean, user-centered issue.
disable-model-invocation: true
argument-hint: What problem or context do you want to turn into an issue?
---

# Issue It

`/issue-it` transforms problem discussions, bug reports, or architectural gaps into clean, user-centered tracking issues. You synthesize context, isolate distinct problem boundaries, and draft or post an issue optimized for user comprehension.

---

## 1. Target Resolution

When the user invokes `/issue-it`:
- **Explicit Argument Provided** (e.g. `/issue-it memory leak in worker thread` or `/issue-it src/auth/token.ts`): Target that specific problem, file, or architectural component.
- **Active Chat Context / Diff**: If invoked without arguments after debugging, brainstorming, or reviewing changes, synthesize the problem directly from the active conversation context or recent diff.
- **Ambiguous Prompt**: If the problem or scope is unclear, ask the user in one short sentence to clarify what failure condition or gap to capture.

---

## 2. Core Posture

- **Cold-Me Six Weeks Later**: Write for the user reading the issue weeks later with zero active context. Titles must state the exact failure condition (not the proposed fix), and every issue opens with 1–2 sentences of high-level system context before localized details.
- **Semantic Code Anchoring**: Strictly no fenced code blocks or brittle raw line numbers. Anchor locations to durable symbolic pointers (`path/to/file` -> `functionName()`, `ClassName.method()`) so references remain valid as code evolves.
- **Cognitive Slicing**: Protect user working memory. If a problem spans multiple independent system layers or distinct concerns, slice it into separate, coherent sub-issues rather than packing a monolithic issue.

---

## 3. Execution Lifecycle (Phase Gates)

Every `/issue-it` execution follows 3 deterministic phase gates:

### Gate 1: Target Resolution & Context Slicing
- Resolve the target scope from user input or active chat context.
- Assess exploration scope:
  - **Inline Execution**: Synthesize directly in the main chat if the issue derives from the immediate conversation or 1–2 familiar files.
  - **Research Subagent**: Dispatch a `research` subagent if 3+ unfamiliar files or noisy codebase exploration is required, keeping main chat context clean.
- Evaluate problem scope: if multiple distinct abstraction layers or failure modes exist, slice into separate sub-issues.

### Gate 2: Issue Draft Generation
- Format each issue according to [ISSUE-FORMAT.md](ISSUE-FORMAT.md):
  1. **Problem-First Title**: Exact failure condition or gap.
  2. **Big-Picture Context**: 1–2 high-level framing sentences for cold re-orientation.
  3. **Localized Problem**: Specific failure mechanics and conditions.
  4. **Affected Locations**: File paths and durable symbol pointers (no code blocks).
  5. **Fix Direction (Optional)**: High-level architectural strategy only; no code snippets or pseudo-code.

### Gate 3: User Confirmation & Tracker Publishing
- Present the drafted issue (or sliced sub-issues) clearly in the chat for user review.
- Provide the optional GitHub CLI (`gh issue create`) command from [ISSUE-FORMAT.md](ISSUE-FORMAT.md).
- If configured to publish directly to GitHub or an issue tracker CLI, ask for explicit user confirmation before creating the issue.

---

## 4. Failure Modes

- **Solution-First Titles**: Titling issues with proposed fixes instead of failure conditions. Fix: State what breaks or is missing so the problem is obvious from an issue list skim.
- **Big-Picture Omission**: Jumping straight into localized details without high-level system framing. Fix: Always provide 1–2 opening context sentences for cold re-orientation.
- **Code-As-Context Trap**: Dumping code snippets or raw line numbers into the issue body. Fix: Use durable file paths and symbol names only.
- **Monolithic Packing**: Merging multiple distinct domain problems into one issue. Fix: Apply Cognitive Slicing to produce independent, focused sub-issues.
- **Implementation Overspecification**: Writing concrete code patches in the fix direction. Fix: Restrict fix direction to architectural strategy and boundaries.
- **Unconfirmed Tracker Publishing**: Creating tracking issues via CLI or API without explicit user review. Fix: Always gate publication behind user confirmation.

---

## Flat Reference Files

- [ISSUE-FORMAT.md](ISSUE-FORMAT.md): Issue markdown schema, structural rationale, and tracker CLI publishing snippet.
