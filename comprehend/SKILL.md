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

Every `/comprehend` invocation operates as a distinct, bounded **time block** powered by a clean-head subagent:

### 1. Session Framing & Subagent Dispatch (Start)
In the opening turn:
- Read `.journal/comprehend/NOTES.md` into context (or initialize it per [SETUP-FORMAT.md](SETUP-FORMAT.md) if missing) to load the user's active preferences.
- State the target code slice and dispatch a dedicated **Comprehend Generator Subagent** using template [generator-prompt.md](generator-prompt.md).
- The subagent:
  1. Inspects target code files, diffs, and architectural seams with zero context pollution.
  2. Initializes the session record (`.journal/comprehend/records/0001-<slug>.md`) per [RECORD-FORMAT.md](RECORD-FORMAT.md).
  3. Compiles the standalone HTML walkthrough report into `.journal/comprehend/modules/0001-<slug>.html` styled with `.journal/assets/styles/journal.css` per [MODULE-FORMAT.md](MODULE-FORMAT.md).
  4. Returns a lightweight receipt (output file paths + 2-sentence big-picture summary).

### 2. Report Delivery, Interactive Q&A & Module Revisions
Once the subagent completes:
- Present the clickable link to the user: `[Open Walkthrough: <slug>](file:///...)` alongside the 2-sentence big-picture summary.
- Invite the user to view the report in their browser and ask any targeted questions or probe edge-case invariants.
- Answer follow-up questions in short, bite-sized turns (1–2 paragraphs max) without polluting the chat with massive code dumps.
- **Handling User Feedback & Walkthrough Revisions**:
  - Update `.journal/comprehend/NOTES.md` inline so new preferences are permanently remembered.
  - **Never edit or regenerate the HTML module inline**: If the user requests module changes, additions, code-block restructuring, or formatting adjustments, dispatch a **Comprehend Revision Subagent** using template [revision-prompt.md](revision-prompt.md).
  - The revision subagent updates `.journal/comprehend/modules/0001-<slug>.html` on disk and returns a clean 1-line receipt, keeping our main conversation context pristine.

### 3. Session Wrap-up (Finish)
When dialogue finishes or the user indicates they are done:
- Synthesize any key breakthroughs or mental model shifts made during chat from the user's first-person perspective.
- Update the **Session Summary & Insights** section in the session record (`.journal/comprehend/records/0001-<slug>.md`) per [RECORD-FORMAT.md](RECORD-FORMAT.md) and append them to the bottom section of the HTML report.
- State where the session record and report were saved.

---

## Subagent Contracts & Dispatch Recipes

### 1. Generator Subagent Contract
- **Template:** [generator-prompt.md](generator-prompt.md)
- **Model Selection:** Inherit default or use standard/capable model for deep code analysis.
- **Inputs Handed to Subagent:** Target file paths/diff, `NOTES.md` path, `journal.css` path, output HTML and MD paths.
- **Subagent Mandate:** Inspects code -> Writes `records/0001-<slug>.md` -> Writes `modules/0001-<slug>.html` -> Returns receipt only.
- **Code Block Standard:** Breaks down code chunks using the 4-question framework:
  1. *What goes in? (Input)*
  2. *How is it transformed? (Transformation)*
  3. *What rule is guarded? (Invariant / Gatekeeper)*
  4. *What comes out? (Output / Action)*

### 2. Revision Subagent Contract
- **Template:** [revision-prompt.md](revision-prompt.md)
- **Model Selection:** Fast/Standard tier (targeted HTML refactoring).
- **Inputs Handed to Subagent:** Existing HTML path, `NOTES.md` path, exact user feedback text.
- **Subagent Mandate:** Reads HTML + feedback -> Rewrites `.html` module directly on disk -> Returns receipt only.


---

## Walkthrough Posture & Interaction Rules

### First Principle: You Explain, the User Owns
Comprehension is the user's. The subagent generates a spatial, persistent HTML map; you act as the interactive sounding board to clarify subtleties and validate mental models.

### Clean Context via Subagents
Never dump raw HTML markup or massive code traces directly into the parent chat. Delegating HTML compilation to an isolated subagent ensures:
- **Clean Head**: The subagent inspects the code with 100% fresh attention and zero historical context mud.
- **Token Efficiency**: The parent conversation remains fast, responsive, and unbloated for ongoing work.

### Two-Way Pacing: Never Monologue
When answering follow-up questions in chat, never dump massive walls of text.
- **One Slice at a Time:** Explain specific questions concisely (1–2 paragraphs max).
- **Pause and Yield:** End messages cleanly to yield the turn to the user.
- **User Steers:** Let the user react and guide which edge cases or invariants to explore.

### Single Source of Truth for Voice: `NOTES.md`
Tone, presentation style, and explanation structure are governed strictly by `.journal/comprehend/NOTES.md`.
- Both the parent agent and the generator subagent ingest `NOTES.md` to shape explanation depth and retention focus.
- Dynamically update `NOTES.md` whenever the user provides feedback per [SETUP-FORMAT.md](SETUP-FORMAT.md).

### Explain, Don't Quiz
You present structured code explanations and answer questions. You never interrogate, quiz, or grade checkpoint questions.

---

## The Ownership Workspace

The workspace is private; add `.journal/` to the project's `.gitignore` on first run.

```
.journal/comprehend/
  NOTES.md                # User preferences and key takeaways (see SETUP-FORMAT.md)
  records/*.md            # Session mission and summary records (see RECORD-FORMAT.md)
  modules/*.html          # Walkthrough HTML reports compiled by subagent (see MODULE-FORMAT.md)
  reference/*.html        # Glossaries, callouts, code-reading maps
.journal/assets/
  styles/journal.css      # Tailored stylesheet dynamically generated on setup
```

---

## Failure Modes of this Skill

- **Monologue Dump / Inline Generation Bloat**: Dumping raw HTML code or massive multi-page text into the parent chat instead of delegating report compilation to the subagent.
- **Inline Revision Bloat**: Attempting to rewrite or patch existing walkthrough `.html` files directly in the parent chat upon receiving user feedback instead of delegating the revision to a subagent.
- **Context Mud Drift**: Attempting to generate deep code walkthroughs inside a fatigued, 100k+ token parent session instead of using a fresh subagent.
- **Preferences Routing Drift / Unread NOTES.md**: Writing comprehend explanation preferences to global configuration files instead of `.journal/comprehend/NOTES.md`, or failing to pass `NOTES.md` to the subagent.
- **Observer Log Drift (Evaluator Tone)**: Documenting sessions as third-person teacher or auditor notes instead of recording substantive technical insights in the user's voice.
- **Robot Dashboard / Status Formatting**: Using rigid status tables or sterile emojis (🟢/🔴) to manage sessions.
- **Quiz / Checkpoint Drift**: Asking test questions or checkpoints. Stop quizzing; user drives questioning.
- **Mission Drift**: Scope changes without updating the session record's mission section.

---

## Disclosed Reference & Definitions

- [GLOSSARY.md](GLOSSARY.md): Detailed definitions of *Frontier*, *Signals*, *Walkthrough*, and *Desirable Difficulty*.
- [SETUP-FORMAT.md](SETUP-FORMAT.md): Guidelines for onboarding interviews and preference maintenance.
- [RECORD-FORMAT.md](RECORD-FORMAT.md): Specification for session mission and summary records.
- [MODULE-FORMAT.md](MODULE-FORMAT.md): Specification for Walkthrough HTML reports (structure, aesthetics, and styling).
