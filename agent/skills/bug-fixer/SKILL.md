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

## Windows Installer Diagnostics

Use this path when the user reports:

- exe cannot open
- installer is blocked by Windows
- Windows says the app cannot be installed
- SmartScreen or Smart App Control blocks the installer
- double-clicking an installer does nothing or Windows Security blocks it

Do not immediately assume the application code is broken. Do not default to telling the user to disable Windows security features.

Check in this order:

1. Windows Smart App Control blocking
2. Microsoft Defender SmartScreen blocking
3. Microsoft Defender false positive
4. Mark-of-the-Web source marker on the downloaded file
5. Missing code signing
6. Missing publisher information
7. Missing version information
8. Inno Setup `.iss` configuration gaps
9. Running from an untrusted path, download folder, network location, or chat-app cache
10. Packers, obfuscation, excessive permissions, or bundled unknown `.exe` / `.dll` files

Temporary disabling of Smart App Control, SmartScreen, Defender, or firewall may only be presented as a development-test diagnostic option when the user confirms the installer source is trusted. It must not be presented as the formal release solution.

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
- If Windows blocks an installer, first separate packaging/security-reputation problems from application runtime bugs.
