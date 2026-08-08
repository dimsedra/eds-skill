# RECORD Format

A session record is a brief markdown file in `.journal/comprehend/records/`, titled `0001-<slug>.md`. It captures a single session's shape so the walkthrough can be reconstructed later. Agent's voice. Not a transcript.

## Template

```md
---
date: {YYYY-MM-DD}
slice: {the slice the session covered, or '-' if mission-level}
mode: {gating | paying-down}
frontier: {one sentence: where the ownership frontier moved this session}
---

## Covered

{1-3 bullets: what the session walked through. The shape, not the transcript. The agent's voice.}

## User questions

{1-3 bullets: the questions the user asked that drove the session. These are the moments that shaped the conversation. The user's words, paraphrased. If the user asked nothing, note "no questions" — the agent was talking too much.}

## Ownership signals observed

{1-3 bullets: recital, question depth, pushback, connection, defence. The agent observed these in the conversation. If fewer than 2, the user hasn't owned the slice yet — the next session's scope is closer than they think.}

## Doc written?

{Yes / No. If yes, the file path of the walkthrough doc. If no, why not — ownership not yet demonstrated, user declined, or session cut short.}

## Next session

{1-2 sentences: what the next session should pick up. Either a new slice to walk through, or a re-activation of an earlier slice.}
```

## When to write a record

- After every session that walked through a slice — even if no walkthrough doc was written.
- After every mission-level event: mission changed, success criterion reached, mission archived.

If a session produced nothing worth recording (rare), no record is needed. The journal is not a transcript.

## What the agent should NOT write

- **A summary of the user's explanations.** The user owns those. The record captures the *shape* of the conversation, not its content.
- **A score or grade.** The skill is explaining, not testing. The frontier note is a position, not a rating.
- **Verbatim dialogue.** Paraphrase. The record is for reconstructing the walkthrough, not replaying it.
