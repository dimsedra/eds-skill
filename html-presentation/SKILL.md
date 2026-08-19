---
name: html-presentation
description: Build modular HTML presentation slide decks with responsive viewport fitting, custom keyboard navigation, and exact PDF/print export. Use when the user asks to create HTML slides, build a presentation deck, convert slides to HTML, generate slide presentations, or export HTML slides to PDF.
disable-model-invocation: false
---

# HTML Presentation

Build modular, responsive HTML presentation slide decks with dedicated print/PDF export capabilities.

---

## Core Posture

- **Discover Before Building**: Clarify visual identity, aspect ratio, typography, and structure before writing code.
- **Full-Bleed Viewport Fitting**: The presentation viewport and slide canvas must fit 100% edge-to-edge with zero outer margins or gaps. Content breathing room belongs strictly inside the slide padding.
- **Modular Multi-File Architecture**: Isolate slides into clean HTML fragments; orchestrate viewer state in a central shell.
- **Pure Presentation Hygiene**: Enforce strict semantic HTML without inline styles or leaked Markdown syntax.

---

## Invocation Models

- **User-Invoked (`/html-presentation`)**: Pair interactively with the user to discover deck goals, audience, tone, palette, and slide outline.
- **Agent-Invoked**: When given an existing presentation outline or specification, proceed directly to Gate 1 artifact scaffolding.

---

## Deterministic Phase Gates

### Gate 1: Alignment & Design
- Align on presentation context, aspect ratio (e.g., 16:9), typography, and color palette.
- Scaffold `DECK-DESIGN.md` in the presentation root as the single source of truth for all design tokens and layouts.
- Consult [DECK-ENGINEERING.md](DECK-ENGINEERING.md) for architecture rules and token specifications.

### Gate 2: Delegated Deck Generation
- Dispatch a clean-head subagent to generate all project files on disk to prevent chat bloat:
  - Presentation shell (`index.html`) and PDF print assembler (`export_pdf.html`).
  - Central stylesheet (`css/styles.css`) implementing tokens from `DECK-DESIGN.md`.
  - Interactive loader and controller scripts (`js/slide-loader.js`, `js/main.js`).
  - Slide fragments (`slides/slide-01.html` ... `slides/slide-NN.html`) matching schemas in [SLIDE-FORMAT.md](SLIDE-FORMAT.md).
- Follow loader and controller lifecycle contracts in [SCRIPTS.md](SCRIPTS.md).

### Gate 3: Verification & Delivery
- Verify slide fragment count matches `totalSlides` in `js/slide-loader.js`.
- Check hash navigation (`#slide-1`), keyboard shortcuts, and dropdown synchronization.
- Inspect slide markup for pure HTML hygiene (confirm zero Markdown syntax and zero inline styles).
- Verify `export_pdf.html` contains the 1000ms rendering settlement pause and exact print color CSS.

---

## Failure Modes

- **Chat Bloat**: Emitting dozens of slide HTML fragments in the main conversation instead of delegating file generation to a subagent.
- **Floating Card Slide Drift**: Adding outer margins, rounded borders, or drop shadows to the slide container so slides look like floating cards in a gray void instead of a true full-bleed presentation.
- **Preset Fixation**: Imposing arbitrary palettes or fonts without grounding them in user discovery and `DECK-DESIGN.md`.
- **Markdown Leaking**: Leaving unparsed Markdown syntax (`**bold**`, `` `code` ``, `- list`) inside slide HTML fragments.
- **Inline Style Pollution**: Adding inline `style="..."` attributes or `<style>` blocks into slide fragments instead of `css/styles.css`.
- **Premature Print Export**: Triggering `window.print()` before fragments are fetched or before dynamic rendering (MathJax/Mermaid) settles.

---

## Disclosed References

- [DECK-ENGINEERING.md](DECK-ENGINEERING.md): Multi-file architecture, token system, and high-fidelity PDF export engine.
- [SLIDE-FORMAT.md](SLIDE-FORMAT.md): Semantic slide fragment schemas, layout patterns, and pure HTML hygiene.
- [SCRIPTS.md](SCRIPTS.md): JS controller, slide loader lifecycle, and dynamic re-rendering engines.
