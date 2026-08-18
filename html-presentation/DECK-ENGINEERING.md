# Deck Engineering Guidelines

## 1. Architectural Patterns

Every presentation deck follows the modular multi-file architecture paired with a dedicated print assembly:

### Modular Multi-File Pattern
- **Concept:** A central shell orchestrates dynamic fetching of standalone slide HTML files.
- **Application:** All slide decks requiring clean file separation, isolated slide editing, and modular maintenance.
- **Center of Gravity:** Isolate slide content into dedicated files; maintain viewer state in a central shell.

Scaffold the deck as:

```
presentation/
  index.html              # shell: viewport, controls bar, CDN libs, loads css + js
  css/styles.css          # design tokens (:root) + component styles
  js/slide-loader.js      # fetches slides/slide-NN.html, re-renders MathJax/Mermaid/Prism, syncs hash + controls
  js/pdf-exporter.js      # print/PDF assembly
  js/main.js              # keyboard navigation, fullscreen, control bindings
  slides/slide-01.html    # one slide fragment per file, zero-padded
  slides/slide-02.html
  ...
  export_pdf.html         # print assembly root: fetches fragments, sizes @page, opens print dialog
  DECK-DESIGN.md          # the design language of this deck
```

Each `slides/slide-NN.html` is a self-contained `<section class="slide" id="slide-N">` fragment structured with semantic HTML tailored to the slide's specific purpose (e.g., headings, paragraphs, lists, figures, `<pre><code class="language-*">` code blocks, or modular content containers). Speaker notes live as HTML comments if needed. Fragments stay content-only; the shell owns layout, state, and rendering. Slide fragments are pure HTML documents: never leave raw Markdown formatting inside them (convert `**bold**`, `*italic*`, `` `code` ``, `[text](url)` to native HTML tags). Slide fragments must also contain zero inline CSS or `<style>` blocks—all layout, spacing, colors, and component styles must reside in `css/styles.css` so slide markup remains clean and easy for humans to read and edit.

### Dedicated Print Assembly Pattern
- **Concept:** A dedicated print document layout concatenates all slide sections sequentially into a continuous, page-broken structure.
- **Application:** Generating clean, multi-page PDF exports for the deck.
- **Center of Gravity:** Separate interactive screen presentation logic from multi-page document printing logic.

Scaffold `export_pdf.html` as a print-only root: it loads the same stylesheet and render libraries as the shell, fetches each `slides/slide-NN.html` fragment at runtime, wraps every fragment in a `.print-slide-page` sized to the deck's aspect ratio (page-break rules and exact color adjustment applied), typesets MathJax, renders Mermaid, and highlights Prism code blocks once assembled, waits for graphics to settle, then opens the print dialog.

Assemble by fetching fragments, never by inlining slide content into the export, as a static copy duplicates content and goes stale the moment a slide changes.

---

## 2. Design System & Token Construction

Construct domain-agnostic presentation design systems derived strictly from user discovery:

### Design Language Document
- Once discovery settles the design direction, scaffold a `DECK-DESIGN.md` next to the deck files: palette, typography scale, aspect ratio, surfaces, spacing, and interaction choices.
- Write it for the user to read and steer in plain language with concrete tokens, not as a technical appendix.
- Keep it the single source of truth: CSS tokens derive from it, and later slides and later sessions stay consistent with it.

Scaffold `DECK-DESIGN.md` with these sections, filled as alignment settles them:

1. **Deck Context**: purpose, delivery setting, audience, tone.
2. **Palette**: each color's role (primary, surfaces, text, semantic), its value, where it appears.
3. **Typography**: families and their roles (heading, body, mono), scale, weights, tracking.
4. **Aspect Ratio & Viewport**: target ratio and fitting strategy.
5. **Surfaces & Spacing**: containers, spacing scale, padding, and border tokens.
6. **Components**: reusable slide patterns and components identified during discovery (e.g., slide variants, layouts, callouts, media blocks).
7. **Interaction & Navigation**: keyboard map, controls, hash sync.
8. **Print & PDF**: assembly approach, page breaks, color preservation.

### Dynamic Token Construction
- Build CSS custom properties (`:root`) derived entirely from user alignment.
- Establish distinct token layers for canvas background surfaces, secondary containers, primary typography, muted labels, structural borders, and focal accents.
- Build tokens from discovery alone, because presets make every deck identical and erase the user's context.

### Typography Scaling & Calibration
- Import typography families explicitly chosen by or aligned with the user.
- Tune heading sizes, tracking (letter-spacing), and line-heights to maintain strong hierarchy and prevent awkward line wraps.
- Maintain readable line-heights and visual contrast hierarchy across headings, body text, lists, and metadata.

### Spatial & Surface Chunking
- Group related ideas logically to maintain clear visual hierarchy and prevent cluttered slide canvases.
- Maintain consistent padding, border tokens, and alignment across all slide layouts.
- Enforce strict viewport boundary containment so elements never cause unintended slide scrollbars.

---

## 3. Navigation & Interactive Controls

### Shell & Controller Architecture
Structure the presentation shell and scripts with clear separation of responsibilities:
- **Viewer Shell (`index.html`)**:
  - Encapsulates `<div id="presentation-app">`.
  - Main viewport: `<main class="slide-viewport"><div id="slide-container"></div></main>`.
  - Floating controls bar: `<nav class="controls-bar">` containing:
    - Previous button (`#btn-prev`)
    - Slide counter display (`#slide-counter-display`, e.g., `1 / 20`)
    - Slide jump dropdown (`#slide-select-dropdown`)
    - Next button (`#btn-next`)
    - Fullscreen toggle button (`#btn-fullscreen`)
    - PDF export trigger (`#btn-export-pdf`, opens `export_pdf.html` in a new tab)

### Slide Loader Engine (`js/slide-loader.js`)
Maintain presentation state in `window.SlideLoader`:
- Properties: `totalSlides`, `currentSlide`.
- `loadSlide(index)`:
  - Fetches zero-padded fragment path `slides/slide-NN.html`.
  - Injects HTML into `#slide-container`.
  - Executes dynamic re-rendering passes (MathJax, Mermaid, Prism).
  - Updates counter text (`index / totalSlides`) and dropdown selected value.
  - Updates URL hash: `window.location.hash = 'slide-' + index`.
- `nextSlide()` and `prevSlide()`: Bounds-checked step methods.

### Keyboard & Event Controller (`js/main.js`)
- Populate `#slide-select-dropdown` dynamically from `1` to `totalSlides`.
- Bind button listeners: next, prev, fullscreen (`requestFullscreen()` / `exitFullscreen()`), and export PDF.
- Bind keyboard listeners (ignoring input/select focus):
  - Forward: `ArrowRight`, `PageDown`, `Space`
  - Backward: `ArrowLeft`, `PageUp`
  - Jump: `Home` (slide 1), `End` (last slide)
  - Fullscreen: `F` key
- Read initial hash on load (`window.location.hash.match(/slide-(\d+)/)`) and load initial slide.

### Dynamic Re-rendering Passes
Automatically trigger typesetting, diagram rendering, and syntax highlighting passes whenever slide DOM content updates:
- **MathJax**: `if (window.MathJax?.typesetPromise) window.MathJax.typesetPromise([container])`
- **Mermaid**: `if (window.mermaid) window.mermaid.run({ nodes: container.querySelectorAll('.mermaid') })`
- **Prism**: `if (window.Prism) Prism.highlightAllUnder(container)`

---

## 4. High-Fidelity PDF & Print Export Strategy

### Dedicated Assembly Architecture (`export_pdf.html`)
Scaffold `export_pdf.html` as an automated, multi-page print document:
1. Include the deck stylesheet (`css/styles.css`) and render library CDN scripts (MathJax, Mermaid, Prism).
2. Render a temporary `#loading-status` notice (hidden automatically on `@media print`).
3. Root container: `<div id="pdf-print-deck"></div>`.
4. Script sequentially fetches every slide (`slides/slide-01.html` to `slides/slide-NN.html`), wraps each in a `<div class="print-slide-page">`, and appends to `#pdf-print-deck`.
5. Run all async rendering passes (`await MathJax.typesetPromise`, `await mermaid.run`, `Prism.highlightAll`).
6. **Mandatory graphics pause**: `await new Promise(r => setTimeout(r, 1000))` to guarantee web fonts, formulas, and SVG diagrams settle before the print dialog opens.
7. Hide the loading notice and trigger `window.print()`.

### Exact CSS Print Rules
Embed these strict styling rules inside `export_pdf.html`:

```css
@page {
    size: 16in 9in; /* Match 16:9 landscape aspect ratio */
    margin: 0;
}

html, body {
    width: 100%;
    height: auto;
    overflow: visible !important; /* Critical: allows multi-page print flow */
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

### Print Pitfalls to Avoid
- **Blank Screen / Premature Print:** Calling `window.print()` synchronously before fragments are fetched or before MathJax/Mermaid finishes rendering produces a blank white PDF. Always `await` all fetches, rendering promises, and a 1000ms settlement delay.
- **Overflow Lock Truncation:** Setting `overflow: hidden` or `height: 100vh` on `html`/`body` in print mode locks the viewport to page 1 and truncates all subsequent slides. Always set `overflow: visible !important; height: auto;`.
- **Dimension & Margin Mismatch:** Using relative units (`100vw`/`100vh`) instead of fixed physical inch dimensions matching `@page` (`16in 9in`) causes browser print engines to insert unwanted blank interstitial pages.
- **Canvas Screenshot Fallback Trap:** Avoid using off-screen DOM positioning (`left: -9999px`) with canvas screenshot tools like `html2canvas`; off-screen rendering produces blank output. Use native browser print deck assembly instead.
