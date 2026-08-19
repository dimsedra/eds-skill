---
name: comprehend
description: User-invoked command (/comprehend) for two-way code walkthroughs. Use when the user wants to understand code being shipped, recently shipped, modules, functions, or features.
disable-model-invocation: true
argument-hint: What code do you want to comprehend?
---

# Comprehend

`/comprehend` compiles a visual, standalone HTML code walkthrough directly to disk. Use it whenever the user wants to understand anything in their codebase—code that will be shipped, code that was just shipped, or specific modules, functions, and features.

---

## When to Use

Reach for `/comprehend` when:
- The user wants to understand a **git diff**, pull request, or changes that are about to be shipped or were just shipped.
- The user wants a structured walkthrough of specific modules, functions, or features.
- The user asks to explore, comprehend, or map out how a part of the codebase works.

**Do NOT use when:**
- The change is a trivial 1-line fix (a walkthrough is overkill).
- The user just wants to quickly ship code, run a test, or fix a syntax error without a walkthrough.

---

## Core Posture

- **Compile to Disk, Keep Chat Clean**: Delegate heavy code analysis and HTML rendering to isolated subagents with fresh context windows ("clean head"). Never dump raw HTML or massive code traces into the main conversation.
- **User-Driven Exploration**: Present a clear high-level entry point with a local browser link. The user steers any follow-up questions; you explain mechanisms and invariants directly and concisely.
- **Single Source of Voice**: Tone, structure, and depth are strictly governed by `.journal/comprehend/NOTES.md`.

---

## State Machine & Execution Lifecycle

Every `/comprehend` session executes across deterministic phase gates:

### Gate 1: Workspace & Preferences Check
- Verify the `.journal/comprehend/` workspace exists. If missing, bootstrap per [WORKSPACE.md](WORKSPACE.md).
- Ingest `.journal/comprehend/NOTES.md` to load active user preferences. If empty, run the brief onboarding interview in [WORKSPACE.md](WORKSPACE.md).

### Gate 2: Dispatch Generator Subagent
- Dispatch a **Generator Subagent** using the prompt contract in [PROMPTS.md](PROMPTS.md).
- The subagent:
  1. Inspects the target code slice with a fresh context window.
  2. Compiles the standalone HTML walkthrough (`.journal/comprehend/modules/0001-<slug>.html`) per [MODULE-FORMAT.md](MODULE-FORMAT.md).
  3. Returns a lightweight receipt (file path + 2-sentence summary).

### Gate 3: Deliver Receipt & Exploration Gate
- Output the clickable local link `[Open Walkthrough: <slug>](file:///...)` and the 2-sentence summary.
- Yield turn immediately to the user.
- If the user asks follow-up technical questions, answer concisely in 1–2 paragraphs without code dumping.

### Gate 4: Feedback & Revision Gate
- When the user provides feedback or requests changes to the walkthrough:
  - Update `.journal/comprehend/NOTES.md` if the feedback introduces a lasting preference.
  - **Never edit HTML inline**. Dispatch a **Revision Subagent** using the prompt contract in [PROMPTS.md](PROMPTS.md) to modify `.journal/comprehend/modules/0001-<slug>.html` on disk.
  - Return a clean 1-line update receipt with the refreshed file link.

---

## Failure Modes

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
