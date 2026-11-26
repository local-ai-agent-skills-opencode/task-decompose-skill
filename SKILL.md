---
name: task-decompose
description: Break non-trivial request into ordered atomic checklist with verifiable "done when". Use before planning, architecture or code on anything beyond single trivial edit.
license: MIT
compatibility: opencode
metadata:
  version: "1.1.0"
---

# DECOMPOSE

## Trigger
Any request that is not a single trivial edit.

## Protocol
1. Goal in one dense sentence.
2. Inputs / outputs / constraints / unknowns / edges.
3. Atomic subtasks: independent, ordered, verifiable.
4. Emit exact:

## PLAN
- [ ] 1. <subtask> — done when: <condition>
- [ ] 2. ...

5. Execute in order. Mark [x] only after selfcheck pass.
6. Scope drift >20% or new unknowns → STOP, re-decompose.

## Rules
- ≤7 subtasks per level (group into phases if more).
- Never implement before checklist exists.
- Keep & update checklist; do not recreate.
- After body: emit PLAN immediately. Never re-call this skill. Never re-route.
