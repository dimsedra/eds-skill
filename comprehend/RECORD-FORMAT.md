# RECORD Format (Session Records)

Session records are concise markdown files saved at `.journal/comprehend/records/{SEQUENCE}-{SLUG}.md`.

---

## Record Schema

```md
---
date: {YYYY-MM-DD}
slice: {Target code slice or module}
mode: {gating | paying-down}
---

# Session Mission

## Target Slice
{1-2 sentences: target code, location, and functional purpose.}

## Driver
{1-2 sentences: PR diff gate, refactoring prep, bug incident, or debt paydown.}

## Success Criterion
{1 sentence: clear definition of successful comprehension.}

---

# Session Summary & Insights

## Walkthrough Report
- Report: `.journal/comprehend/modules/{SEQUENCE}-{SLUG}.html`

## Topics Explored
- {Topic 1}
- {Topic 2}

## Breakthroughs & Realizations (User POV)
- {Dilemma/Question explored → Concrete technical insight that resolved it}

## Next Steps
- {1 sentence on follow-up code slices to explore}
```

---

## Invariants

- **No Code Dumps**: Focus strictly on architectural drivers and cognitive breakthroughs.
- **User Perspective**: Document insights in the user's voice rather than passive observer logs (e.g., state the insight that clicked, not "user understood the code").
- **Zero Grading**: Never include scores, checkpoints, or fluency evaluations.
