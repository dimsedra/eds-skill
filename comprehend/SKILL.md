---
name: comprehend
description: User-invoked command (/comprehend) for two-way code walkthroughs. Use before merging to gate a diff or after to pay down comprehension debt.
disable-model-invocation: true
argument-hint: What code do you want to comprehend?
---

# Comprehend

`/comprehend` compiles a visual, standalone HTML code walkthrough directly to disk and provides interactive exploration driven by the user.

---

## Core Posture

- **Compile to Disk, Keep Chat Clean**: Delegate heavy code analysis and HTML rendering to isolated subagents with fresh context windows ("clean head"). Never dump raw HTML or massive code traces into the main conversation.
- **User-Driven Exploration**: Present a clear high-level entry point. The user steers the depth, pacing, and questions; you explain mechanisms and invariants without quizzing or grading.
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
  2. Initializes the session record (`.journal/comprehend/records/0001-<slug>.md`) per [RECORD-FORMAT.md](RECORD-FORMAT.md).
  3. Compiles the standalone HTML walkthrough (`.journal/comprehend/modules/0001-<slug>.html`) per [MODULE-FORMAT.md](MODULE-FORMAT.md).
  4. Returns a lightweight receipt (file path + 2-sentence summary).

### Gate 3: Deliver Receipt & User Exploration Gate
- Output the clickable local link `[Open Walkthrough: <slug>](file:///...)` and the 2-sentence summary.
- Yield turn immediately to the user.
- If the user asks technical questions, answer concisely in 1–2 paragraphs without code dumping.

### Gate 4: Feedback & Revision Gate
- When the user provides feedback or requests changes to the walkthrough:
  - Update `.journal/comprehend/NOTES.md` if the feedback introduces a lasting preference.
  - **Never edit HTML inline**. Dispatch a **Revision Subagent** using the prompt contract in [PROMPTS.md](PROMPTS.md) to modify `.journal/comprehend/modules/0001-<slug>.html` on disk.
  - Return a clean 1-line update receipt to the user.

### Gate 5: Session Wrap-Up Gate
- When dialogue concludes or the user is satisfied:
  - Summarize breakthroughs and technical realizations from the user's first-person perspective.
  - Update the **Session Summary & Insights** in the session record (`.journal/comprehend/records/0001-<slug>.md`) and append them to the bottom section of the HTML module.

---

## Failure Modes

- **Inline HTML Pollution**: Dumping markup or extensive code diffs into the parent chat instead of delegating file writes to a subagent.
- **Inline Revision Bloat**: Editing or rewriting walkthrough `.html` files directly in the parent context upon feedback.
- **Context Fatigue Drift**: Analyzing large code slices within a bloated parent session instead of dispatching a clean-head subagent.
- **Preference Routing Leakage**: Writing comprehension preferences to global agent files rather than `.journal/comprehend/NOTES.md`.
- **Evaluator Voice Drift**: Documenting session insights as an external auditor/teacher instead of recording substantive technical realizations in the user's voice.
- **Checkpoint/Quiz Drift**: Interrogating the user or testing comprehension instead of providing clear explanations on demand.

---

## Flat Reference Files

- [WORKSPACE.md](WORKSPACE.md): Setup, directory structure, stylesheet generation, and preferences routing.
- [PROMPTS.md](PROMPTS.md): Subagent dispatch contracts for generator and revision agents.
- [MODULE-FORMAT.md](MODULE-FORMAT.md): HTML walkthrough document specifications and layout rules.
- [RECORD-FORMAT.md](RECORD-FORMAT.md): Session record markdown schema and mission tracking.
- [GLOSSARY.md](GLOSSARY.md): System terminology definitions.
