# Comprehend Skill

Dialogue-based, conversational, two-way code walkthroughs tailored to your preferences and proficiency. Use it before the merge to understand the diff, or after to pay down comprehension debt.

This repository hosts `/comprehend` as a standalone, pluggable skill.

---

## Installation

Install the skill on your coding agent using `npx skills`:

```bash
npx skills@latest add dimsedra/eds-skill
```

---

## Why `/comprehend` Exists

In agent-led development, code is produced at an unprecedented speed, creating instant **comprehension debt** — code in your repo that you can't explain, defend in a review, or debug at 3 AM. 

`/comprehend` resolves this:
*   **Before the merge:** Use gating mode to walkthrough and understand the diff so you can fully defend the code before it ships.
*   **After the merge:** Use paying-down mode to walk through code slices over multiple sessions, building long-term retention.

Comprehension belongs to the human. The agent's role is strictly to **inform and explain** code clearly, adapting to your preferences. The agent does not test, quiz, or grade you.

---

## How It Works

### 1. First-Run Setup & Dynamic CSS
On its first run in a project, `/comprehend` automatically:
- Scaffolds a private `.journal/` workspace (and appends it to `.gitignore`).
- **Dynamic CSS:** Inspects your project's code, structure, and styling to dynamically generate a clean, premium, highly readable CSS stylesheet tailored specifically to your project's aesthetic. This is written to `.journal/assets/styles/journal.css`.
- Runs a short onboarding interview to establish your preferred learning style (e.g., systemic/structural, step-by-step logic tracing, or conceptual metaphors) and saves it to `.journal/comprehend/NOTES.md`.

### 2. Walking Through Code
You invoke the command and point it at the code:
```bash
/comprehend src/auth/session.ts
```
The agent explains the code in line with your preferences. You ask follow-up questions about why decisions were made, invariant logic, or dependencies.

### 3. Optional Walkthrough Docs
When the walkthrough dialogue finishes, the agent will flatly ask if you want to capture the explanation. If you accept, the agent formats a walkthrough HTML document under `.journal/comprehend/modules/` in **your own words** based on the conversation, linking the project-tailored `journal.css`.

---

## The Ownership Workspace

All comprehension progress is saved in a private workspace `.journal/` at the root of your project:

```
.journal/
  assets/
    styles/journal.css     # Stylesheet dynamically generated to match your project
  comprehend/
    MISSION.md             # The focus of your current walkthrough and success criteria
    NOTES.md               # Your active explanation preferences (continually refined by the agent)
    records/*.md           # Brief session records capturing the shape of walkthroughs
    modules/*.html         # Optional walkthrough documents in your own words
    reference/*.html       # Project-specific glossaries, invariants, and reading maps
```

---

## References

For deep-dive documentation on skill formats and behaviors:
*   [GLOSSARY.md](comprehend/GLOSSARY.md) - Standard definitions (frontier, signals, desirable difficulty, etc.).
*   [SETUP-FORMAT.md](comprehend/SETUP-FORMAT.md) - Guidelines for onboarding interviews and how the agent dynamically maintains `NOTES.md`.
*   [MISSION-FORMAT.md](comprehend/MISSION-FORMAT.md) - How `MISSION.md` is structured.
*   [RECORD-FORMAT.md](comprehend/RECORD-FORMAT.md) - Structure for markdown session records.
*   [MODULE-FORMAT.md](comprehend/MODULE-FORMAT.md) - Rules for generating walkthrough HTML documents.
*   [WRITING-HTML-REPORT.md](comprehend/WRITING-HTML-REPORT.md) - Layout, typography, and print-ready HTML conventions.
