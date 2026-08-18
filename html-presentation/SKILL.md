---
name: html-presentation
description: Build modular HTML presentation slide decks with responsive viewport fitting, custom keyboard navigation, and exact PDF/print export. Use when the user asks to create HTML slides, build a presentation deck, convert slides to HTML, generate slide presentations, or export HTML slides to PDF.
disable-model-invocation: false
---

# HTML Presentation

## First Principle

Every choice you make (architecture, aesthetic, technique) follows from the user's context, brand, and presentation goals. A fixed template shapes the deck around itself, not around the user; discover requirements first, then engineer a custom system.

---

## Core Posture

- **Discover Before Building**: Clarify visual identity, aspect ratio, typography, interaction, and structural requirements before writing code.
- **Modular Architecture**: Build every deck using the modular multi-file pattern (central shell with isolated slide fragments) and dedicated print assembly.
- **Maintain Presentation Hygiene**: Keep content markup clean and semantic, and ensure exact color preservation on print/PDF export.

---

## Triggers

Reach for this skill when the user requests:
- Creating HTML slides or web presentation decks.
- Converting raw text, markdown, or existing documents into web slides.
- Implementing navigation, viewport scaling, or PDF export for HTML slide decks.

---

## When NOT to Invoke

- Generating a static document or academic manuscript.
- Providing a plain text outline without web UI engineering → respond directly.
- Building a standalone web application or landing page.

---

## Execution Workflow

### 1. Requirements Discovery
Align with the user on:
- Purpose, domain, and delivery setting (pitch, defense, lecture, report, workshop).
- Aesthetic direction (palette contrast, typography family, surface styling).
- Aspect ratio (16:9 landscape, 4:3, responsive viewport).
- Control requirements (keyboard navigation, UI indicators, PDF export target).
- Content structural requirements (citations, tags, or author notes if requested).

### 2. Architecture & Design Tokens
Consult [DECK-ENGINEERING.md](DECK-ENGINEERING.md):
- Once alignment settles the design direction, scaffold `DECK-DESIGN.md` next to the deck files: palette, typography, aspect ratio, surfaces, and interaction. The document, not your memory, holds the design, allowing the user to steer it while keeping every file consistent.
- Scaffold the modular presentation layout matching the contracts in [DECK-ENGINEERING.md](DECK-ENGINEERING.md) (`index.html`, `js/slide-loader.js`, `js/main.js`, and `export_pdf.html`).
- Construct custom CSS variables for colors, typography scaling, spacing, and surfaces derived entirely from user alignment.

### 3. Content Transformation
Transform presentation content into clean HTML:
- Structure each slide using semantic HTML elements tailored to its specific content and purpose.
- Format text and media using appropriate standard semantic tags.
- Pure HTML only (zero Markdown leaking): Never use raw Markdown syntax (such as `**bold**`, `*italic*`, `` `code` ``, `[text](url)`, or `- bullet`) inside `.html` files. Convert all formatting to native HTML tags (`<strong>`, `<em>`, `<code>`, `<a>`, `<ul><li>`).
- Include metadata, citations, or speaker notes only when requested or relevant to the presentation context.
- Maintain strict separation of content and styling: slide fragments are optimized for human reading and editing. Never use inline `style="..."` attributes or `<style>` blocks in slide files; all layout and component styles belong in `css/styles.css`.

### 4. Interaction & Export Verification
Apply patterns from [DECK-ENGINEERING.md](DECK-ENGINEERING.md):
- Bind keyboard navigation listeners and sync slide state with UI controls and hash URLs following the controller and loader contracts.
- Ensure dynamic elements (MathJax formulas, Mermaid diagrams, or Prism syntax-highlighted code blocks) re-render on slide changes.
- Verify print/PDF export geometry and force exact color rendering (`print-color-adjust: exact`) using the runtime assembly script pattern in `export_pdf.html` (including fixed inch dimensions and the mandatory async rendering settlement delay).

---

## Failure Modes

- **Preset Fixation**: Forcing specific colors, fonts, or component templates onto a project without user discovery.
- **Template Copying**: Copying fixed example content or themes instead of engineering a system tailored to the user's specific topic and brand.
- **Markdown Leaking**: Leaving raw Markdown syntax (such as `**text**`, `*text*`, or `` `code` ``) inside `.html` files instead of native HTML tags.
- **Inline Style Pollution**: Adding inline `style="..."` or `<style>` tags into slide fragments instead of defining reusable classes in `css/styles.css`.
- **Premature Print / Blank Export**: Calling `window.print()` synchronously before fragments are fetched or before MathJax/Mermaid finishes rendering. Always await all async passes and a 1000ms delay before print.
- **Print Overflow Lock**: Setting `overflow: hidden` or `height: 100vh` on `html`/`body` in print mode, which cuts off multi-page slide flow.
- **Print Background Loss**: Omitting exact print color properties (`print-color-adjust: exact !important`), causing browsers to strip backgrounds in PDF exports.

---

## Disclosed Reference

- [DECK-ENGINEERING.md](DECK-ENGINEERING.md): Unified guide for architecture patterns, design system construction, interactive navigation, and exact PDF export.
