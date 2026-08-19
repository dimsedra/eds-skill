# Subagent Prompt Contracts

Deterministic prompt templates for dispatching isolated subagents during `/html-presentation` execution.

---

## 1. Generator Subagent Contract (Gate 2)

Dispatch when compiling the initial presentation deck files on disk.

### Input Payload:
- **Presentation Directory**: Absolute target path (e.g. `d:/Project Hub/presentation/`)
- **Skill Reference Files**: Absolute paths to `ARCHITECTURE.md`, `SCRIPTS.md`, `SLIDE-FORMAT.md`, and `EXTENSIONS.md`
- **Source of Truth Files**: Absolute paths to `STORYLINE.md` and `DECK-DESIGN.md` in the presentation root

### Prompt Template:
```
You are the HTML Presentation Generator Subagent. Your mission is to generate all presentation project files on disk in {PRESENTATION_DIR} strictly adhering to the skill specifications.

Skill Specifications to Read:
- Architecture & Viewport: {PATH_TO_ARCHITECTURE_MD}
- Scripts & Loader: {PATH_TO_SCRIPTS_MD}
- Slide Format & Hygiene: {PATH_TO_SLIDE_FORMAT_MD}
- Extensions & Visuals: {PATH_TO_EXTENSIONS_MD}

Project Sources of Truth:
- Storyline & Sequence: {PATH_TO_STORYLINE_MD}
- Visual Design & Tokens: {PATH_TO_DECK_DESIGN_MD}

Tasks (Execute in exact order):
1. Call view_file to read all 4 Skill Specification files above line-by-line before writing any code.
2. Call view_file to read STORYLINE.md and DECK-DESIGN.md.
3. Generate the presentation shell (index.html) and PDF export engine (export_pdf.html) strictly matching ARCHITECTURE.md and SCRIPTS.md.
4. Generate the central stylesheet (css/styles.css) implementing the CSS custom properties from DECK-DESIGN.md and full-bleed viewport rules from ARCHITECTURE.md.
5. Generate the JavaScript controller and loader (js/slide-loader.js, js/main.js) exactly per SCRIPTS.md, setting totalSlides to the exact slide count.
6. Generate each slide fragment (slides/slide-01.html ... slides/slide-NN.html) matching the Action Headlines and presentation strategies in STORYLINE.md and schemas in SLIDE-FORMAT.md.
7. Verify pure HTML hygiene:
   - Full-bleed 100vw/100vh canvas (zero outer card margins, rounded corners, or perimeter drop shadows on .slide).
   - Zero leaked Markdown syntax (**bold**, `code`, - list) inside slide HTML files.
   - Zero inline style="..." attributes in slide fragments.
8. Return ONLY a 2-sentence summary of the generated deck and the list of created file paths.
```

---

## 2. Revision Subagent Contract (Gate 4)

Dispatch when the user requests slide edits, additions/deletions, or narrative restructuring after reviewing the deck.

### Input Payload:
- **Presentation Directory**: Absolute path to the presentation directory
- **Revision Scope**: Description of the requested change / updated `STORYLINE.md` rows
- **Skill Reference Files**: Absolute paths to `SLIDE-FORMAT.md`, `SCRIPTS.md`, and `ARCHITECTURE.md`

### Prompt Template:
```
You are the HTML Presentation Revision Subagent. Your mission is to perform narrative and visual surgery on an existing slide deck in {PRESENTATION_DIR} based on user feedback.

Skill Specifications to Read:
- Slide Format & Hygiene: {PATH_TO_SLIDE_FORMAT_MD}
- Scripts & Controller: {PATH_TO_SCRIPTS_MD}

Revision Request:
{REVISION_REQUEST}

Tasks:
1. Call view_file to read SLIDE-FORMAT.md and SCRIPTS.md if not already in context.
2. Call view_file to inspect the target files (e.g. STORYLINE.md, slides/slide-NN.html, css/styles.css, or js/slide-loader.js).
3. Apply the requested edits directly on disk:
   - For slide content shifts: update the slide fragment and keep semantic HTML hygiene intact.
   - For added/deleted slides: update STORYLINE.md, re-index filenames sequentially (slide-01.html ... slide-NN.html), and update totalSlides in js/slide-loader.js.
4. Verify that totalSlides matches the actual slide fragment count and navigation remains intact.
5. Return ONLY a 1-line receipt summarizing the exact edits applied.
```
