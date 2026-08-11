# MODULE Format

Reference for structuring walkthrough HTML reports produced by `/comprehend`.

---

## Core Mental Model: The "Cold-Me Six Weeks Later" Rule

An HTML walkthrough report is created for the user returning to this code weeks or months later with zero active context. It must pass the cold-start test: a reader opening the report cold must instantly get high-level system re-orientation before diving into detailed code mechanics.

---

## Creation Criterion

A walkthrough report is created **only** when all three conditions are met:
1. The walkthrough dialogue reaches a natural conclusion or stopping point.
2. The agent offers the report concisely.
3. The user explicitly accepts.

The agent does **not** judge or grade ownership.

---

## Document Structure & Pacing

An HTML walkthrough report consists of two distinct sections separated by a divider:

### 1. Primary Walkthrough (Top Section - Agent-Authored)
- **Big-Picture Re-Orientation First:** Always start with a 1–2 paragraph high-level system overview. Explain what component or slice this document covers, where it sits in the broader architecture, and why this walkthrough was conducted.
- **Dialogue Progression (A → C → D):** Author the core walkthrough tailored to the user's preferred explanation style (saved in `NOTES.md`), directly following the progression of topics discussed during the session (e.g. if the dialogue walked through topics A, C, and D, the report covers A, C, and D in that order).
- **Architecture & Invariants:** Detail code architecture, entry/exit points, non-obvious logic, load-bearing invariants, and adjacent seams according to `NOTES.md` preferences.
- **Citations:** Include precise `file:line` references for every claim.

### 2. Divider (`<hr>`)

### 3. Session Log (Bottom Section - User Notes & Framing)
- **User's Interactive Notes:** Placed at the bottom below the `<hr>` divider.
- **User's Words & Framing:** Capture the user's interactive session notes, questions, pushbacks, key connections, and dictated insights recorded during the conversation.

---

## Formatting & Location

- Save HTML walkthrough reports under `.journal/comprehend/modules/0001-<slug>.html`.
- Link the workspace stylesheet (`.journal/assets/styles/journal.css`).
- Follow the visual and print conventions in [WRITING-HTML-REPORT.md](WRITING-HTML-REPORT.md).
