# Alignment & Grilling Protocol

Interactive prep session guide for discovering presentation intent, structuring the storyline, and locking in design decisions before generating slide code.

---

## Core Mental Model: The Pre-Flight Narrative Lock

Slides are purely the visual rendering layer; the narrative architecture must be locked in beforehand. Never generate slide files until the audience transformation, 1-sentence takeaway, and slide-by-slide Action Headlines are explicitly approved by the user.

---

## 1. Paced 3-Round Grilling Protocol

Ask questions **strictly one round per message turn** (1–2 concise questions max). Wait for the user's response before proceeding to the next round. Never dump all rounds at once.

### Round 1: Topic, Audience & Core Takeaway
*Goal: Understand the subject matter, the audience's starting mindset, and the single main message.*
- **Question 1**: *"What is the presentation topic/subject, and who is your target audience?"*
- **Question 2**: *"What is the single main takeaway or point you want them to remember if they forget everything else next week?"*

### Round 2: Delivery Modality & Slide Budget
*Goal: Lock in presentation format and length.*
- **Question 1**: *"Is this presented live with you speaking (visual backdrop, minimal text), or sent as a standalone read-ahead document (self-explanatory cards)?"*
- **Question 2**: *"How many slides are we aiming for (e.g., 5-slide crisp brief vs. 10-slide complete walkthrough)?"*

### Round 3: Slide Content Framework (Action Headlines) & Visual Vibe
*Goal: Synthesize Rounds 1 & 2 into a draft storyline and lock the visual mood.*
- **Action Headline Proposal**: The agent proposes a draft sequence of **Action Headlines** (active assertions that form a complete story when skimmed top-to-bottom):
  - *Slide 1: [Hero Title & Subtitle]*
  - *Slide 2: [Action Headline: Current problem or context]*
  - *Slide 3: [Action Headline: Core proposal or solution]*
  - *Slide 4: [Action Headline: Architecture / Proof / Data]*
  - *Slide 5: [Action Headline: Next steps or call to action]*
- **Question**: *"Does this headline sequence tell the exact story you want, and what visual tone and palette fits best (e.g. dark modern engineering vs. clean executive light)?"*

---

## 2. The `DECK-DESIGN.md` Blueprint Schema

Once Round 3 is confirmed, scaffold `DECK-DESIGN.md` in the presentation root as the single source of truth:

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
