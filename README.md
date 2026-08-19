# Eds' Agent Skills

A collection of user-centered, modular skills for AI coding agents. These skills help agents communicate clearly, avoid bloated output, and produce clean, production-ready work.

---

## Skills Overview

* **[`/comprehend`](comprehend/SKILL.md)**: Generates standalone HTML code walkthroughs so you can understand what was built without flooding your chat.
* **[`/issue-it`](issue-it/SKILL.md)**: Turns bug discussions into clean GitHub issues with durable code pointers and zero pasted code blocks.
* **[`/write-skills`](write-skills/SKILL.md)**: A guide for creating clean, universal agent skills using a simple flat file structure.
* **[`/html-presentation`](html-presentation/SKILL.md)**: Builds modular, full-bleed HTML slide decks with an interactive prep session and exact PDF export.
* **[`personal/`](personal/README.md)**: Custom workflows for personal projects.

---

## Quick Installation

Install these skills on your coding agent using `npx skills`:

```bash
npx skills@latest add dimsedra/eds-skill
```

---

## What Each Skill Does

### 1. `/comprehend`: Understand Code Without the Bloat
When AI writes code fast, it is easy to lose track of how things work. `/comprehend` spins off a background agent to generate a clean, interactive HTML walkthrough report on your disk, letting you review and understand changes at your own pace.

### 2. `/issue-it`: Write Clear, Durable GitHub Issues
AI agents often write issues filled with walls of code that quickly become outdated. `/issue-it` enforces problem-focused titles, 1–2 sentence context summaries, and durable symbol links (`path/to/file` -> `functionName()`) instead of brittle line numbers or code blocks.

### 3. `/write-skills`: Build Better Agent Skills
A practical blueprint for engineering agent skills. It keeps the main `SKILL.md` lean as an orchestrator and puts domain details into flat reference files (`UPPERCASE-SLUG.md`) in the skill root, preventing messy nested folders.

### 4. `/html-presentation`: Build Custom Web Slide Decks
Create responsive, full-bleed HTML presentations:
* **Paced Alignment Session**: Sifts your raw brain dump into a clean storyline (`STORYLINE.md`) and visual style (`DECK-DESIGN.md`) before writing any code.
* **Full-Bleed Viewport**: True edge-to-edge slides with zero card-like margins.
* **Easy Narrative Edits**: Smoothly handles slide tweaks, adding/cutting slides, and major storyline pivots.
* **High-Quality PDF Export**: Dedicated printable page setup that looks identical on screen and in print.

---

## Documentation & Reference Files

### `/comprehend`
* [`SKILL.md`](comprehend/SKILL.md): Main walkthrough workflow.
* [`PROMPTS.md`](comprehend/PROMPTS.md): Subagent prompt contracts.
* [`WORKSPACE.md`](comprehend/WORKSPACE.md): Workspace setup and styles.
* [`MODULE-FORMAT.md`](comprehend/MODULE-FORMAT.md): HTML walkthrough layout rules.
* [`GLOSSARY.md`](comprehend/GLOSSARY.md): Common terms and definitions.

### `/issue-it`
* [`SKILL.md`](issue-it/SKILL.md): Main issue drafting rules and phase gates.
* [`ISSUE-FORMAT.md`](issue-it/ISSUE-FORMAT.md): Issue template and GitHub CLI command.

### `/write-skills`
* [`SKILL.md`](write-skills/SKILL.md): Main skill engineering guide.
* [`SKILL-ENGINEERING.md`](write-skills/SKILL-ENGINEERING.md): Architecture rules, tone, and avoiding overfitting.

### `/html-presentation`
* [`SKILL.md`](html-presentation/SKILL.md): Main slide deck orchestrator.
* [`ALIGNMENT.md`](html-presentation/ALIGNMENT.md): Interactive prep session guide and blueprint schemas.
* [`ARCHITECTURE.md`](html-presentation/ARCHITECTURE.md): Multi-file shell, full-bleed CSS, and PDF engine.
* [`SLIDE-FORMAT.md`](html-presentation/SLIDE-FORMAT.md): Semantic slide fragment layouts.
* [`EXTENSIONS.md`](html-presentation/EXTENSIONS.md): Cookbook for code blocks (Prism), diagrams (Mermaid), math (MathJax), and SVG charts.
* [`SCRIPTS.md`](html-presentation/SCRIPTS.md): JavaScript controller and slide loader.
