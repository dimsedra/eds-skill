# Deck Engineering Guidelines

## 1. Architectural Patterns

Match presentation deck architecture to project scale, distribution context, and output requirements:

### Modular Multi-File Pattern
- **Concept:** A central shell orchestrates dynamic fetching of standalone slide HTML files.
- **Application:** Multi-slide decks requiring isolated slide editing, clean file separation, or modular maintenance.
- **Center of Gravity:** Isolate slide content into dedicated files; maintain viewer state in a central shell.

Scaffold the deck as:

```
presentation/
  index.html              # shell: viewport, controls bar, CDN libs, loads css + js
  css/styles.css          # design tokens (:root) + component styles
  js/slide-loader.js      # fetches slides/slide-NN.html, re-renders MathJax/Mermaid, syncs hash + controls
  js/pdf-exporter.js      # print/PDF assembly
  js/main.js              # keyboard navigation, fullscreen, control bindings
  slides/slide-01.html    # one slide fragment per file, zero-padded
  slides/slide-02.html
  ...
  export_pdf.html         # print assembly root: fetches fragments, sizes @page, opens print dialog
  DECK-DESIGN.md          # the design language of this deck
```

Each `slides/slide-NN.html` is a self-contained `<section class="slide" id="slide-N">` fragment: optional `slide-cover` variant, a `<header>` (title + slide number), an `<article class="slide-body">` (lead text, grids, cards, callouts), and a `<footer>` (references, tags). Speaker notes live as HTML comments. Fragments stay content-only — the shell owns layout, state, and rendering.

### Single-File Dynamic Pattern
- **Concept:** All slide sections reside within a single HTML file, controlled via CSS visibility or DOM state toggles.
- **Application:** Compact presentations, rapid prototypes, or self-contained single-file distribution without web server constraints.
- **Center of Gravity:** Minimize fetch dependencies while preserving clean section boundaries.

### Dedicated Print Assembly Pattern
- **Concept:** A dedicated print document layout concatenates all slide sections sequentially into a continuous, page-broken structure.
- **Application:** Any deck requiring clean, multi-page PDF generation.
- **Center of Gravity:** Separate interactive screen presentation logic from multi-page document printing logic.

Scaffold `export_pdf.html` as a print-only root: it loads the same stylesheet and render libraries as the shell, fetches each `slides/slide-NN.html` fragment at runtime, wraps every fragment in a `.print-slide-page` sized to the deck's aspect ratio (page-break rules and exact color adjustment applied), typesets MathJax and renders Mermaid once assembled, waits for graphics to settle, then opens the print dialog.

Assemble by fetching fragments, never by inlining slide content into the export — a static copy duplicates content and goes stale the moment a slide changes.

---

## 2. Design System & Token Construction

Construct domain-agnostic presentation design systems derived strictly from user discovery:

### Design Language Document
- Once discovery settles the design direction, scaffold a `DECK-DESIGN.md` next to the deck files: palette, typography scale, aspect ratio, surfaces, spacing, and interaction choices.
- Write it for the user to read and steer — plain language, concrete tokens — not a technical appendix.
- Keep it the single source of truth: CSS tokens derive from it, and later slides and later sessions stay consistent with it.

Scaffold `DECK-DESIGN.md` with these sections, filled as alignment settles them:

1. **Deck Context** — purpose, delivery setting, audience, tone.
2. **Palette** — each color's role (primary, surfaces, text, semantic), its value, where it appears.
3. **Typography** — families and their roles (heading, body, mono), scale, weights, tracking.
4. **Aspect Ratio & Viewport** — target ratio and fitting strategy.
5. **Surfaces & Spacing** — cards, callouts, grids; padding and border tokens.
6. **Components** — the slide anatomy: header, body, footer, cover variant, tags, highlights.
7. **Interaction & Navigation** — keyboard map, controls, hash sync.
8. **Print & PDF** — assembly approach, page breaks, color preservation.

### Dynamic Token Construction
- Build CSS custom properties (`:root`) derived entirely from user alignment.
- Establish distinct token layers for canvas background surfaces, secondary containers, primary typography, muted labels, structural borders, and focal accents.
- Build tokens from discovery alone — presets make every deck identical and erase the user's context.

### Typography Scaling & Calibration
- Import typography families explicitly chosen by or aligned with the user.
- Pair heading sizes with tight tracking (letter-spacing) to keep title shapes crisp and avoid loose word wrapping.
- Maintain readable line-heights and visual contrast hierarchy across headings, body text, lists, and metadata.

### Spatial & Surface Chunking
- Group related ideas into visual surfaces (cards, callout blocks, columns, parameter grids) to prevent cluttered slide canvases.
- Maintain consistent padding, border tokens, and alignment across all slide layouts.
- Enforce strict viewport boundary containment so elements never cause unintended slide scrollbars.

---

## 3. Navigation & Interactive Controls

### Keyboard Navigation Engine
- Bind standard navigation triggers: forward (Right Arrow, Page Down, Space), backward (Left Arrow, Page Up), jump (Home, End), and fullscreen toggle (F key).
- Prevent default page scrolling when navigating, while maintaining form input accessibility.

### State & Hash Synchronization
- Synchronize current slide index with hash URLs (`#slide-XX`) for deep-linking and page refresh resilience.
- Keep visual controls (slide counters, dropdown jumpers, progress indicators) synchronized with current state.

### Dynamic Re-rendering Passes
- Automatically trigger typesetting or diagram rendering passes (MathJax, Mermaid, syntax highlighters) whenever slide DOM content updates.

---

## 4. High-Fidelity PDF & Print Export Strategy

### Dedicated Assembly & Page Breaks
- Assemble all slide sections sequentially into a continuous print document layout.
- Fetch slide fragments at runtime like the shell does — an inlined static copy goes stale the moment slides change.
- Set `@page` sizing to match target aspect ratio (e.g. 16:9 landscape) with zero margins.
- Apply CSS page-break rules (`page-break-after: always` and `page-break-inside: avoid`) to force exactly 1 slide per PDF page.

### Render Before Print
- Typeset formulas and diagrams (MathJax, Mermaid) after assembly, and let the renderer settle before opening the print dialog — printing before rendering yields blank formulas and empty diagrams.

### Exact Color Preservation
- Apply exact print color adjustment rules (`print-color-adjust: exact !important` and `-webkit-print-color-adjust: exact !important`) to root and slide containers.
- Preserves full-bleed background colors, gradients, and surface styling even when browser print dialogs have background graphics unchecked.

### Print Pitfalls to Avoid
- **Canvas Screenshot Fallback Trap:** Avoid using off-screen DOM positioning (`left: -9999px`) with canvas screenshot tools like `html2canvas`; off-screen rendering produces blank output. Use native browser print deck assembly instead.
- **Missing Color Adjustment:** Omitting print color adjustment rules strips background styling in PDF exports.
