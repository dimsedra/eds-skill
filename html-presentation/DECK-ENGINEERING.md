# Deck Engineering Guidelines

Guidelines for presentation architecture, design token contracts, and high-fidelity PDF export.

---

## 1. Modular Multi-File Architecture

Every slide deck uses a modular multi-file structure separating presentation shell, styles, scripts, slide content, and print assembly.

### File Tree Layout

```
presentation/
  index.html              # Viewer shell: viewport, controls bar, CDN libs, loader
  css/styles.css          # Design tokens (:root) + layout and component styles
  js/slide-loader.js      # Slide loader: fragment fetcher, hash sync, dynamic re-rendering
  js/main.js              # Keyboard navigation, dropdown, and UI event controller
  slides/slide-01.html    # Zero-padded standalone slide fragments
  slides/slide-02.html
  ...
  export_pdf.html         # Dedicated print assembly root for PDF generation
  DECK-DESIGN.md          # Design token and layout specification
```

### Separation of Concerns
- **Shell (`index.html`)**: Mounts the presentation application, provides the slide viewport (`#slide-container`), and hosts navigation controls.
- **Styles (`css/styles.css`)**: Defines CSS custom properties on `:root` and reusable component classes.
- **Fragments (`slides/slide-NN.html`)**: Pure semantic HTML containing slide content only. Zero inline styles or script tags.
- **Export Root (`export_pdf.html`)**: Assembles all fragments at runtime into a multi-page printable document.

---

## 2. Design System & Token Construction

### The `DECK-DESIGN.md` Contract
Before generating slide code, scaffold `DECK-DESIGN.md` in the presentation root. This file serves as the single source of truth for both narrative structure and programmatic styling:

#### Part A: Narrative Blueprint & Slide Content Framework
1. **Topic & Audience**: Topic, setting, audience profile, and their baseline mindset.
2. **The 1-Sentence "Big Idea"**: The single governing takeaway the audience must remember.
3. **Delivery Modality & Budget**: Live spoken companion (minimal text, visual punch) vs. Standalone read-ahead document (structured detail), plus locked slide count.
4. **Slide Content Framework (Action Headlines Sequence)**:
   - Every slide defined by an **Action Headline** (active assertion, e.g. *"Isolated Subagents Cut Chat Clutter by 80%"*).
   - Reading headlines from Slide 1 to Slide $N$ forms a complete, coherent narrative (the 30-second skim test).
   - Mapping each headline to its supporting proof layout (Hero, Split 2-Col, Metric Grid, Code Window, Architecture Diagram).

#### Part B: Design Tokens & Visual Hierarchy
1. **Palette**: Color roles (`--bg-primary`, `--bg-surface`, `--text-primary`, `--text-muted`, `--border-color`, `--accent-color`).
2. **Typography**: Font families (heading, body, code), modular scale, weights, and tracking.
3. **Aspect Ratio & Dimensions**: Target ratio (16:9 default: 16in × 9in / 1920px × 1080px) and full-bleed fitting rules.
4. **Surfaces & Spacing**: Internal slide padding, component layout classes, and clean contrast.

### Dynamic Token Construction
All values in `css/styles.css` derive directly from `DECK-DESIGN.md`. Avoid arbitrary hardcoded color hexes or ad-hoc margins across slide components.

### Full-Bleed Viewport Architecture (Zero Floating Cards)
To ensure slides render as a true full-bleed presentation on screen and in fullscreen:

1. **Root & Viewport Invariants**:
   ```css
   html, body {
       margin: 0;
       padding: 0;
       width: 100vw;
       height: 100vh;
       overflow: hidden;
       background: var(--bg-primary);
   }

   #slide-container, .slide {
       width: 100vw;
       height: 100vh;
       margin: 0;
       box-sizing: border-box;
       overflow: hidden;
       position: relative;
   }
   ```
2. **Prohibited Card Effects on Slide Frame**:
   - **No Outer Margins**: Never add `margin: 2rem auto` or `max-width: 1200px` to `#slide-container` or `.slide`.
   - **No Frame Shadows or Rounded Corners**: Never apply `border-radius` or `box-shadow` to the root `.slide` element.
3. **Internal Content Padding**: Content breathing room is achieved purely through internal slide padding (e.g. `padding: 4rem 6rem;` on `.slide` or `.slide-content`), ensuring the slide background always touches every display edge.

---

## 3. High-Fidelity PDF & Print Export Engine

### Dedicated Runtime Assembly (`export_pdf.html`)
To prevent stale duplicate markup, `export_pdf.html` fetches every slide fragment dynamically at export time:

1. Loads `css/styles.css` and CDN libraries (MathJax, Mermaid, Prism).
2. Displays a temporary `#loading-status` banner (hidden automatically in print media).
3. Sequentially fetches `slides/slide-01.html` through `slides/slide-NN.html`.
4. Wraps each fragment inside a `.print-slide-page` container appended to `#pdf-print-deck`.
5. Executes asynchronous typesetting and diagram rendering passes (`MathJax.typesetPromise`, `mermaid.run`, `Prism.highlightAll`).
6. **Mandatory graphics pause**: `await new Promise(resolve => setTimeout(resolve, 1000))` ensures web fonts, SVGs, and formulas settle before invoking `window.print()`.

### Exact CSS Print Rules

Embed these critical styles inside `export_pdf.html`:

```css
@page {
    size: 16in 9in; /* Match presentation aspect ratio */
    margin: 0;
}

html, body {
    width: 100%;
    height: auto;
    overflow: visible !important; /* Allows multi-page print flow */
    background: #ffffff;
    -webkit-print-color-adjust: exact !important;
    print-color-adjust: exact !important;
}

#pdf-print-deck {
    width: 100%;
    display: flex;
    flex-direction: column;
}

.print-slide-page {
    width: 16in;
    height: 9in;
    page-break-after: always;
    page-break-inside: avoid;
    box-sizing: border-box;
    overflow: hidden;
    position: relative;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    -webkit-print-color-adjust: exact !important;
    print-color-adjust: exact !important;
}

@media print {
    .print-loading-notice {
        display: none !important;
    }
}
```

### Critical Print Guardrails
- **No Overflow Locking**: Never apply `overflow: hidden` or `height: 100vh` to `html`/`body` in print mode (locks output to page 1).
- **Physical Print Units**: Use explicit inch units (`16in 9in`) matching `@page` to prevent empty interstitial pages.
- **Exact Color Preservation**: Always declare `-webkit-print-color-adjust: exact !important` and `print-color-adjust: exact !important`.
