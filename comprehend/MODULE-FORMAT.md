# MODULE Format

Reference for structuring walkthrough HTML documents produced by `/comprehend`.

---

## Creation Criterion

A walkthrough document is created **only** when all three conditions are met:
1. The walkthrough dialogue reaches a natural conclusion or stopping point.
2. The agent offers the document flatly (*"Want me to capture this as a walkthrough doc, in your words, for you to revisit later?"*).
3. The user explicitly accepts.

The agent does **not** judge or grade ownership.

---

## Agent Behavior & Document Structure

When constructing a walkthrough document:

### 1. Primary Agent Explanation (Top Section)
- Author the core walkthrough: code architecture, entry/exit points, non-obvious logic, load-bearing invariants, and adjacent seams.
- Include precise file:line citations for every claim.

### 2. Divider (`<hr>`)

### 3. Session Log (Bottom Section)
- Capture the user's interactive session notes:
  - **User Questions**: Questions or clarifications requested by the user.
  - **Key Connections / Insights**: Structural notes or connections discussed during the session.

---

## Formatting & Verification

- Save HTML walkthroughs under `.journal/comprehend/modules/0001-<slug>.html`.
- Link the workspace stylesheet (`.journal/assets/styles/journal.css`).
- Follow the aesthetic and print rules in [WRITING-HTML-REPORT.md](WRITING-HTML-REPORT.md).
