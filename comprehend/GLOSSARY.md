# GLOSSARY

Vocabulary used in `/comprehend`. One-line definitions; `_Avoid_` lines for terms that drift.

## Ownership frontier

The boundary of code the user can already explain, without the agent.
_Avoid_: "knowledge gap" (too generic), "blind spot" (overloaded with bug-fixing meaning)

## Ownership signal

An observable moment in the conversation where the user demonstrates real comprehension, not just fluency. Signals: recital (user explains without re-reading), question depth (user asks *why*, not *what*), pushback (user disagrees with the agent with reason), connection (user links the slice to other code unprompted), defence (user can answer a sharp review-style question). 2–3 signals for a slice is the threshold for offering the walkthrough doc.
_Avoid_: "ownership claim" (overloaded with the project-management sense of *claim*)

## Walkthrough

The conversation itself — the agent's explanation of a slice, walked through with the user. May be ephemeral (one session) or persisted as an optional walkthrough doc.
_Avoid_: "tutorial" (too generic), "lesson" (too generic)

## Walkthrough doc

An optional HTML file in `.journal/comprehend/modules/`, titled `0001-<slug>.html`. Captured at the moment of ownership, in the **user's** voice. The user dictates the structure; the agent formats. The agent does not write the prose.
_Avoid_: "module" (the old name; loaded with a meaning the skill no longer supports), "doc" (overloaded)

## Session record

A markdown file in `.journal/comprehend/records/`, titled `0001-<slug>.md`. Brief note of what was covered in a session, the questions the user asked, the ownership signals observed. Agent's voice. Not a transcript.
_Avoid_: "log" (too generic), "transcript" (suggests verbatim capture)

## Reference document

An HTML file in `.journal/comprehend/reference/`. Glossaries, callout lists, code-reading maps. Compressed reference the user revisits more often than walkthrough docs.
_Avoid_: "cheat sheet" (too informal), "wiki" (loaded with team-collaboration meaning)

## Component

A reusable asset in `.journal/assets/`. A shared stylesheet, a diagram helper, a code-listing style. Walkthrough docs and reference documents link to components; components are not inline.
_Avoid_: "template" (overloaded with boilerplate meaning)

## Mission

The slice of codebase the user is trying to own, and *why this slice, now*. Lives in `.journal/comprehend/MISSION.md`. The driver is what makes comprehension stick.
_Avoid_: "goal" (too generic), "objective" (project-management register)

## Wisdom layer

The part of ownership that comes from running the code under real conditions — error paths, debugging, modifying for a new requirement. Distinct from knowledge (conversation) and skills (re-walking).
_Avoid_: "experience" (too generic), "practical knowledge" (verbose)

## Desirable difficulty

Techniques — retrieval practice, spacing, interleaving — that build *storage* strength rather than fluency. Harder in the moment, stickier in the long run.
_Avoid_: "active recall" (jargon), "spaced repetition" (means the same thing but isn't ours)

## Explaining vs testing

The agent's posture. Explain: walk through, fill gaps, ask the user to articulate. Test: ask, grade, mark wrong. `/comprehend` is always explaining.
_Avoid_: "non-judgmental" (vague), "supportive" (loaded with therapy register)

## Hype drift

A failure mode where the agent slips into praise language — "Great answer!", "Brilliant response!", "🏆 Ownership Milestone Achieved!" — building up the user's responses with "you're so right that..." or offering the walkthrough doc as a sales pitch with exclamation marks and verbose accommodations. Praise is evaluation; the agent's posture is to inform, not to make the user feel good. The user doesn't need the agent to tell them they've understood.
_Avoid_: "encouragement" (loaded with teacher register), "positivity" (vague)

## Salesy offer

A failure mode where the agent's offer of the walkthrough doc balloons into a pitch: intensifiers ("I think you've *completely* got this!"), verbose accommodations ("let me know any specific points or sections you'd like highlighted"), and a sales close ("we can move forward to our next task!"). The offer is a question, not a pitch. Two sentences max.
_Avoid_: "engagement" (loaded with marketing register), "CTA" (jargon; loaded with marketing meaning)

## Primary source

The code itself. `/comprehend` does not use external resources — no "read this book" step. When the agent grounds a claim, it reads the file and cites file:line.
_Avoid_: "source of truth" (overloaded with database meaning)

## User preferences

How the user likes explanations to land — described by the user in their own words (free-form) and saved in `.journal/comprehend/NOTES.md`. The agent reads `NOTES.md` at the start of every session and adapts.
_Avoid_: "learning style" (psychology jargon; this is a simpler self-report)
