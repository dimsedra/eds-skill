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
Before generating slide code, scaffold `DECK-DESIGN.md` in the presentation root. This file serves as the single source of truth for human steering and programmatic styling:

1. **Deck Context**: Purpose, audience, setting (pitch, lecture, defense, workshop), and tone.
2. **Palette**: Color roles (`--bg-primary`, `--bg-surface`, `--text-primary`, `--text-muted`, `--border-color`, `--accent-color`).
3. **Typography**: Font families (heading, body, code), modular scale, weights, and tracking.
4. **Aspect Ratio & Dimensions**: Target ratio (16:9 default: 16in × 9in / 1920px × 1080px) and fitting rules.
5. **Surfaces & Spacing**: Container styles, padding scale, border radius, and elevation tokens.
6. **Component Catalog**: Identified layout primitives (hero, split 2-col, metric cards, code window, comparison).
7. **Navigation & Controls**: Keyboard mapping, counter format, and dropdown behavior.
8. **Print & PDF**: Page dimensions, page breaks, and color preservation settings.

### Dynamic Token Construction
All values in `css/styles.css` derive from `DECK-DESIGN.md`. Avoid arbitrary hardcoded color hexes or ad-hoc margins across slide components.

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
