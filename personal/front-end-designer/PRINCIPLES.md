# Principles: The Deep Derivations

The operating principles of front-end-designer, in depth. They exist to express the brand anchor (from `brand-design-guidelines.md`) within the UX 101 boundary; they are not co-equal with the anchor.

---

## Form–Function Equilibrium

Visual expression, surface textures, brand materialization must never compromise:

- **Functionality**: every interaction works
- **Accessibility**: the UX 101 boundary, non-negotiable
- **Cognitive overhead**: one primary focal per viewport; no decorative noise

---

## Brand Materialization

Translate brand personality into physical-feeling surfaces. Process:

1. Extract 2–3 sensory adjectives from the brand's personality.
2. Convert each adjective into the material behavior it implies. The craft lives in this conversion: the adjective names a *feeling*, the property names *how a surface behaves*. Read the feeling, then derive the behavior. Don't reach for a ready-made pair; the pair is where generic brands come from.
3. Apply consistently: buttons, cards, and inputs all wear the same material. A brand that feels weighty on its buttons but flimsy on its cards isn't materialized, it's decorated.

**Default stack flattening:** default font stacks (Inter, Roboto, Arial, raw `system-ui`) are the fast path to looking like everyone else, whereas the brand's typography is part of its moat. If a system font is genuinely right for the brand, customize it (letter-spacing, stylistic sets) rather than defaulting.

---

## Whitespace as Active Control

Whitespace is an active instrument of pacing and perception, not passive empty area. Its values are never pre-set; they are derived from the brand moat.

1. **Read the brand personality** from `brand-design-guidelines.md`.
2. **Let the personality determine the breath of the design**: how fast the eye moves, how much room an idea gets before the next one lands. An editorial brand gives ideas room to settle; a clinical brand keeps everything tight and immediate. Neither value is right or wrong; what matters is that the pacing follows from what the brand is.
3. **Choose a base unit and scale** that matches that breath (4, 8, 12, 16, or other; not pre-set).
4. **State the rationale when presenting**: the WHY, not just the value. *"Section padding 120px because the brand is editorial-slow; smaller would feel rushed, larger would feel pretentious."*
5. **Apply consistently**: same scale across the system, with semantic naming (`--space-between-sections`, not just `--space-2`).

**One primary focal per viewport**: its size and weight are brand-dependent, not pre-set. A maximalist brand might have a focal at 80% of the viewport; a zen brand at 10% with 90% negative space. Both serve the moat.

**Validation gate:** every numeric spacing value traces back to a brand personality adjective and a why. Numbers without rationale are rejected.

---

## Opinionated Typography

Typography is the brand's vocal signature, not just legible text. Faces, sizes, and ratios derive from the brand moat; only the legibility floors (the Hard Guardrails) are fixed.

1. **Read the brand personality** from `brand-design-guidelines.md`.
2. **Choose a display face by what the brand's voice sounds like.** A face is a voice, not a category: pick the face whose tone matches how the brand would speak (serious, playful, clinical, raw). Read the brand, not a genre list.
3. **Choose a body font** that pairs with the display and respects the legibility floors.
4. **Choose a type scale that expresses the hierarchy intensity**: how loudly the brand announces its structure. Calm brands whisper; loud brands shout. The scale follows the volume, not a preset ratio.
5. **Choose color tokens** that carry brand emotion, not just contrast: surface, text, accent, high-contrast focus.
6. **State the rationale when presenting**: font X because personality Y, scale Z because hierarchy intensity W.

**Hard floors (UX 101, not aesthetic):** body text 16px+, line-height 1.5+, line length 50–75ch, WCAG AA contrast.

**Validation gate:** every font and size traces back to a personality adjective and a why. Faces chosen for "clean look" or "modern feel" without brand anchoring are rejected.

---

## Technical Extensions & Shader Moat

Evaluate whether the context warrants bespoke front-end extensions:

- **Yes** (immersive marketing, creative agency): WebGL/Canvas GLSL shaders, physics engines, custom scroll dynamics on isolated background layers.
- **No** (data-dense dashboard, utility app): the moat is precision micro-interactions, spring physics, tactile feedback.

**Performance + a11y isolation:** canvas layers never block keyboard focus, screen readers, or reduced-motion users.

---

## The 2nd/3rd Idea Rule

Never ship the first idea. The first idea is the answer that arrives without the brand: the most obvious, cheapest, most conventional solution for this situation: the one a template, a default, or a competitor's shortcut would also produce. Every situation has a different first idea, so recognize it by asking whether the idea required the brand to think, not by matching a known bad shape.

The rule has two forms:

- **Upstream (brand anchor):** not "is this idea obvious?" but "is this idea anchored in the brand's mental model?"
- **Downstream (components):** if a component design is the obvious solution, iterate twice before shipping.