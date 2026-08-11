# Deck Engineering Guidelines

Unified reference guide for architectural patterns, design system construction, interactive navigation, and exact PDF export for HTML slide decks.

---

## 1. Architectural Patterns

Match presentation deck architecture to project scale, distribution context, and output requirements:

### Modular Multi-File Pattern
- **Concept:** A central shell script orchestrates dynamic fetching of standalone slide HTML files.
- **Application:** Multi-slide decks requiring isolated slide editing, clean file separation, or modular maintenance.
- **Center of Gravity:** Isolate slide content into dedicated files; maintain viewer state in a central shell.

### Single-File Dynamic Pattern
- **Concept:** All slide sections reside within a single HTML file, controlled via CSS visibility or DOM state toggles.
- **Application:** Compact presentations, rapid prototypes, or self-contained single-file distribution without web server constraints.
- **Center of Gravity:** Minimize fetch dependencies while preserving clean section boundaries.

### Dedicated Print Assembly Pattern
- **Concept:** A dedicated print document layout concatenates all slide sections sequentially into a continuous, page-broken structure.
- **Application:** Any deck requiring clean, multi-page PDF generation.
- **Center of Gravity:** Separate interactive screen presentation logic from multi-page document printing logic.

---

## 2. Design System & Token Construction

Construct domain-agnostic presentation design systems derived strictly from user discovery:

### Dynamic Token Construction
- Build CSS custom properties (`:root`) derived entirely from user alignment.
- Establish distinct token layers for canvas background surfaces, secondary containers, primary typography, muted labels, structural borders, and focal accents.
- Never impose preset color schemes, default theme names, or arbitrary color hexes.

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
- Set `@page` sizing to match target aspect ratio (e.g. 16:9 landscape) with zero margins.
- Apply CSS page-break rules (`page-break-after: always` and `page-break-inside: avoid`) to force exactly 1 slide per PDF page.

### Exact Color Preservation
- Apply exact print color adjustment rules (`print-color-adjust: exact !important` and `-webkit-print-color-adjust: exact !important`) to root and slide containers.
- Preserves full-bleed background colors, gradients, and surface styling even when browser print dialogs have background graphics unchecked.

### Print Pitfalls to Avoid
- **Canvas Screenshot Fallback Trap:** Avoid using off-screen DOM positioning (`left: -9999px`) with canvas screenshot tools like `html2canvas`; off-screen rendering produces blank output. Use native browser print deck assembly instead.
- **Missing Color Adjustment:** Omitting print color adjustment rules strips background styling in PDF exports.
