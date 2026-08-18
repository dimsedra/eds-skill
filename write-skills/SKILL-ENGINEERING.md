# Skill Engineering Guidelines

The deeper reference behind SKILL.md: what overfitting does to your reasoning, and how to keep a skill universal.

---

## 1. Overfitting: A Skill That Stops Generalizing

Overfitting binds you to the artifacts of one situation (such as a snippet, a preset, or a number), and you follow those instead of the direction behind them. Keep every instruction at the level of the class of problem.

### Fixation on Specifics
Showing exact snippets, fixed classes, or complete templates in a skill invites copying instead of reasoning about the actual requirements. Describe the direction (architectural intent, design principles, structural patterns) and let the specifics follow.

### Single-Project Bias
Turning one user's one-off preference into a mandatory rule forces irrelevant edge cases onto everyone else. One-off specifics belong in the discovery phase of the situation that produced them, not in the rule.

### Preset Uniformity
Preset themes and hardcoded colors make every output identical regardless of context. Build tokens dynamically from what the user tells you during discovery.

### Vanity Numbers vs. Functional Invariants
Differentiate cosmetic metrics from operational invariants:
- **Vanity Numbers (Avoid)**: Hardcoding cosmetic quotas ("write 10+ items", "under 5 lines") claims precision the situation doesn't have and encourages optimizing the count over quality. Use qualitative criteria (scale, modularity, clarity) instead.
- **Functional Invariants (Enforce)**: Quantitative bounds are mandatory when protecting against system failure, runaway agent loops, or safety violations (e.g., loop termination counters, token caps, 0 failing tests, p99 latency SLOs, chunk size thresholds).

### Mindless Compliance vs. Deterministic State Machines
- **Mindless Compliance (Avoid)**: Turning open-ended judgment into rigid do-this/don't-do-that checklists that prevent root-cause reasoning.
- **Deterministic State Machines (Enforce)**: Requiring strict sequential gates where causal ordering or safety invariants are absolute (e.g., Expand -> Migrate -> Contract migrations, Plan -> Approve -> Execute for destructive commands, Red -> Green -> Refactor in TDD).

---

## 2. Steering Your Reasoning

### Leading Words
Anchor the skill's posture with compact concepts you already hold (*Discover First*, *Semantic Hygiene*). A single repeated leading word carries a whole region of behaviour for a few tokens.

### Positive Guardrails
Say where reasoning should land, with the why in one line. When a prohibition is unavoidable, pair it with the direction it protects, because a bare prohibition names what to avoid and makes it more available.

### Checkable Completion
Close each phase with a condition you can objectively verify (binary state transitions, zero-failure test runs, invariant proofs) so work ends when it is genuinely complete, not when it feels complete.

---

## 3. File Structure

- **`SKILL.md`**: frontmatter, first principle, posture, workflow, failure modes, and pointers.
- **Flat `UPPERCASE-SLUG.md` files**: reference detail lives directly in the skill folder, reached on demand. No nested subdirectories.
- **Lean**: every line steers reasoning or guards a boundary; nothing else survives.
