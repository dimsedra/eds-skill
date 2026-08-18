# Context: `/comprehend` Skill

Domain model and glossary for code comprehension within the `.journal/` workspace.

## Language

**Ownership Frontier**:
The boundary of code that the user can already explain without the agent.
_Avoid_: knowledge gap, blind spot.

**Ownership Signal**:
An observable moment in the conversation where the user demonstrates real comprehension (e.g., recital, question depth, pushback, connection, defence).
_Avoid_: ownership claim.

**Mission**:
The slice of codebase the user is trying to own, and the specific reason why they are doing it now. Saved in `.journal/comprehend/MISSION.md`.
_Avoid_: goal, objective.

**Walkthrough Doc**:
A standalone HTML file in `.journal/comprehend/modules/` compiled upfront by a dedicated subagent, capturing the walkthrough in the user's voice.
_Avoid_: module.

**Session Record**:
A markdown file in `.journal/comprehend/records/` capturing the shape of the conversation and observed ownership signals.
_Avoid_: log, transcript.

## Relationships

- A **Mission** defines the scope of the **Ownership Frontier** we are trying to expand.
- A walkthrough session moves the **Ownership Frontier** outward by walking through code slices.
- Each walkthrough session produces a **Session Record**.
- The parent agent dispatches a clean-head subagent to compile the **Walkthrough Doc** directly to disk upfront upon invocation.
- Multiple sessions are conducted until **Ownership Signals** are observed.
