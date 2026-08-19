---
name: comprehend
description: User-invoked command (/comprehend) to generate an HTML code walkthrough for a git diff, module, function, or feature.
disable-model-invocation: true
argument-hint: What code do you want to comprehend?
---

# Comprehend

You were invoked by the user via `/comprehend` to compile a visual, standalone HTML code walkthrough directly to disk for a target code slice (a git diff, pull request, module, function, or feature).

---

## 1. Resolve the Target Code Slice

When the user runs `/comprehend`:
- **Explicit Argument Provided** (e.g. `/comprehend src/orders/`): Target that specific file, directory, function, or feature.
- **Active Git Diff**: If invoked without arguments before or after a merge/PR, inspect the active git diff or recent commits.
- **Ambiguous Target**: If no code slice or diff is identifiable, ask the user in one short sentence which part of the codebase they want to walk through.

---

## 2. Core Posture

- **Compile to Disk, Keep Chat Clean**: Delegate heavy code analysis and HTML rendering to an isolated subagent with a fresh context window ("clean head"). Never dump raw HTML markup or massive code blocks into the main chat.
- **User-Driven Exploration**: Present a clear high-level entry point with a local browser link. The user steers any follow-up questions; you answer directly and concisely without quizzing or grading.
- **Single Source of Voice**: Tone, structure, and depth are strictly governed by `.journal/comprehend/NOTES.md`.

---

## 3. Execution Lifecycle (Phase Gates)

Every `/comprehend` execution follows deterministic phase gates:

### Gate 1: Workspace & Preferences Check
- Verify the `.journal/comprehend/` workspace exists. If missing, bootstrap per [WORKSPACE.md](WORKSPACE.md).
- Ingest `.journal/comprehend/NOTES.md` to load active user preferences. If empty, run the brief onboarding interview in [WORKSPACE.md](WORKSPACE.md).

### Gate 2: Dispatch Generator Subagent
- Dispatch a **Generator Subagent** using the prompt template in [PROMPTS.md](PROMPTS.md).
- The subagent:
  1. Inspects the target code slice with a fresh context window.
  2. Compiles the standalone HTML walkthrough (`.journal/comprehend/modules/0001-<slug>.html`) per [MODULE-FORMAT.md](MODULE-FORMAT.md).
  3. Returns a lightweight receipt (file path + 2-sentence summary).

### Gate 3: Deliver Receipt & Yield Turn
- Output the clickable local link `[Open Walkthrough: <slug>](file:///...)` and the 2-sentence summary.
- Yield turn immediately to the user.
- If the user asks follow-up technical questions, answer concisely in 1-2 paragraphs without code dumping.

### Gate 4: Feedback & Revision Gate
- When the user provides feedback or requests changes to the walkthrough:
 - Update `.journal/comprehend/NOTES.md` if the feedback introduces a lasting preference.
 - **Never edit HTML inline**. Dispatch a **Revision Subagent** using the prompt template in [PROMPTS.md](PROMPTS.md) to modify `.journal/comprehend/modules/0001-<slug>.html` on disk.
 - Return a clean 1-line update receipt with the refreshed file link.

---

## 4. Failure Modes

- **Inline HTML Pollution**: Dumping markup or extensive code diffs into the parent chat instead of delegating file writes to a subagent.
- **Inline Revision Bloat**: Editing or rewriting walkthrough `.html` files directly in the parent context upon feedback.
- **Context Fatigue Drift**: Analyzing large code slices within a bloated parent session instead of dispatching a clean-head subagent.
- **Preference Routing Leakage**: Writing comprehension preferences to global agent files rather than `.journal/comprehend/NOTES.md`.
- **Checkpoint/Quiz Drift**: Interrogating the user or testing comprehension instead of providing clear explanations on demand.

---

## Flat Reference Files

- [WORKSPACE.md](WORKSPACE.md): Setup, directory structure, stylesheet generation, and preferences routing.
- [PROMPTS.md](PROMPTS.md): Subagent dispatch contracts for generator and revision agents.
- [MODULE-FORMAT.md](MODULE-FORMAT.md): HTML walkthrough document specifications and layout rules.
- [GLOSSARY.md](GLOSSARY.md): System terminology definitions.
