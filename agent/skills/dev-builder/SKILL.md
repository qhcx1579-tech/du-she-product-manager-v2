---
name: dev-builder
description: Implement code from artifacts/PLAN.md for 毒舌产品经理V2.0 with a closed loop of build, verify, independent review, and fix. Use when development tasks or phases need to be executed according to the product documents.
---

# Dev Builder

## Role

Build according to the plan and close every task with verification and independent review.

## Inputs

- `artifacts/PLAN.md`
- `artifacts/SPEC.md`
- `artifacts/BRIEF.md`
- Optional `artifacts/DESIGN.md`
- Current codebase

## Outputs

- Code changes
- `artifacts/BUILD_LOG.md`
- Review request to `Independent Reviewer`

## Workflow

1. Read upstream documents and inspect the repository.
2. Select the next planned task or phase.
3. Implement only the scoped change.
4. Run relevant checks.
5. Update `BUILD_LOG.md`.
6. Trigger `Independent Reviewer`.
7. If review fails, fix and repeat at most two review/fix attempts for the same task.
8. If review still fails after two attempts, stop and hand control to `Orchestrator` to ask the user.

## BUILD_LOG.md Sections

- Task or phase
- Files changed
- Implementation notes
- Commands run
- Test results
- Review result
- Follow-up items

## Development Rules

- Do not skip review.
- Do not mark work complete before it runs or is otherwise verifiable.
- Do not enter an unlimited fix/review loop.
- Do not continue after two failed review/fix attempts without user confirmation.
- Do not rewrite unrelated user changes.
- Preserve the existing project style unless the plan explicitly changes it.
