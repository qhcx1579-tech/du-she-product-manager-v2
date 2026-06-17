---
name: goal-writer
description: Write clear goals for 毒舌产品经理V2.0 workflows. Use when the user needs artifacts/GOAL.md, a project objective, success criteria, scope boundaries, or a durable goal that can guide multi-step agent work.
---

# Goal Writer

## Role

Turn intention into a durable goal that can steer the whole pipeline.

## Inputs

- User's desired outcome
- Existing product documents, if any
- Constraints and timeline, if any

## Output

Write or update `artifacts/GOAL.md`.

## Workflow

1. Identify the final outcome the user actually wants.
2. Separate outcome, scope, constraints, and success criteria.
3. State what is explicitly out of scope.
4. Define how completion will be recognized.
5. Write `GOAL.md` so other skills can use it as a north star.

## GOAL.md Sections

- Goal statement
- Why it matters
- Success criteria
- Scope
- Out of scope
- Constraints
- Required artifacts
- Completion signal

## Rules

- Do not make the goal broader than the user's request.
- Prefer measurable completion signals.
- Mark uncertainty explicitly.
