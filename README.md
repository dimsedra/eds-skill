# Agent Skills

A collection of user-centered, pluggable agent skills designed to improve comprehension and clarity in AI-assisted development.

This repository hosts four skills:
*   **`/comprehend`** — Dialogue-based, two-way code walkthroughs to gate pre-merge diffs or pay down comprehension debt.
*   **`/issue-it`** — Convert problem discussions and bugs into clean, user-centered GitHub issues (no code block bloat, problem-focused titles).
*   **`/write-skills`** — Meta-skill for writing, refining, and auditing universal agent skills against overfitting and verbosity.
*   **`html-presentation`** — Engineer custom HTML slide decks with responsive viewport fitting, keyboard navigation, and exact PDF export.

---

## Installation

Install the skills on your coding agent using `npx skills`:

```bash
npx skills@latest add dimsedra/eds-skill
```

---

## Skills Included

### 1. `/comprehend` — Code Walkthrough & Ownership
In agent-led development, code is produced at an unprecedented speed, creating instant **comprehension debt**. `/comprehend` runs a bounded session time block to walk through code slices 1–2 paragraphs at a time.

*   **Pre-Merge (Gating Mode):** Understand a diff before merging so you can defend it in code review.
*   **Post-Merge (Paying-down Mode):** Walk through complex modules over time to build long-term retention.

### 2. `/issue-it` — User-Centered Issue Drafting
Agents often write issues catered to themselves — filled with verbose prompt language, agent register, and pasted code blocks. `/issue-it` enforces user-centered issue drafting:
*   **Problem-Focused Titles:** Describe the failure condition, not generic solution actions.
*   **Big-Picture & Localized Context:** 1–2 sentence architecture context followed by digestible problem details.
*   **Location Pointers, Zero Code Snippets:** Strict prohibition on code blocks (` ``` `). Refers to files and line ranges (`path/to/file:L10-L20`) so issues stay clean and readable for the user.
*   **High-Level Fix Direction:** Outlines strategic design intent without pasting code implementations into the issue tracker.

### 3. `/write-skills` — Skill Engineering Meta-Skill
A meta-methodology for engineering universal agent skills that steer LLM reasoning without overfitting or template fixation:
*   **Nudge Center of Gravity:** Shift the LLM's posture through principles and dynamic discovery, not hardcoded code blocks or preset themes.
*   **Anti-Overfitting Audit:** Strip code block fixation, single-project bias, preset color hardcoding, and arbitrary numeric thresholds.

### 4. `html-presentation` — HTML Slide Deck Engineering
Build custom, web-based presentation decks for any domain or visual requirement:
*   **Dynamic Discovery First:** Align with user context, brand, and delivery setting before writing code.
*   **Architecture Patterns:** Modular multi-file, single-file dynamic, or dedicated print assembly based on project scale.
*   **Exact PDF Export:** Full-bleed color preservation, page-break precision, and print-ready geometry.

---

## Workspace Structures

*   **Comprehend Workspace:** `.journal/comprehend/` (contains `NOTES.md`, `records/*.md`, and `modules/*.html`).
*   **Issue-It Output:** Prepares formatted markdown issues or pushes directly to GitHub via `gh issue create`.

---

## References

### `/comprehend` Documentation
*   [SKILL.md](comprehend/SKILL.md) — Core walkthrough skill instructions.
*   [GLOSSARY.md](comprehend/GLOSSARY.md) — Standard definitions (frontier, signals, desirable difficulty, etc.).
*   [SETUP-FORMAT.md](comprehend/SETUP-FORMAT.md) — Guidelines for onboarding interviews and preference maintenance.
*   [MODULE-FORMAT.md](comprehend/MODULE-FORMAT.md) — HTML walkthrough report structure and aesthetic guidelines.

### `/issue-it` Documentation
*   [SKILL.md](issue-it/SKILL.md) — Core user-centered issue drafting rules.
*   [ISSUE-FORMAT.md](issue-it/ISSUE-FORMAT.md) — GitHub issue template structure and rules.

### `/write-skills` Documentation
*   [SKILL.md](write-skills/SKILL.md) — Meta-skill for engineering universal agent skills.
*   [SKILL-ENGINEERING.md](write-skills/SKILL-ENGINEERING.md) — Overfitting prevention, posture nudging, and information hierarchy.

### `html-presentation` Documentation
*   [SKILL.md](html-presentation/SKILL.md) — Slide deck engineering skill instructions.
*   [DECK-ENGINEERING.md](html-presentation/DECK-ENGINEERING.md) — Architecture patterns, design systems, navigation, and PDF export.
