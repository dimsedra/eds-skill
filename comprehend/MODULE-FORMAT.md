# MODULE Format (HTML Walkthrough Reports)

Specification for structuring and styling standalone walkthrough HTML documents compiled by `/comprehend`.

---

## Core Mental Model: Cold-Start Orientation

The document is designed for the user returning six weeks later with zero active context. It must orient the big picture before explaining mechanical details.

---

## Document Layout

An HTML walkthrough report consists of two distinct sections separated by a divider:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Walkthrough: {Slug}</title>
  <link rel="stylesheet" href="../../assets/styles/journal.css">
</head>
<body>
  <!-- SECTION 1: Agent Walkthrough -->
  <header>
    <h1>{Title}</h1>
    <p class="subtitle">{1-2 sentence high-level orientation & driver}</p>
  </header>

  <main>
    <section class="overview">
      <!-- High-level architectural role, entry/exit points -->
    </section>

    <section class="mechanics">
      <!-- Core logic, invariants, step-by-step traces with semantic anchors (file paths, function/class names, interface types) -->
    </section>
  </main>

  <hr>

  <!-- SECTION 2: User Insights & Breakthroughs -->
  <section class="user-insights">
    <h2>Realizations & Mental Model Shifts</h2>
    <!-- Core technical dilemmas explored and the realization that resolved them, written in the user's first-person perspective -->
  </section>
</body>
</html>
```

---

## Standards & Invariants

- **Semantic Code Anchoring**: Every code reference must cite stable semantic anchors (file path paired with named function, method, class, or type) rather than brittle line numbers.
- **Clean Semantic HTML**: Use semantic tags (`<header>`, `<main>`, `<section>`, `<aside>`, `<figure>`).
- **External Stylesheet**: Link `../../assets/styles/journal.css` without polluting the file with bloated inline `<style>` tags.
- **Perspective Separation**:
  - Top Section: Agent-authored structural walkthrough.
  - Bottom Section: Substantive technical insights in the user's voice (no third-person observer commentary).
- **Print & Responsive Ready**: Ensure clean rendering across display sizes and PDF export.
