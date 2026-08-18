# RECORD Format (Session Mission & Record)

A session record is a brief markdown file in `.journal/comprehend/records/0001-<slug>.md`. Each `/comprehend` session has its own focused mission and record combined in one file.

You initialize the **Mission** section at session start, and complete the **Session Summary & Insights** section as the session finishes.

---

## Template Structure

```md
---
date: {YYYY-MM-DD}
slice: {target code slice or module}
mode: {gating | paying-down}
---

# Session Mission

## Target Slice
{1-2 sentences: which code, where it lives, and what it does.}

## Why This Slice, Now (Driver)
{1-2 sentences: the driver. Gating a PR diff, an upcoming refactor, a 3am incident, or paying down debt.}

## Success Criterion
{1-2 sentences: what success looks like for this session.}

---

# Session Summary & Insights

## Covered
{1-3 bullets: what the session walked through, following the dialogue progression.}

## Dilemmas & Insights (User POV)
{1-3 bullets: core dilemma or question explored → the concrete technical realization that clicked.}

## Report Status
{Path to HTML walkthrough report (.journal/comprehend/modules/0001-<slug>.html) if created, or 'None' if declined.}

## Next Steps
{1-2 sentences: what the next session should pick up.}
```

---

## Execution Workflow

1. **Session Start:** Create or open `records/0001-<slug>.md`. Fill in the **Session Mission** (Target Slice, Driver, Success Criterion).
2. **Session Finish:** Update the **Session Summary & Insights** section (Covered, Dilemmas & Insights, Report Status, Next Steps).

---

## Guidelines for Writing Records

- **Do NOT write code blocks in records.** Keep records focused on high-level shape, driver, and substantive insights.
- **Write in the user's voice.** Capture takeaways from the user's first-person perspective (the question explored and the realization that resolved it) so a cold reader six weeks later recalls their own mental journey.
- **Avoid empty observer logs.** State the actual technical reasoning that clicked rather than third-person meta-statements (such as stating that the user examined or understood something).
- **Do NOT score or grade.** Document the cognitive journey objectively without evaluating proficiency.
