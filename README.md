# Comprehend Skill

Dialogue-based, conversational, two-way code walkthroughs tailored to your preferences and proficiency. Use it before the merge to understand the diff, or after to pay down comprehension debt.

This repository hosts `/comprehend` as a standalone, pluggable skill.

---

## Installation

Install the skill on your coding agent using `npx skills`:

```bash
npx skills@latest add dimsedra/eds-skill
```

---

## Why `/comprehend` Exists

In agent-led development, code is produced at an unprecedented speed, creating instant **comprehension debt** — code in your repo that you can't explain, defend in a review, or debug at 3 AM. 

`/comprehend` resolves this:
*   **Before the merge (Gating Mode):** Walk through and understand the diff so you can gate the change and defend the code in review before it ships.
*   **After the merge (Paying-down Mode):** Walk through existing code slices over multiple sessions, building long-term retention and ownership.

Comprehension belongs to the human. The agent's role is strictly to **inform and explain** code clearly, adapting to your preferences. The agent does not test, quiz, or grade you.

---

## How It Works

### 1. First-Run Setup & Dynamic CSS
On its first run in a project, `/comprehend` automatically:
- Scaffolds a private `.journal/` workspace (and appends it to `.gitignore`).
- **Dynamic CSS:** Inspects your project's code, structure, and styling to dynamically generate a clean, premium, highly readable CSS stylesheet tailored specifically to your project's aesthetic. This is written to `.journal/assets/styles/journal.css`.
- Runs a short onboarding interview to establish your preferred learning style (e.g., systemic/structural, step-by-step logic tracing, or conceptual metaphors) and saves it to `.journal/comprehend/NOTES.md`.

### 2. Bounded Session Time Block
Every `/comprehend` invocation runs as a distinct, bounded **time block**. The agent opens and closes the session conversationally (without sterile dashboards or emojis):

*   **Opening:** *"Opening a session for `src/auth/session-store.ts` (gating mode). Let's start with the token parsing entry point..."*
*   **Closing:** *"That wraps up this session for `src/auth/session-store.ts`. I've logged our session record to `.journal/comprehend/records/0001-jwt-validation.md` (and generated `.journal/comprehend/modules/0001-jwt-validation.html`)."*

---

## Usage Example (Session & HTML Report)

Here is a complete walkthrough showing natural session framing:

### 1. User Invokes & Agent Opens Session
```bash
/comprehend I want to walk through the JWT validation diff in PR #14 before merging.
```

> **Agent:** *"Opening a session for `src/auth/session-store.ts` (gating mode). Here is the entry point for JWT validation:"*
> 
> * **Entry Point:** `validateSessionToken()` ([src/auth/session-store.ts:L18](file:///src/auth/session-store.ts#L18)) parses the bearer token header.
> * **Load-Bearing Invariant:** Token expiration is checked *before* DB lookup ([src/auth/session-store.ts:L42](file:///src/auth/session-store.ts#L42)), avoiding unnecessary DB load on expired tokens.

### 2. Conversational Dialogue
You ask follow-up questions to understand decisions or non-obvious logic:

> **User:** *"Why did we move token expiration check before the DB query?"*  
> **Agent:** *"Checking expiration in-memory eliminates DB lookups for expired requests, preventing potential DB denial-of-service under high request rates."*

### 3. Flat Offer & Optional HTML Report
When the walkthrough dialogue finishes, the agent flatly offers to capture the walkthrough:

> **Agent:** *"Would you like me to capture this walkthrough in an HTML report, in your own words, for future reference?"*  
> **User:** *"Yes, please."*

### 4. Natural Session Wrap-Up
The agent writes `.journal/comprehend/modules/0001-jwt-validation.html` and closes the session:

> **Agent:** *"That wraps up this session for `src/auth/session-store.ts`. I've logged our session record to `.journal/comprehend/records/0001-jwt-validation.md` and saved the HTML report to `.journal/comprehend/modules/0001-jwt-validation.html`."*

---

## The Ownership Workspace

All comprehension progress is saved in a private workspace `.journal/` at the root of your project:

```
.journal/
  assets/
    styles/journal.css     # Stylesheet dynamically generated to match your project
  comprehend/
    MISSION.md             # The focus of your current walkthrough and success criteria
    NOTES.md               # Your active explanation preferences (continually refined by the agent)
    records/*.md           # Brief session records capturing the shape of walkthroughs
    modules/*.html         # Optional walkthrough documents in your own words
    reference/*.html       # Project-specific glossaries, invariants, and reading maps
```

---

## References

For deep-dive documentation on skill formats and behaviors:
*   [GLOSSARY.md](comprehend/GLOSSARY.md) - Standard definitions (frontier, signals, desirable difficulty, etc.).
*   [SETUP-FORMAT.md](comprehend/SETUP-FORMAT.md) - Guidelines for onboarding interviews and how the agent dynamically maintains `NOTES.md`.
*   [MISSION-FORMAT.md](comprehend/MISSION-FORMAT.md) - How `MISSION.md` is structured.
*   [RECORD-FORMAT.md](comprehend/RECORD-FORMAT.md) - Structure for markdown session records.
*   [MODULE-FORMAT.md](comprehend/MODULE-FORMAT.md) - Rules for generating walkthrough HTML documents.
*   [WRITING-HTML-REPORT.md](comprehend/WRITING-HTML-REPORT.md) - Layout, typography, and print-ready HTML conventions.
