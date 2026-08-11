# Writing HTML Reports

Convention guide for HTML walkthrough documents produced by `/comprehend`.

Produce durable, readable documents that pass the **"Cold-Me Six Weeks Later"** test: a user opening the report weeks later with zero active context can instantly gain high-level system re-orientation before diving into line-level mechanics.

---

## Behavioral Principles

### 1. Document Structure
- **Big-Picture Re-Orientation First**: Start the top section with a high-level architectural overview of the slice before line-level details.
- **Walkthrough at Top**: Present the primary agent explanation following the exact session dialogue progression (A → C → D).
- **`<hr>` Separator**: Place a horizontal rule between the primary walkthrough and the session log.
- **Session Log at Bottom**: Capture the user's actual questions, pushbacks, key breakthroughs, and dictated framing recorded during the conversation.

### 2. Aesthetic & Typography
- **Visual Consistency**: Adopt the typography, spacing, and font choices generated in the project's `.journal/assets/styles/journal.css`.
- **Side Notes & Callouts**: Use `<aside>` or `<figure>` elements for supplementary notes, definitions, or code callouts without breaking the narrative flow.
- **Readability**: Ensure a comfortable reading layout (optimal line length, clear headings, proper contrast).

### 3. Assets & Stylesheets
- **Link Shared Stylesheet**: Link the shared workspace stylesheet (`.journal/assets/styles/journal.css`).
- **Use Components**: Reference reusable component assets in `.journal/assets/` rather than inlining duplicated styles or scripts.

### 4. Print-Test Verification
- Ensure the HTML renders cleanly on screen and prints to PDF or paper without broken section headings or cluttered UI controls.
