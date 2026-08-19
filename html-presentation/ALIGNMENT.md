# Alignment & Grilling Protocol

Interactive prep session guide for discovering presentation intent, sifting raw human thoughts, structuring the storyline, and locking in design decisions before generating slide code.

---

## Core Posture: The Sifter & Mirror Pattern

Human thinking is exploratory, unstructured, and messy. When the user blurts out raw thoughts, half-formed ideas, or rambling context:
- **Never force rigid forms**: Do not demand bullet points or interrogate the user with rigid checklists.
- **Sift the stream**: Actively parse the raw input to extract: (1) Core Topic & Setting, (2) Audience Profile & Baseline Mindset, (3) 1-Sentence Core Takeaway ("Big Idea"), and (4) Specific raw slide ideas or anecdotes.
- **Reflect a structured mirror**: Synthesize the extracted pieces into a clean draft sequence of **Action Headlines** and reflect it back to the user in plain English for confirmation.

---

## 1. Paced Alignment Dialogue

Keep questions focused and paced (ask strictly 1–2 questions per turn; wait for response before advancing):

### Turn 1: Topic, Audience & Core Takeaway
*Goal: Anchor the subject matter, audience context, and the single main message.*
- **Prompt**: *"What is the presentation about, who is your audience, and what is the single main point you want them to walk away with?"*
- **Sifting Task**: Parse the user's response into Topic, Target Audience, and a tentative 1-sentence Big Idea.

### Turn 2: Delivery Modality & Slide Budget
*Goal: Lock in presentation format and length.*
- **Prompt**: *"Is this presented live with you speaking (visual punch, minimal text), or sent as a standalone read-ahead document (self-explanatory cards)? How many slides are we aiming for?"*

### Turn 3: Storyline Reflection (Action Headlines) & Visual Vibe
*Goal: Present the synthesized Slide Content Framework for user validation.*
- **Sifting Task**: Assemble the user's ideas into a sequence of **Action Headlines** (assertions that tell a complete story top-to-bottom):
  - *Slide 1: [Hero Title & Subtitle]*
  - *Slide 2: [Action Headline: Current challenge or context]*
  - *Slide 3: [Action Headline: Core proposal or mechanism]*
  - *Slide 4: [Action Headline: Architecture / Proof / Data]*
  - *Slide 5: [Action Headline: Next steps or call to action]*
- **Prompt**: Present the draft sequence and ask: *"Does this headline sequence tell the exact story you want, and what visual tone and palette fits best (e.g. dark modern engineering vs. clean executive light)?"*

---

## 2. The `DECK-DESIGN.md` Blueprint Schema

Once the storyline and design choices are agreed, lock them into `DECK-DESIGN.md` in the presentation root:

```markdown
# Deck Design Specifications

## 1. Narrative Blueprint & Storyline
- **Topic & Setting**: [Presentation subject and context]
- **Target Audience**: [Audience profile and baseline mindset]
- **The 1-Sentence "Big Idea"**: [Governing takeaway with clear stakes]
- **Modality**: [Live Companion Keynote | Standalone Read-Ahead]
- **Slide Count**: [Total number of slides]

## 2. Slide Content Framework (Action Headlines Sequence)
- **Slide 01**: [Hero Title] — Layout: `.slide-hero`
- **Slide 02**: [Action Headline: Lead Claim] — Layout: `.split-layout` (Problem contrast)
- **Slide 03**: [Action Headline: Lead Claim] — Layout: `.code-window` / `.mermaid` (Mechanics)
- **Slide 04**: [Action Headline: Lead Claim] — Layout: `.card-grid .col-3` (Metrics & Proof)
- **Slide 05**: [Action Headline: Lead Claim] — Layout: `.cta-layout` (Next steps)

## 3. Design Tokens & Typography
- `--bg-primary`: [Hex color]
- `--bg-surface`: [Hex color]
- `--text-primary`: [Hex color]
- `--text-muted`: [Hex color]
- `--accent-color`: [Hex color]
- `--border-color`: [Hex color]
- **Heading Font**: [Font family, weight]
- **Body Font**: [Font family, weight, line-height]
- **Code Font**: [Font family]
```
