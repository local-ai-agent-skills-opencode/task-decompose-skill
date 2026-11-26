# task-decompose

**Languages:** English | [Русский](README.ru.md)

Break a non-trivial request into an ordered, atomic checklist with verifiable “done when” conditions. Use this skill before planning, architecture, or code changes on anything beyond a single trivial edit.

- **Name:** `task-decompose`
- **Version:** `1.1.0`
- **License:** MIT
- **Compatibility:** `opencode`

## Overview

`task-decompose` turns an ambiguous or multi-step request into a concrete execution plan. It produces a checklist of small, ordered, independently verifiable subtasks. Each subtask has an explicit completion condition so progress can be checked without guessing.

This skill is intended to be used **before implementation**, not during or after it. If the request cannot be reduced to a single trivial edit, decompose it first.

## When to Use

Use this skill when the request is:

- more than a single trivial edit;
- ambiguous enough that implementation order matters;
- likely to require planning, architecture, or multiple code changes;
- composed of dependent steps, unknowns, or edge cases;
- large enough that scope drift is possible.

## When Not to Use

Do not use this skill for:

- a single trivial edit;
- a request that is already fully decomposed and verified;
- purely informational questions that require no implementation plan.

## Protocol

1. **State the goal in one dense sentence.**
2. **Identify:**
   - inputs;
   - outputs;
   - constraints;
   - unknowns;
   - edge cases.
3. **Create atomic subtasks.** Each subtask must be:
   - independent where possible;
   - ordered correctly;
   - verifiable.
4. **Emit the plan in exactly this format:**

## PLAN
- [ ] 1. <subtask> — done when: <condition>
- [ ] 2. <subtask> — done when: <condition>


5. **Execute in order.** Mark a task as `[x]` only after its self-check passes.
6. **Stop and re-decompose** if scope drift exceeds 20% or new unknowns appear.

## Output Format

The plan must use this exact structure:

## PLAN
- [ ] 1. <subtask> — done when: <condition>
- [ ] 2. <subtask> — done when: <condition>
- [ ] 3. <subtask> — done when: <condition>

Each “done when” condition must be objectively checkable.

## Rules

- Keep each level to **7 or fewer subtasks**. If there are more, group them into phases.
- **Never implement before the checklist exists.**
- Keep and update the existing checklist. Do not recreate it.
- After the body is complete, emit `PLAN` immediately.
- Never re-call this skill.
- Never re-route.

## Example

Request: “Add request validation and tests for the user creation endpoint.”

## PLAN
- [ ] 1. Inspect the current user creation endpoint and its tests — done when: endpoint behavior, validation gaps, and existing test coverage are documented.
- [ ] 2. Define validation rules for required fields and invalid input — done when: each rule has a clear expected error response.
- [ ] 3. Implement validation in the endpoint — done when: invalid requests return the documented errors and valid requests still succeed.
- [ ] 4. Add tests for valid, invalid, and edge-case inputs — done when: all new tests pass and cover each validation rule.
- [ ] 5. Run the relevant test suite and self-check the checklist — done when: tests pass and every checklist item is verified.

## Quality Gates

A valid decomposition must satisfy all of the following:

- the goal is expressed in one sentence;
- constraints, unknowns, and edge cases are visible;
- every subtask has a verifiable “done when” condition;
- subtasks are ordered and atomic;
- no implementation begins before the checklist exists;
- scope drift is detected and handled by stopping and re-decomposing.

## License

MIT
