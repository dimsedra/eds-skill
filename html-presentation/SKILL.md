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
- **Sifter & Mirror Alignment**: Meet unstructured human brain dumps with active listening, sifting raw thoughts into clear Action Headlines.
- **Full-Bleed Viewport Fitting**: The presentation viewport and slide canvas must fit 100% edge-to-edge with zero outer margins or gaps. Content breathing room belongs strictly inside the slide padding.
- **Modular Multi-File Architecture**: Isolate slides into clean HTML fragments; orchestrate viewer state in a central shell.
- **Pure Presentation Hygiene**: Enforce strict semantic HTML without inline styles or leaked Markdown syntax.

---

## Invocation Models

- **User-Invoked (`/html-presentation`)**: Pair interactively with the user to discover deck goals, audience, tone, palette, and slide outline.
- **Agent-Invoked**: When given an existing presentation outline or specification, proceed directly to Gate 1 artifact scaffolding.

---

## Deterministic Phase Gates

### Gate 1: Alignment & Design (4-Pass Funnel Session)
- Execute the funnel alignment session per [ALIGNMENT.md](ALIGNMENT.md) (ask strictly 1 pass per turn; wait for response):
  - **Pass 1 (Open Brain Dump)**: Wide-open invitation for raw thoughts, topic, audience, and ideas with zero interrogation pressure.
  - **Pass 2 (Sift & Clarify)**: Mirror extracted core message and clarify only missing format/budget parameters.
  - **Pass 3 (Storyline Lock-In)**: Propose synthesized Action Headlines sequence for pure narrative validation.
  - **Pass 4 (Visual Styling & Theme)**: Lock visual mood, color palette tokens, and typography.
- Scaffold `DECK-DESIGN.md` in the presentation root as the single source of truth for narrative flow and design tokens.
- Consult [ARCHITECTURE.md](ARCHITECTURE.md) for shell architecture and full-bleed viewport tokens.

### Gate 2: Delegated Deck Generation
- Dispatch a clean-head subagent to generate all project files on disk to prevent chat bloat:
  - Presentation shell (`index.html`) and PDF print assembler (`export_pdf.html`) per [ARCHITECTURE.md](ARCHITECTURE.md).
  - Central stylesheet (`css/styles.css`) implementing tokens from `DECK-DESIGN.md`.
  - Interactive loader and controller scripts (`js/slide-loader.js`, `js/main.js`) per [SCRIPTS.md](SCRIPTS.md).
  - Slide fragments (`slides/slide-01.html` ... `slides/slide-NN.html`) matching schemas in [SLIDE-FORMAT.md](SLIDE-FORMAT.md).

### Gate 3: Verification & Initial Delivery
- Verify slide fragment count matches `totalSlides` in `js/slide-loader.js`.
- Check hash navigation (`#slide-1`), keyboard shortcuts, and dropdown synchronization.
- Inspect slide markup for pure HTML hygiene (confirm zero Markdown syntax and zero inline styles).
- Verify `export_pdf.html` contains the 1000ms rendering settlement pause and exact print color CSS.

### Gate 4: Iterative Revision & Re-Entry Gate
Accommodate non-linear human iteration based on user feedback:
- **Slide Tweaks**: Edit targeted `slides/slide-NN.html` fragments or `css/styles.css` directly.
- **Slide Additions / Deletions**: Update `DECK-DESIGN.md`, generate or remove fragments, re-index sequential filenames (`slide-01.html` ... `slide-NN.html`), and update `totalSlides` in `slide-loader.js`.
- **Storyline Pivots**: Re-enter Gate 1 per [ALIGNMENT.md](ALIGNMENT.md), update Action Headlines in `DECK-DESIGN.md`, and re-dispatch subagent to regenerate the deck.

---

## Failure Modes

- **Rigid Interrogation Drift**: Forcing the user to answer formulaic questions instead of sifting their raw, unstructured thoughts.
- **Question Dump Bloat**: Dumping all alignment questions at once in a massive wall of text instead of conversational, round-by-round turns.
- **Unground Deck Generation**: Generating slide files before locking in the Slide Content Framework and Big Idea in `DECK-DESIGN.md`.
- **Stale Index Regressions**: Inserting or deleting slide fragments without updating `totalSlides` or re-numbering subsequent slide files.
- **Chat Bloat**: Emitting dozens of slide HTML fragments in the main conversation instead of delegating file generation to a subagent.
- **Floating Card Slide Drift**: Adding outer margins, rounded borders, or drop shadows to the slide container so slides look like floating cards in a gray void instead of a true full-bleed presentation.
- **Preset Fixation**: Imposing arbitrary palettes or fonts without grounding them in user discovery and `DECK-DESIGN.md`.
- **Markdown Leaking**: Leaving unparsed Markdown syntax (`**bold**`, `` `code` ``, `- list`) inside slide HTML fragments.
- **Inline Style Pollution**: Adding inline `style="..."` attributes or `<style>` blocks into slide fragments instead of `css/styles.css`.
- **Premature Print Export**: Triggering `window.print()` before fragments are fetched or before dynamic rendering (MathJax/Mermaid) settles.

---

## Disclosed References

- [ALIGNMENT.md](ALIGNMENT.md): Paced 3-round grilling protocol, storyline blueprints, and `DECK-DESIGN.md` schema.
- [ARCHITECTURE.md](ARCHITECTURE.md): Multi-file shell architecture, full-bleed viewport CSS, and PDF export engine.
- [SLIDE-FORMAT.md](SLIDE-FORMAT.md): Semantic slide fragment schemas, layout patterns, and pure HTML hygiene.
- [SCRIPTS.md](SCRIPTS.md): JS controller, slide loader lifecycle, and dynamic re-rendering engines.
