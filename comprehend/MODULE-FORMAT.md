# MODULE Format

Reference for structuring walkthrough HTML reports produced by `/comprehend`.

---

## Creation Criterion

A walkthrough report is created **only** when all three conditions are met:
1. The walkthrough dialogue reaches a natural conclusion or stopping point.
2. The agent offers the report flatly (e.g. asking if the user wants the walkthrough captured in an HTML report for future reference).
3. The user explicitly accepts.

The agent does **not** judge or grade ownership.

---

## Document Structure & Pacing

An HTML walkthrough report consists of two distinct sections separated by a divider:

### 1. Primary Walkthrough (Top Section)
- **Agent-Authored Clarity:** Author the core walkthrough for maximum technical clarity, directly following the progression of topics discussed during the session (e.g., if the dialogue walked through topics A, C, and D, the report covers A, C, and D in that order).
- **Technical Precision:** Detail code architecture, entry/exit points, non-obvious logic, load-bearing invariants, and adjacent seams.
- **Citations:** Include precise `file:line` references for every claim.

### 2. Divider (`<hr>`)

### 3. Session Log (Bottom Section)
- **User's Interactive Notes:** Placed at the bottom below the `<hr>` divider.
- **User's Words & Framing:** Capture the user's interactive session notes, questions, pushbacks, key connections, and dictated insights recorded during the conversation.

---

## Formatting & Location

- Save HTML walkthrough reports under `.journal/comprehend/modules/0001-<slug>.html`.
- Link the workspace stylesheet (`.journal/assets/styles/journal.css`).
- Follow the visual and print conventions in [WRITING-HTML-REPORT.md](WRITING-HTML-REPORT.md).
