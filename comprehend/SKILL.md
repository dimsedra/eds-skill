---
name: comprehend
description: User-invoked command (/comprehend) for two-way code walkthroughs. Use before merging to gate a diff or after to pay down comprehension debt.
disable-model-invocation: true
argument-hint: What code do you want to comprehend?
---

# Comprehend

`/comprehend` is a two-way code walkthrough tailored to the user's preferences (saved in `NOTES.md`) and proficiency. You present clear, structured code explanations; the user drives questioning and context.

---

## Triggers & Boundaries

### When to Invoke
Reach for this skill when the user requests pre-merge diff ownership or post-merge code comprehension.

### When NOT to Invoke
- The user just wants to ship code or run tests.
- The user just got a code review from a pull request.
- The user wants to learn a new *concept*, not understand existing code.
- The change is one-line or trivial, so a walkthrough is overkill.
- The user is exploring a brand-new idea with no code yet.

---

## Execution Modes

### Gating Mode (Before the Merge)
Single session, fast. You provide clear, structured explanations of the diff so the user understands what is shipping. The user asks questions whenever they want deeper context or edge-case clarification.

### Paying-down Mode (After the Merge)
Multi-session, paced. Walk through code over multiple sessions, one slice at a time, referencing earlier slices to build long-term retention.

---

## First-Run Setup & Onboarding

On first invocation in a new project, execute setup before starting the walkthrough:

1.  **Directories:** Create `.journal/comprehend/records/`, `.journal/comprehend/modules/`, `.journal/comprehend/reference/`, and `.journal/assets/styles/`.
2.  **Gitignore:** Append `.journal/` to the project's `.gitignore` file.
3.  **Dynamic CSS Generation:**
    *   Inspect the host project's files (languages, frameworks, themes, styling configurations).
    *   Dynamically generate a clean, readable CSS stylesheet tailored to the project (supporting a comfortable font family, responsive margins, clean headers, and code block styling).
    *   Write the CSS contents to `.journal/assets/styles/journal.css`.
4.  **Preference Onboarding:** Follow [SETUP-FORMAT.md](SETUP-FORMAT.md) to discover the user's explanation preference via a short interview and save it to `.journal/comprehend/NOTES.md`.

---

## Session Lifecycle (Time Block)

Every `/comprehend` invocation operates as a distinct, bounded **time block**.

### 1. Session Framing (Start)
In the opening turn, establish context naturally:
- Read `.journal/comprehend/NOTES.md` into context (or initialize it per [SETUP-FORMAT.md](SETUP-FORMAT.md) if missing) so your explanation style immediately aligns with the user's active preferences.
- Create or open the session record (`.journal/comprehend/records/0001-<slug>.md`) and initialize the **Session Mission** (Target Slice, Driver, Success Criterion) per [RECORD-FORMAT.md](RECORD-FORMAT.md).
- State the target code slice and active mode (Gating vs. Paying-down).
- Begin immediately with the first bite-sized entry point explanation.

### 2. Session Progression
Walk through the code 1–2 paragraphs at a time, yielding each turn to allow the user to ask questions and steer the focus.

### 3. Session Wrap-up (Finish)
Close the session cleanly when dialogue finishes:
- Synthesize session takeaways from the user's first-person perspective: document the core dilemma or question explored and the concrete technical realization that resolved it, avoiding empty third-person meta-summaries.
- Update the **Session Summary & Insights** section in the session record (`.journal/comprehend/records/0001-<slug>.md`) per [RECORD-FORMAT.md](RECORD-FORMAT.md).
- **Mandatory Offer:** Always explicitly ask the user if they would like an HTML walkthrough report created for this session before concluding.
- If the user accepts, generate the HTML report into `.journal/comprehend/modules/0001-<slug>.html` per [MODULE-FORMAT.md](MODULE-FORMAT.md).
- State where the session record and report (if generated) were saved.

---

## Walkthrough Posture & Interaction Rules

### First Principle: You Explain, the User Owns
Comprehension is the user's. Your job is to walk through the code with the user: not to write a walkthrough doc, not to summarise, not to fill in a journal. You inform; the user articulates.

### Two-Way Pacing: Never Monologue
A walkthrough is a two-way conversation, not a lecture. You must never dump a massive wall of text detailing entry points, edge-case invariants, and logic all at once.
- **One Slice at a Time:** Explain a single entry point or architectural seam concisely (1–2 paragraphs max).
- **Pause and Yield:** End messages cleanly to yield the turn to the user.
- **User Steers:** Let the user react, ask questions, or direct which part of the code to explore next before diving into deeper edge cases or invariants.

### Single Source of Truth for Voice: `NOTES.md`
Tone, presentation style, and explanation structure are governed strictly by `.journal/comprehend/NOTES.md`.
- Read `.journal/comprehend/NOTES.md` at the start of every session and shape your explanation depth, pacing, and retention focus accordingly.
- Dynamically update `NOTES.md` whenever the user provides feedback—whether given during an active walkthrough or received as out-of-session directives per [SETUP-FORMAT.md](SETUP-FORMAT.md). Never redirect comprehend explanation preferences to global agent configuration files.

### Explain, Don't Quiz
You present structured code explanations and pause. The user drives questioning; you never interrogate, quiz, or grade checkpoint questions.

### Concluding & Mandatory Report Offer
You do not generate an HTML report automatically, but you must **always ask**.
When the dialogue reaches a natural stopping point or the user indicates they are done, always explicitly ask if the user wants an HTML walkthrough report saved.
If the user accepts, generate the report (top: your walkthrough following the dialogue progression; bottom: user realizations and mental model shifts in the user's voice) into `.journal/comprehend/modules/0001-<slug>.html` per [MODULE-FORMAT.md](MODULE-FORMAT.md).

---

## The Ownership Workspace

The workspace is private; add `.journal/` to the project's `.gitignore` on first run.

```
.journal/comprehend/
  NOTES.md                # User preferences and key takeaways (see SETUP-FORMAT.md)
  records/*.md            # Session mission and summary records (see RECORD-FORMAT.md)
  modules/*.html          # Walkthrough HTML reports (see MODULE-FORMAT.md)
  reference/*.html        # Glossaries, callouts, code-reading maps
.journal/assets/
  styles/journal.css      # Tailored stylesheet dynamically generated on setup
```

You initialize mission info at session start and complete summary info at session end in `records/0001-<slug>.md`. See [RECORD-FORMAT.md](RECORD-FORMAT.md).

---

## Failure Modes of this Skill

- **Monologue Dump**: Outputting a massive wall of text covering entry points, edge cases, and invariants all at once. Fix: Explain one concise slice at a time (1–2 paragraphs) and pause to yield control to the user.
- **Preferences Routing Drift / Unread NOTES.md**: Writing comprehend explanation preferences to global configuration files instead of `.journal/comprehend/NOTES.md`, or failing to read `NOTES.md` before generating explanations. Fix: Treat `NOTES.md` as the exclusive single source of truth for comprehend explanation style.
- **Observer Log Drift (Evaluator Tone)**: Documenting sessions as third-person teacher or auditor notes (e.g., stating that the user examined or understood a topic) instead of recording the substantive technical insight in the user's voice.
- **Robot Dashboard / Status Formatting**: Using rigid status tables, emojis (🟢/🔴), or sterile templates to manage sessions. Fix: Express session boundaries dynamically as a peer engineer.
- **Drift into Doc-writing**: Drafting docs without walking through code first. Explain conversationally.
- **Rubber-stamp (pre-merge)**: Merging without walking through. Ensure entry points and invariants are explained conversationally.
- **Quiz / Checkpoint Drift**: Asking test questions or checkpoints. Stop quizzing; user drives questioning.
- **Skipping Report Offer**: Ending a session without explicitly asking the user if they would like an HTML walkthrough report created. Fix: Always make the offer clearly at session conclusion.
- **Theatre (post-merge)**: Un-visited walkthrough docs. Reference previous records to build connection.
- **Mission Drift**: Scope changes without updating the session record's mission section. Update the record when focus shifts.

---

## Disclosed Reference & Definitions

- [GLOSSARY.md](GLOSSARY.md): Detailed definitions of *Frontier*, *Signals*, *Walkthrough*, and *Desirable Difficulty*.
- [SETUP-FORMAT.md](SETUP-FORMAT.md): Guidelines for onboarding interviews and preference maintenance.
- [RECORD-FORMAT.md](RECORD-FORMAT.md): Specification for session mission and summary records.
- [MODULE-FORMAT.md](MODULE-FORMAT.md): Specification for Walkthrough HTML reports (structure, aesthetics, and styling).
