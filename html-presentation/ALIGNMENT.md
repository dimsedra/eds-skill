# Alignment & Grilling Protocol

Interactive prep session guide for discovering presentation intent, sifting raw human thoughts, structuring the storyline, and locking in design decisions before generating slide code.

---

## Core Posture: The Sifter & Mirror Pattern

Human thinking is exploratory, unstructured, and messy. When the user blurts out raw thoughts, half-formed ideas, or rambling context:
- **Never force rigid forms**: Do not demand bullet points or interrogate the user with rigid checklists.
- **Sift the stream**: Actively parse the raw input to extract: (1) Core Topic & Setting, (2) Audience Profile & Baseline Mindset, (3) 1-Sentence Core Takeaway ("Big Idea"), and (4) Specific raw slide ideas or anecdotes.
- **Reflect a structured mirror**: Synthesize the extracted pieces into a clean draft sequence of **Action Headlines** and reflect it back to the user in plain English for confirmation.

---

## 1. The 4-Pass Funnel Alignment Dialogue

Structure the alignment as a funnel—moving from wide, loose exploration down to precise narrative and visual decisions. Ask questions strictly **one pass per message turn**; wait for response before advancing.

### Pass 1: The Open Brain Dump (Wide & Loose)
*Goal: Give the user full freedom to dump raw thoughts without interrogation pressure.*
- **Opening Invitation**: *"What do you have in mind for this presentation? Feel free to dump your raw thoughts, topic, target audience, rough ideas, or any specific points you want to cover."*
- **Sifting Task**: Actively parse the user's raw stream to extract tentative topic, audience angle, core thesis, and any specific slide anecdotes.

### Pass 2: Sift & Clarify (Target Missing Context)
*Goal: Mirror the extracted core back to the user and clarify only what's missing.*
- **Mirror**: Reflect back the synthesized topic and takeaway:
  *"Here is what I'm hearing: the core message is [1-sentence synthesis], aimed at [audience]."*
- **Targeted Clarification**: Ask only for missing parameters:
  *"To sharpen this: Is this presented live with you speaking (visual punch), or sent as a standalone read-ahead document? Roughly how many slides are we aiming for (e.g. 5-slide brief vs. 10-slide walkthrough)?"*

### Pass 3: Storyline & Slide Content Framework (Pure Narrative Lock)
*Goal: Validate and lock the slide-by-slide narrative before discussing visuals.*
- **Action Headlines Proposal**: Present the synthesized Slide Content Framework:
  - *Slide 1: [Hero Title & Subtitle]*
  - *Slide 2: [Action Headline: Core problem / context]*
  - *Slide 3: [Action Headline: Core proposal / mechanism]*
  - *Slide 4: [Action Headline: Proof / Architecture / Data]*
  - *Slide 5: [Action Headline: Next steps / Call to action]*
- **Validation Prompt**: *"Does this headline sequence tell the exact story you want, or should we swap, reorder, or adjust any point?"*

### Pass 4: Visual Styling & Theme (Look & Feel)
*Goal: Lock visual aesthetics once the storyline is settled.*
- **Prompt**: *"What visual tone and palette fits best for this deck? (e.g., Dark modern engineering with cyan accent, Clean editorial light with slate blue, or custom brand colors)?"*
- **Scaffold**: Write the approved narrative and visual tokens into `DECK-DESIGN.md` in the presentation root.

---

## 2. The `DECK-DESIGN.md` Blueprint Schema

Once Pass 4 is confirmed, scaffold `DECK-DESIGN.md` in the presentation root:

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
