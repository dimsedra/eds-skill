---
name: html-presentation
description: Build modular HTML presentation slide decks with responsive viewport fitting, custom keyboard navigation, and exact PDF/print export. Use when the user asks to create HTML slides, build a presentation deck, convert slides to HTML, generate slide presentations, or export HTML slides to PDF.
disable-model-invocation: false
---

# HTML Presentation

`html-presentation` provides the execution framework to engineer custom, web-based presentation decks for any domain, prompt context, or visual requirement.

---

## First Principle

The user's context, brand, and presentation goals dictate every architectural, aesthetic, and technical choice. Never apply fixed templates, preset color schemes, default fonts, or rigid UI structures. Always discover requirements first, then engineer a custom presentation system.

---

## Core Posture

- **Discover Before Building**: Clarify visual identity, aspect ratio, typography, interaction, and structural requirements before writing code.
- **Architect for Context**: Choose modular multi-file, single-file, or print-assembly patterns based on scale and output needs.
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
- Scaffold the presentation layout appropriate for deck scale.
- Construct custom CSS variables for colors, typography scaling, spacing, and surfaces derived entirely from user alignment.

### 3. Content Transformation
Transform presentation content into clean HTML:
- Use semantic structural elements for headers, content bodies, and footers.
- Map text formatting to native semantic tags (`<strong>`, `<em>`, `<code>`, `<ul>`).
- Format user-requested citations, tags, or metadata in appropriate structural zones.

### 4. Interaction & Export Verification
Apply patterns from [DECK-ENGINEERING.md](DECK-ENGINEERING.md):
- Bind keyboard navigation listeners and sync slide state with UI controls and hash URLs.
- Ensure dynamic elements (such as math formulas, diagrams, or code highlighters, if present) re-render on slide changes.
- Verify print/PDF export geometry and force exact color rendering (`print-color-adjust: exact`).

---

## Failure Modes

- **Preset Fixation**: Forcing specific colors, fonts, or component templates onto a project without user discovery.
- **Template Copying**: Copying fixed example structures instead of engineering a system tailored to the prompt.
- **Print Background Loss**: Omitting exact print color properties, causing browsers to strip backgrounds in PDF exports.

---

## Disclosed Reference

- [DECK-ENGINEERING.md](DECK-ENGINEERING.md) — Unified guide for architecture patterns, design system construction, interactive navigation, and exact PDF export.
