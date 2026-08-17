---
name: write-skills
description: Meta-skill guide for writing, refining, and engineering universal, predictable, non-overfitted agent skills. Use when designing new agent skills, refactoring existing skills, or auditing skill instructions for verbosity and overfitting.
disable-model-invocation: false
---

# Write Skills

Write skills that steer your reasoning toward a center of gravity: clear direction, not rigid scripts. A skill is an instruction, not an essay: tell yourself where to aim, and let yourself rationalize the rest.

---

## How to Write

- **Act as the user.** When you write a skill, you take the user's seat: write it the way this file writes to you (second person, direct, "you").
- **Nudge, don't dictate.** Express each rule as a direction with a reason, so you can generalize it. A checklist of do-this/don't-do-that items makes you obey the items and miss the class of problem behind them.
- **Name failure modes, not forbidden artifacts.** Say what failure you're guarding against (fixation, brittleness, single-project bias). Don't list artifacts to strip, because you will hunt only those and miss the class.
- **State directions positively.** Say where reasoning should land. Keep prohibitions only as hard guardrails, always paired with the direction they protect.
- **Prefer qualitative criteria over numbers.** "10+ items" claims a precision the situation doesn't have and makes you optimize the number. "Scale, modularity, distribution" keeps judgment where it belongs.
- **Write the why.** When a direction protects against a failure mode, say so in one line, so you can generalize it to cases the rule never names.
- **Stay lean.** Every line either steers reasoning or guards a boundary. Cut everything else.
- **Demonstrate the direction.** This file is directions, not artifact lists. Your skill should read the same way.

---

## Core Posture

- **Principle Over Template**: guide by posture, structural boundaries, and intent discovery, not copy-paste artifacts.
- **Universal Context**: keep instructions at the level of the class of problem, so any user, domain, or visual preference fits without hardcoded assumptions.
- **Zero Verbosity**: no fluff, narrative filler, or duplicate definitions; every line serves direction or guardrails.
- **Flat File Hierarchy**: keep supplementary reference files flat in the skill folder (`UPPERCASE-SLUG.md`), no nested sprawl.

---

## When to Use

- The user wants a new agent skill designed from scratch.
- An existing skill suffers from verbosity, hardcoded examples, or rigid template fixation.
- The user wants a skill audited for universal applicability and posture alignment.

---

## Workflow

1. **Discover the intent.** Before writing anything, determine what posture the skill should establish: where should your thinking land, what boundaries should it respect, where should your judgment stay free? Pick leading words (compact concepts you already hold) that anchor that posture.
2. **Architect the skill.** Write a lean `SKILL.md`: frontmatter, posture, workflow, failure modes, and pointers. Push detail into flat `UPPERCASE-SLUG.md` reference files only where you need it on demand.
3. **Write with direction.** State each rule as a direction with its reason. Keep discovery dynamic by aligning with the user's context and brand instead of applying defaults.
4. **Read it back as you will meet it.** Does it steer reasoning, or dictate artifacts? Would a literal reading of any line send you wrong? The skill passes when the direction survives contact with cases it never names.

---

## Failure Modes

- **Checklist Fixation**: writing the skill as a compliance list of do-this/don't-do-that items; you obey the items and stop reasoning about the class of problem. Fix: name the failure mode, state the direction, delete the artifact list.
- **Template Overfitting**: including specific code blocks or preset styles that invite blind copying instead of dynamic reasoning.
- **Project Over-indexing**: turning one user's one-off preference into a mandatory global rule, forcing irrelevant edge-case logic onto future users. Put it in discovery, not in the rule.
- **Arbitrary Thresholds**: hardcoded numbers that claim precision the situation doesn't have and make you optimize the number instead of the outcome.
- **Verbosity Sprawl**: narrative prose that inflates token load without steering reasoning anywhere new.
- **No-Payload Lines**: lines you would follow by default anyway; they cost load and say nothing. Cut them.

---

## Disclosed Reference

- [SKILL-ENGINEERING.md](SKILL-ENGINEERING.md): Deeper reference on overfitting, posture, and file structure.
