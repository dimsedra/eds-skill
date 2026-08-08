# Setup & Preference Onboarding

Guidelines for the onboarding interview and dynamic maintenance of the user's explanation preferences.

---

## 1. Onboarding Interview (First-Run Setup)

If `.journal/comprehend/NOTES.md` does not exist or is empty, the agent must run the onboarding interview to establish the user's preferred code explanation approach.

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

Preferences are not static. The agent must continuously observe how the user reacts to explanations and dynamically update `NOTES.md`.

### Triggers for Updating Preferences
Update the preferences in `NOTES.md` when the user:
1.  **Explicitly requests a change:** "Explain this differently," "Avoid high-level summaries, just show me the code," or "Can you trace the exact method call?"
2.  **Demonstrates strong ownership signals:** If the user easily recites, pushbacks, or defends code when explained using a specific structure (e.g. flow diagrams), note that format as highly effective.
3.  **Shows confusion or fluency friction:** If the user struggles or asks for repeated clarification under the current explanation style, note the friction points to avoid (e.g., "Avoid jumping straight to lines of code without architectural context").

### Rules for Updating `NOTES.md`
*   **Preserve Custom User Notes:** Do not modify or delete bullet points that the user manually wrote or explicitly requested to keep.
*   **Incremental Refinement:** Add new insights as bullet points at the bottom or refine existing agent-written bullets.
*   **Keep it Actionable:** Every preference bullet must translate directly into how the agent structures its next message (e.g., "Use ASCII sequence diagrams for data flow").
*   **Limit Sprawl:** Keep the preferences to a maximum of 5 rungs. If a new insight is added, merge or prune less useful ones.
*   **Notify the User:** Briefly notify the user when updating `NOTES.md` (e.g., *"Note: I've updated your preferences in `NOTES.md` to prioritize data-flow diagrams based on our discussion."*). Do this flatly, without asking for confirmation unless unsure.
