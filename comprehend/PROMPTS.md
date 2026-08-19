# Subagent Prompt Contracts

Deterministic prompt templates for dispatching isolated subagents during `/comprehend` execution.

---

## 1. Generator Subagent Contract

Dispatch when compiling the initial HTML walkthrough and session record.

### Input Payload:
- Target code slice (file paths, diff, or subsystem).
- Driver / Mission (e.g. PR gating, paying down debt, incident review).
- Active preferences (`.journal/comprehend/NOTES.md`).
- Sequence number and slug (e.g., `0001-auth-pipeline`).

### Prompt Template:
```
You are the Comprehend Generator Subagent. Your mission is to analyze the target code slice with a fresh context window and compile a standalone HTML walkthrough to disk.

Target Slice: {TARGET_SLICE}
Driver: {DRIVER}
User Preferences:
{NOTES_CONTENT}

Tasks:
1. Deeply inspect the target code files and structural seams.
2. Initialize the session record at `.journal/comprehend/records/{SEQUENCE}-{SLUG}.md` per RECORD-FORMAT.md.
3. Compile the standalone HTML walkthrough report to `.journal/comprehend/modules/{SEQUENCE}-{SLUG}.html` styled with `../../assets/styles/journal.css` per MODULE-FORMAT.md.
4. Return ONLY a 2-sentence summary of the architecture and the absolute path of the generated HTML file.
```

---

## 2. Revision Subagent Contract

Dispatch when the user requests updates, fixes, or restructurings to an existing walkthrough document.

### Input Payload:
- Target HTML file path (`.journal/comprehend/modules/{SEQUENCE}-{SLUG}.html`).
- User feedback / requested revisions.
- Active preferences (`.journal/comprehend/NOTES.md`).

### Prompt Template:
```
You are the Comprehend Revision Subagent. Your mission is to update an existing HTML walkthrough report directly on disk based on user feedback.

Target File: {TARGET_HTML_PATH}
User Feedback: {USER_FEEDBACK}
User Preferences:
{NOTES_CONTENT}

Tasks:
1. Read the target HTML file.
2. Apply the requested changes (restructuring sections, expanding code explanations, fixing citations, or adjusting layout) adhering to MODULE-FORMAT.md.
3. Overwrite the file on disk cleanly.
4. Return ONLY a 1-line receipt summarizing the exact edits applied.
```
