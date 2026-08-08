# Developer Rules for Comprehend Skill

This repository is a single-skill, standalone, pluggable workspace for the `/comprehend` skill.

## Repository Layout

*   `comprehend/SKILL.md` — The main agent instructions.
*   `comprehend/GLOSSARY.md` — Glossary of terms (frontier, signals, etc.).
*   `comprehend/SETUP-FORMAT.md` — Guide for user onboarding and dynamic preferences.
*   `comprehend/MISSION-FORMAT.md` — Mission document layout.
*   `comprehend/RECORD-FORMAT.md` — Session record structure.
*   `comprehend/MODULE-FORMAT.md` — Walkthrough HTML layout.
*   `comprehend/WRITING-HTML-REPORT.md` — HTML output and typography styling rules.
*   `comprehend/agents/openai.yaml` — Skill metadata and client configuration.

## Contribution Guidelines

1.  **Strict Singularity:** Do not add other skills or sibling buckets. This repository must remain exclusively focused on `/comprehend` to keep it clean and pluggable.
2.  **No Static Stylesheets:** Do not commit a static `tufte.css` or generic styles. The stylesheet `.journal/assets/styles/journal.css` must be dynamically generated during the setup phase of `comprehend/SKILL.md` to fit the specific project's tech stack and style guidelines.
3.  **Onboarding & Updating Preferences:** Always follow the guidelines in `comprehend/SETUP-FORMAT.md`. If preferences are empty, perform onboarding. Continuously monitor user feedback during the walkthrough and update `.journal/comprehend/NOTES.md` with new insights.
4.  **Distribution:** The skill is distributed via `npx skills` pointing directly to this GitHub repository. Ensure `SKILL.md` contains accurate markdown and a valid YAML frontmatter.
