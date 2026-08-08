# Writing HTML Reports

Convention guide for HTML walkthrough documents produced by `/comprehend`.

Focus on **agent behavior** when generating HTML walkthrough documents: produce durable, readable documents that serve as long-term reference for the user.

---

## Behavioral Principles

### 1. Document Structure
- **Walkthrough at Top**: Present the primary agent explanation and code walkthrough as structured, readable HTML.
- **`<hr>` Separator**: Place a horizontal rule between the primary walkthrough and the session log.
- **Session Log at Bottom**: Capture the user's actual questions, pushback, key breakthroughs, and moments of understanding recorded during the conversation.

### 2. Aesthetic & Typography
- **Visual Consistency**: Adopt the typography, spacing, and font choices generated in the project's `.journal/assets/styles/journal.css`.
- **Side Notes & Callouts**: Use `<aside>` or `<figure>` elements for supplementary notes, definitions, or code listings without breaking the narrative flow.
- **Readability**: Ensure a comfortable reading layout (optimal line length, clear headings, proper contrast).

### 3. Assets & Stylesheets
- **Link Shared Stylesheet**: Link the shared workspace stylesheet (`.journal/assets/styles/journal.css`).
- **Use Components**: Reference reusable component assets in `.journal/assets/` rather than inlining duplicated styles or scripts.

### 4. Print-Test Verification
- Ensure the HTML renders cleanly on screen and prints to PDF or paper without broken section headings or cluttered UI controls.
