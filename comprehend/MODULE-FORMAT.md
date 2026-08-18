# MODULE Format (HTML Walkthrough Reports)

Reference guide for structuring and styling walkthrough HTML reports produced by `/comprehend`.

---

## Core Mental Model: The "Cold-Me Six Weeks Later" Rule

An HTML walkthrough report is created for the user returning to this code weeks or months later with zero active context. It must pass the cold-start test: a reader opening the report cold must instantly get high-level system re-orientation before diving into detailed code mechanics.

---

## Creation Criterion

A walkthrough report is created **only** when all three conditions are met:
1. The walkthrough dialogue reaches a natural conclusion or stopping point.
2. You offer the report concisely.
3. The user explicitly accepts.

You do **not** judge or grade ownership.

---

## Document Structure & Layout

An HTML walkthrough report consists of two distinct sections separated by a divider:

### 1. Primary Walkthrough (Top Section - Agent-Authored)
- **Big-Picture Re-Orientation First:** Always start with a 1–2 paragraph high-level system overview. Explain what component or slice this document covers, where it sits in the broader architecture, and why this walkthrough was conducted.
- **Dialogue Progression (A → C → D):** Author the core walkthrough tailored to the user's preferred explanation style (saved in `NOTES.md`), directly following the progression of topics discussed during the session (e.g. if the dialogue walked through topics A, C, and D, the report covers A, C, and D in that order).
- **Architecture & Invariants:** Detail code architecture, entry/exit points, non-obvious logic, load-bearing invariants, and adjacent seams according to `NOTES.md` preferences.
- **Citations:** Include precise `file:line` references for every claim.

### 2. Divider (`<hr>`)

### 3. User Realizations & Mental Model Shifts (Bottom Section - User's Voice)
- **User's Interactive Realizations:** Placed at the bottom below the `<hr>` divider.
- **First-Person Voice & Framing:** Capture interactive session notes strictly from the user's perspective. Document the core questions or dilemmas explored and the concrete technical insights that resolved them.
- **Zero Observer Evaluator Language:** Avoid third-person auditor phrases (such as stating what the user examined or understood); record the substantive technical explanation that settled the mental model so a reader returning six weeks later can instantly re-anchor.

---

## Aesthetic, Typography & Assets

- **Stylesheet:** Link the shared workspace stylesheet (`.journal/assets/styles/journal.css`).
- **Visual Consistency:** Adopt the typography, spacing, and font choices generated in `journal.css`.
- **Side Notes & Callouts:** Use `<aside>` or `<figure>` elements for supplementary notes, definitions, or code callouts without breaking the narrative flow.
- **Readability:** Ensure a comfortable reading layout (optimal line length, clear headings, proper contrast).
- **Components:** Reference reusable component assets in `.journal/assets/` rather than inlining duplicated styles or scripts.
- **Print Verification:** Ensure the HTML renders cleanly on screen and prints to PDF or paper without broken section headings or cluttered UI controls.

---

## File Location

- Save HTML walkthrough reports under `.journal/comprehend/modules/0001-<slug>.html`.
