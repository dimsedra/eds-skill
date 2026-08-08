# MISSION Format

`MISSION.md` lives at the root of the `.journal/comprehend/` workspace. It captures *what* the user is trying to own and *why this slice, now*.

## Template

```md
# Mission: {one-line name of the slice}

## The slice

{1-3 sentences: which code, where it lives, what it does.}

## Why this slice, now

{1-3 sentences: the driver. A 3am page, an upcoming refactor, a code review where you couldn't defend a choice. The driver is what makes the comprehension stick — without it, the walkthroughs stay shallow.}

## Success criterion

{1-2 sentences: how will you know you own it? "I can re-explain this cold in two weeks." "I can extend it without the agent in the room." "I can debug a real issue that touches it." Pick one. Don't pick all three.}
```

## When to update

- The slice or scope changes — the user realises they wanted a different area.
- The driver changes — the original 3am page is no longer the right reason.
- The user reaches the success criterion — note it. The mission is done; archive it or rename it.

When the mission evolves, add a record capturing the change. The journal needs to be able to reconstruct *why* the user was chasing this slice, not just *that* they were.

## When NOT to update

Don't update the mission to reflect a single session's drift. If the user is bouncing between modules in a way that doesn't add up, that's a **mission drift** failure mode — see the `SKILL.md`. Update the mission, but also add a record.
