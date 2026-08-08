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

### 2. Walking Through Code
You invoke the command and point it at the target file or diff:
```bash
/comprehend src/auth/session.ts
```
The agent explains the code in line with your preferences. You ask follow-up questions about why decisions were made, invariant logic, or dependencies.

### 3. Optional Walkthrough Docs
When the walkthrough dialogue finishes, the agent will flatly ask if you want to capture the explanation. If you accept, the agent formats a walkthrough HTML document under `.journal/comprehend/modules/` in **your own words** based on the conversation, linking the project-tailored `journal.css`.

---

## Usage Example (From Invocation to HTML Report)

Here is a complete walkthrough of gating a pull request diff before merging:

### 1. User Invokes the Skill
```bash
/comprehend I want to walk through the JWT validation diff in PR #14 before merging.
```

### 2. Agent Explains the Code
The agent inspects the target code and provides a clear, structured explanation tailored to your preferences:

> **Agent:** Here is the architecture of the JWT validation diff in `src/auth/session-store.ts`:
> 
> * **Entry Point:** `validateSessionToken()` ([src/auth/session-store.ts:L18](file:///src/auth/session-store.ts#L18)) parses the bearer token header.
> * **Load-Bearing Invariant:** Token expiration is now checked *before* database lookup ([src/auth/session-store.ts:L42](file:///src/auth/session-store.ts#L42)), avoiding unnecessary DB load on expired tokens.
> * **Decoupled Seam:** Signature verification was moved to a separate helper `verifySignature()` ([src/auth/crypto.ts:L10](file:///src/auth/crypto.ts#L10)).

### 3. Conversational Dialogue
You ask follow-up questions to understand why decisions were made or clarify non-obvious logic:

> **User:** *"Why did we move the token expiration check before the DB query?"*  
> **Agent:** *"Checking expiration in-memory eliminates DB lookups for expired requests, preventing potential DB denial-of-service under high request rates."*

### 4. Flat Offer & Optional HTML Report
When the walkthrough dialogue reaches a natural conclusion, the agent flatly offers to capture the walkthrough:

> **Agent:** *"Would you like me to capture this walkthrough in an HTML report, in your own words, for future reference?"*  
> **User:** *"Yes, please."*

### 5. Generated HTML Walkthrough Report
The agent writes the walkthrough document to `.journal/comprehend/modules/0001-jwt-validation.html`, styled with your project's custom `journal.css`:

```
.journal/
  assets/
    styles/journal.css              # Custom project stylesheet
  comprehend/
    records/0001-jwt-validation.md   # Session summary
    modules/0001-jwt-validation.html # Generated walkthrough HTML report
```

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
