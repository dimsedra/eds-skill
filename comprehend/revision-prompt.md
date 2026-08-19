# Comprehend Revision Subagent Prompt Template

Use this template when dispatching a subagent to revise an existing HTML walkthrough module based on user feedback.

```markdown
Subagent (role: "Comprehend Walkthrough Reviser", type: "self"):
  prompt: |
    You are revising an existing Comprehend Walkthrough Module for: [TARGET_SLICE_NAME]

    ## Inputs & Paths
    - Existing Module Path: [MODULE_HTML_PATH] (e.g. .journal/comprehend/modules/0001-[slug].html)
    - User Preferences File: [NOTES_FILE_PATH] (e.g. .journal/comprehend/NOTES.md)
    - User Feedback / Revision Instructions:
      [EXACT_USER_FEEDBACK_AND_REQUESTED_CHANGES]

    ## Your Job
    1. **Read Inputs:** Read the existing HTML module at [MODULE_HTML_PATH] and the user preferences in [NOTES_FILE_PATH].
    2. **Apply Revisions:** Update the HTML module directly on disk to incorporate the user's feedback:
       - Refactor or add code blocks with chunk-by-chunk interpretation guides (Input, Transformation, Invariant, Output).
       - Restructure sections, improve clarity, or adjust visual formatting as requested.
       - Preserve valid HTML, `<head>` styling links, and the two-section layout (`<hr>` divider between Agent walkthrough and User insights).
    3. **Self-Review:** Verify that all requested changes are present in the HTML file, the markup is valid, and the text is clear and readable.

    ## Contract & Constraints
    - **Never Spawn Subagents:** Perform all editing yourself.
    - **Write Directly to Disk:** Modify the file on disk. Never dump raw HTML markup into your final response.
    - **Clean Receipt Output:** Return ONLY this short contract (under 8 lines):
      - **Status:** DONE | BLOCKED | NEEDS_CONTEXT
      - **Module Path:** [file:///MODULE_HTML_PATH]
      - **Summary of Revisions:** 1–2 bullet points summarizing the changes made.
```
