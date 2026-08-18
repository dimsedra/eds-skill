# Setup & Preference Onboarding

Guidelines for the onboarding interview and dynamic maintenance of the user's explanation preferences.

---

## 1. Onboarding Interview (First-Run Setup)

If `.journal/comprehend/NOTES.md` does not exist or is empty, run the onboarding interview to establish the user's preferred code explanation approach.

### The Pitch
Ask the user one open-ended question to discover their preferred learning and explanation style. Avoid rigid forms; offer a few illustrative options to guide their response:

*   **Systemic / Structural:** Focus on how modules interact, architectural boundaries, and data flow.
*   **Step-by-Step / Line-by-Line:** Trace execution paths, inputs, outputs, and exact code lines.
*   **Analogy-Driven / Conceptual:** Use high-level design metaphors first, then anchor them in the code.
*   **Interactive Q&A:** Present very short, high-level summaries and let the user prompt for deeper drill-downs.

### Writing to `NOTES.md`
Format the user's response into 3–5 concise, highly actionable bullet points under a `# User Preferences` heading in `.journal/comprehend/NOTES.md`.

*   **Correct (actionable):** "Frame explanations as cohesive systems first, then trace individual components."
*   **Incorrect (generic):** "User likes diagrams and clean code."

---

## 2. Dynamic Preferences Maintenance (Subsequent Sessions)

Preferences are not static. Continuously observe how the user reacts to explanations and dynamically update `NOTES.md`.

### Triggers for Updating Preferences
Update the preferences in `NOTES.md` when the user:
1.  **Gives Out-of-Session Directives:** Direct feedback given outside of an active walkthrough targeting comprehend explanation style, conceptual depth, pacing, or retention goals must be written directly to `NOTES.md`.
2.  **Explicitly Requests Adjustments During Walkthrough:** Structural shifts requested during dialogue (such as asking for higher-level architectural context or deeper line execution traces).
3.  **Demonstrates Strong Ownership Signals:** If explanations structured in a specific pattern generate immediate clarity, synthesis, or effective questioning, record that approach as preferred.
4.  **Shows Fluency Friction:** If an explanation style causes repeated confusion or stalls momentum, record the friction point to avoid in future sessions.

### Rules for Updating `NOTES.md`
*   **Exclusive Destination:** All preferences governing `/comprehend` explanation depth, pacing, and retention focus belong strictly in `.journal/comprehend/NOTES.md`, never in global agent configuration files.
*   **Preserve Custom User Notes:** Do not modify or delete bullet points that the user manually wrote or explicitly requested to keep.
*   **Incremental Refinement:** Add new insights as bullet points at the bottom or refine existing agent-written bullets.
*   **Keep it Actionable:** Every preference bullet must translate directly into how you structure your next explanation turn.
*   **Limit Sprawl:** Keep the preferences lean. When a new insight arrives, merge or prune less useful bullets.
*   **Notify the User:** When you update `NOTES.md`, state briefly what changed and why. Don't ask for confirmation unless unsure.
