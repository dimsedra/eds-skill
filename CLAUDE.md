# Developer Rules for Skills Repository

This repository hosts pluggable, user-invoked agent skills (`disable-model-invocation: true`).

## Repository Layout

*   `comprehend/` — Skill for dialogue-based code walkthroughs and private comprehension journals.
    *   `comprehend/SKILL.md` — Core instructions.
    *   `comprehend/GLOSSARY.md` — Domain vocabulary.
    *   `comprehend/SETUP-FORMAT.md` — Preference onboarding and dynamic maintenance.
    *   `comprehend/MODULE-FORMAT.md`, `RECORD-FORMAT.md`.
*   `issue-it/` — Skill for user-centered GitHub issue creation.
    *   `issue-it/SKILL.md` — Core instructions and failure modes.
    *   `issue-it/ISSUE-FORMAT.md` — Issue template structure.
    *   `issue-it/agents/openai.yaml` — Skill metadata.

## Authoring Guidelines

1.  **No Verbatim Script Trapping:** Do not include hardcoded quote scripts (`""`) in `SKILL.md` files. State behavioral rules cleanly to prevent LLMs from parroting fixed scripts.
2.  **User-Centered Issue Design:** `/issue-it` outputs must strictly omit code snippets (` ``` `), relying instead on location pointers (`file:line`). Titles must remain problem-focused.
3.  **User-Invoked Frontmatter:** Both skills set `disable-model-invocation: true`. Descriptions must state the slash command and user-facing purpose.
4.  **Distribution:** Distributed via `npx skills` pointing directly to this repository.
