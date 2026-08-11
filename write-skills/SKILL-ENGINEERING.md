# Skill Engineering Guidelines

Unified reference guide for preventing overfitting, establishing operational posture, and steering LLM attention in agent skills.

---

## 1. Preventing Overfitting

Guidelines to ensure agent skills remain universal, flexible, and free of single-project bias:

### Code Block Overfitting
- **Anti-Pattern:** Writing explicit code snippets, fixed CSS classes, or complete HTML templates inside skill files.
- **Why It Fails:** The LLM fixates on copy-pasting the exact code block, ignoring the user's distinct requirements.
- **Solution:** Describe architectural directions, design principles, and structural patterns in clear prose rather than rigid code blocks.

### Single-Project Over-Indexing
- **Anti-Pattern:** Elevating a specific user request from one session (e.g., hiding speaker notes in comments or using blue theme cards) into a mandatory global skill rule.
- **Why It Fails:** Forces irrelevant edge-case logic onto future users who have completely different needs.
- **Solution:** Frame project-specific needs as dynamic discovery options during Phase 1 alignment rather than mandatory rules.

### Preset & Color Hardcoding
- **Anti-Pattern:** Defining theme presets (e.g. "Academic = blue", "Corporate = slate") or hardcoding color hex codes.
- **Why It Fails:** Restricts creative flexibility and forces uniform styling across all outputs.
- **Solution:** Mandate dynamic token construction derived strictly from user discovery.

### Arbitrary Numeric Thresholds
- **Anti-Pattern:** Hardcoding arbitrary numbers (e.g. "10+ items = multi-file", "under 10 = single file").
- **Why It Fails:** Artificially limits decision making when real-world context demands a different structure.
- **Solution:** Use qualitative criteria based on project scale, modularity, and distribution requirements.

---

## 2. Skill Posture & LLM Nudging

Guidelines for steering LLM attention, establishing operational posture, and maintaining token efficiency:

### Leading Words & Posture Anchors
- Use compact, high-leverage terms pretrained in the model (e.g. *Discover First*, *Semantic Hygiene*, *Zero Hardcoding*, *Exact-Print*).
- Repeated leading words anchor regional reasoning across turns without requiring verbose explanations.

### Positive Behavioral Guardrails
- State target behaviors positively (what to do and why) rather than relying solely on prohibitions.
- Pair necessary prohibitions with the exact alternative action to prevent negative priming.

### Checkable Completion Criteria
- End each workflow phase with a clear, checkable completion criterion.
- Checkable criteria prevent premature completion and drive thorough execution legwork.

---

## 3. Information Hierarchy & Directory Structure

- **Root `SKILL.md`:** Entry point containing triggers, core posture, workflow phases, failure modes, and reference pointers.
- **Root Supplementary Files (`UPPERCASE-SLUG.md`):** Flat reference files living directly in the skill directory. Avoid nested subdirectories (`references/`) to reduce file depth.
- **Zero Fluff:** Omit generic introductory prose, pleasantries, or redundant summaries. Every line must serve predictability.
