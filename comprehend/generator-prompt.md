# Comprehend Generator Subagent Prompt Template

Use this template when dispatching a subagent to analyze code and generate the initial walkthrough module and session record.

```markdown
Subagent (role: "Comprehend Walkthrough Generator", type: "research" or "self"):
  prompt: |
    You are generating a Comprehend Walkthrough Module and Session Record for: [TARGET_SLICE_NAME]

    ## Target Code & Inputs
    - Target Files / Diff: [LIST_OF_FILES_OR_DIFF_DESCRIPTION]
    - User Preferences File: [NOTES_FILE_PATH] (e.g. .journal/comprehend/NOTES.md)
    - Shared CSS Stylesheet: [CSS_FILE_PATH] (e.g. .journal/assets/styles/journal.css)
    - Output Module Path: [MODULE_HTML_PATH] (e.g. .journal/comprehend/modules/0001-[slug].html)
    - Output Record Path: [RECORD_MD_PATH] (e.g. .journal/comprehend/records/0001-[slug].md)

    ## Your Job
    1. **Read Preferences First:** Read [NOTES_FILE_PATH] to anchor the explanation depth, mental model, and tone to the user's preferences.
    2. **Analyze the Code:** Inspect the target code files thoroughly. Identify the entry points, data transformations, gatekeepers/invariants, and architectural seams.
    3. **Initialize Session Record:** Create [RECORD_MD_PATH] following RECORD-FORMAT.md with the session Mission (Target Slice, Driver, Success Criterion).
    4. **Compile HTML Walkthrough Module:** Write the complete, standalone HTML walkthrough directly to [MODULE_HTML_PATH] following MODULE-FORMAT.md:
       - Link [CSS_FILE_PATH] in the `<head>`.
       - **Top Section (Agent-Authored):**
         - High-level system overview ("Cold-Me Six Weeks Later" rule).
         - Structured code breakdown tailored to user preferences.
         - Chunk-by-chunk code blocks with interpretation guides (Input -> Transformation -> Invariant/Gatekeeper -> Output).
         - Exact `file:line` clickable citations.
       - **Bottom Section (User's Voice):** Realizations, key dilemmas explored, and concrete technical insights.
    5. **Self-Review:** Ensure the HTML is valid, links are clickable, and all target code mechanics are accurately explained without fluff.

    ## Contract & Constraints
    - **Never Spawn Subagents:** Perform all analysis and file creation yourself.
    - **Write Directly to Disk:** Write the complete HTML and MD files to disk. Never dump raw HTML markup or massive code blocks in your final chat reply.
    - **Clean Receipt Output:** Return ONLY this short contract (under 10 lines):
      - **Status:** DONE | BLOCKED | NEEDS_CONTEXT
      - **Module Path:** [file:///MODULE_HTML_PATH]
      - **Record Path:** [file:///RECORD_MD_PATH]
      - **Big-Picture Summary:** 2 sentences in plain English explaining what was covered.
```
