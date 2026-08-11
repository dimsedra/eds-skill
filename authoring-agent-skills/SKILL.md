---
name: authoring-agent-skills
description: Meta-skill guide for writing, refining, and engineering universal, predictable, non-overfitted agent skills. Use when designing new agent skills, refactoring existing skills, or auditing skill instructions for verbosity and overfitting.
disable-model-invocation: false
---

# Authoring Agent Skills

`authoring-agent-skills` provides the meta-methodology to engineer high-impact, universal agent skills that steer LLM probabilistic reasoning to a targeted center of gravity without overfitting or template fixation.

---

## First Principle: Nudge Center of Gravity, Avoid Rigid Presets

A skill exists to establish an operational mindset, decision posture, and execution boundary for the LLM. Never trap the LLM with hardcoded code blocks, opinionated templates, fixed color hexes, specific font names, or arbitrary numeric thresholds. Shift the LLM's center of gravity through principles, posture, and dynamic discovery steps.

---

## Core Posture

- **Principle Over Template**: Guide by posture, structural boundaries, and intent discovery — not by copy-paste code blocks.
- **Universal Context**: Draft instructions to accommodate any user prompt situation, domain, or visual preference without hardcoded assumptions.
- **Zero Verbosity**: Eliminate fluff, narrative filler, and duplicate definitions. Every line must serve predictability or guardrails.
- **Flat File Hierarchy**: Keep supplementary reference files flat in the skill folder using uppercase names (`SLUG-NAME.md`). Avoid nested directory sprawl.

---

## Triggers

Reach for this skill when:
- Designing a new agent skill from scratch.
- Refactoring an existing skill that suffers from verbosity, hardcoded examples, or rigid template fixation.
- Auditing skill files for universal applicability and LLM posture alignment.

---

## Execution Workflow

### 1. Identify Intent & Leading Words
Define the skill's primary leading words and operational posture:
- Identify the core posture (e.g. *Discover First*, *Systemize Second*, *Semantic Hygiene*).
- Define unambiguous model triggers and clear "When NOT to invoke" boundaries.

### 2. Formulate Workflow & Discovery Steps
Structure the execution workflow around dynamic discovery rather than fixed defaults:
- **Phase 1 (Discovery)**: Require the agent to align with user intent, context, and brand before generating output.
- **Phase 2 (Architecture)**: Provide decision criteria for selecting structural patterns based on project scale and delivery target.
- **Phase 3 (Execution)**: Provide principles for semantic markup, data hygiene, and structural clarity.
- **Phase 4 (Verification)**: Define checkable completion criteria and verification passes.

### 3. Audit for Overfitting & Hardcoded Presets
Review the skill against [SKILL-ENGINEERING.md](SKILL-ENGINEERING.md):
- Strip out hardcoded code blocks, specific color hex codes, fixed font names, or preset theme names.
- Remove project-specific edge cases that belong to an individual user's request rather than the universal skill.
- Eliminate arbitrary numeric thresholds (e.g. "10+ items") that artificially constrain decision making.

### 4. Structure & Flatten Files
Consult [SKILL-ENGINEERING.md](SKILL-ENGINEERING.md):
- Keep `SKILL.md` concise, containing only frontmatter, principles, posture, workflow, failure modes, and framework pointers.
- Place supplementary reference files directly in the skill root directory (`UPPERCASE-SLUG.md`).

---

## Failure Modes

- **Template Overfitting**: Including specific code blocks or preset styles that cause the LLM to blindly copy examples instead of reasoning dynamically.
- **Project-Specific Over-indexing**: Turning an individual user's one-off preference into a mandatory global skill rule.
- **Arbitrary Thresholds**: Defining hardcoded numbers (e.g. "10+ slides") that restrict flexibility.
- **Verbosity Sprawl**: Filling skill files with narrative prose that inflates token load without improving execution predictability.

---

## Disclosed Reference

- [SKILL-ENGINEERING.md](SKILL-ENGINEERING.md) — Guidelines for preventing overfitting, establishing operational posture, and steering LLM attention.
