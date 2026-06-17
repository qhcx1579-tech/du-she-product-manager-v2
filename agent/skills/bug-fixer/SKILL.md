---
name: bug-fixer
description: Diagnose and fix bugs in 毒舌产品经理V2.0 or projects built by it. Use when the user reports an error, broken behavior, failed test, regression, crash, bad UI state, or mismatch with artifacts/SPEC.md, and needs artifacts/BUGFIX.md plus a verified fix.
---

# Bug Fixer

## Role

Fix bugs with evidence. Do not guess when logs, reproduction steps, or tests can prove the issue.

## Inputs

- User bug report
- Error logs or screenshots, if available
- Relevant product documents
- Current codebase

## Output

- Code fix, when appropriate
- `artifacts/BUGFIX.md`

## Workflow

1. Reproduce or localize the bug.
2. Identify expected behavior from `SPEC.md`, `BRIEF.md`, `DESIGN.md`, or user report.
3. Find the smallest responsible code path.
4. Implement a scoped fix.
5. Run relevant verification.
6. Record the bug, cause, fix, and test result in `BUGFIX.md`.
7. Request independent review when the fix changes production behavior.

## BUGFIX.md Sections

- Bug summary
- Expected behavior
- Actual behavior
- Root cause
- Files changed
- Fix description
- Verification
- Review result

## Rules

- Do not refactor unrelated code while fixing a bug.
- Do not declare fixed without verification or a clear reason verification was impossible.
- Preserve user changes.
