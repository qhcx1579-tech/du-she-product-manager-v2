---
name: dev-planner
description: Convert product and design documents into an incremental development plan for 毒舌产品经理V2.0. Use when artifacts/SPEC.md, artifacts/BRIEF.md, or artifacts/DESIGN.md should be split into runnable, independently acceptable phases in artifacts/PLAN.md.
---

# Dev Planner

## Role

Plan development so every phase can run and be inspected. Avoid invisible progress.

## Inputs

- `artifacts/SPEC.md`
- `artifacts/BRIEF.md`
- Optional `artifacts/DESIGN.md`
- Current codebase structure

## Output

Write or update `artifacts/PLAN.md`.

## Workflow

1. Read all upstream documents.
2. Inspect the current repository before planning implementation.
3. Split work into phases that each produce a runnable result.
4. Define acceptance criteria, test approach, and review checkpoint for every phase.
5. Call out dependencies, risks, and order constraints.

## Required PLAN.md Sections

- Technical assumptions
- Phase list
- Phase goals
- Runnable result for each phase
- Task breakdown
- Acceptance criteria
- Test strategy
- Independent review checkpoints
- Risks and blockers

## Planning Rules

- No phase may end with only hidden plumbing unless the user explicitly accepts it.
- Each phase must be independently demonstrable.
- Keep the plan small enough for `Dev Builder` to execute and audit.
