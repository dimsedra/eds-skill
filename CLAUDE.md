# Developer Rules for Skills Repository

This repository hosts pluggable agent skills (`disable-model-invocation` varies per skill).

## Repository Layout

*   `comprehend/` — User-invoked skill for dialogue-based code walkthroughs and private comprehension journals.
    *   `comprehend/SKILL.md` — Core instructions.
    *   `comprehend/GLOSSARY.md` — Domain vocabulary.
    *   `comprehend/SETUP-FORMAT.md` — Preference onboarding and dynamic maintenance.
    *   `comprehend/MODULE-FORMAT.md`, `RECORD-FORMAT.md`.
*   `issue-it/` — User-invoked skill for user-centered GitHub issue creation.
    *   `issue-it/SKILL.md` — Core instructions and failure modes.
    *   `issue-it/ISSUE-FORMAT.md` — Issue template structure.
    *   `issue-it/agents/openai.yaml` — Skill metadata.
*   `authoring-agent-skills/` — Meta-skill for engineering universal agent skills.
    *   `authoring-agent-skills/SKILL.md` — Core meta-methodology.
    *   `authoring-agent-skills/SKILL-ENGINEERING.md` — Overfitting prevention and posture nudging.
*   `html-presentation/` — Skill for engineering custom HTML slide decks.
    *   `html-presentation/SKILL.md` — Core deck engineering instructions.
    *   `html-presentation/DECK-ENGINEERING.md` — Architecture, design systems, navigation, and PDF export.

## Authoring Guidelines

1.  **No Verbatim Script Trapping:** Do not include hardcoded quote scripts (`""`) in `SKILL.md` files. State behavioral rules cleanly to prevent LLMs from parroting fixed scripts.
2.  **User-Centered Issue Design:** `/issue-it` outputs must strictly omit code snippets (` ``` `), relying instead on location pointers (`file:line`). Titles must remain problem-focused.
3.  **User-Invoked Frontmatter:** `/comprehend` and `/issue-it` set `disable-model-invocation: true`. `authoring-agent-skills` and `html-presentation` allow model invocation.
4.  **Anti-Overfitting:** Never include hardcoded code blocks, fixed color hexes, preset theme names, or arbitrary numeric thresholds in skill files.
5.  **Distribution:** Distributed via `npx skills` pointing directly to this repository.
