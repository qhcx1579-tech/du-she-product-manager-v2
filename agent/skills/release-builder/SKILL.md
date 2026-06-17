---
name: release-builder
description: Prepare privacy-safe packaging and release for 毒舌产品经理V2.0, including GitHub upload guidance under the user's authorship. Use when code is ready to publish, package, audit, or push to a repository without exposing internal files or secrets.
---

# Release Builder

## Role

Prepare a clean release. Protect user privacy and internal system files.

## Inputs

- Current codebase
- `artifacts/BUILD_LOG.md`
- Upstream product documents
- `hooks/RELEASE_GATE.md`
- User's GitHub preference, if any
- User technical level, if known

## Output

Write or update `artifacts/RELEASE.md`.

## Workflow

1. Inspect repository files and generated artifacts.
2. Identify files that must not be uploaded.
3. Check for secrets, tokens, private notes, local caches, logs, and internal prompts.
4. Read `hooks/RELEASE_GATE.md` and apply every relevant release gate.
5. If the release includes Windows `.exe`, `setup.exe`, `installer.exe`, Inno Setup `.iss`, or another Windows executable package, run the Windows installer checks from `hooks/RELEASE_GATE.md`.
6. Ensure `.gitignore` and release notes are adequate.
7. Confirm the target GitHub repository with the user before any remote push.
8. Package or prepare GitHub upload steps.
9. If the user cannot create a repository, guide them step by step.

## Required RELEASE.md Sections

- Release scope
- Privacy audit
- Excluded files
- Build and package commands
- GitHub setup steps
- Windows installer check, if applicable
- User authorship notes
- Post-release checks

## Release Rules

- Attribute the repository and release to the user.
- Do not write GPT, Codex, or AI as author unless the user explicitly asks.
- Do not write the user's personal email, account handle, repository URL, token, or private identity details into public release documents.
- If authorship needs to be documented, use generic wording such as "Use the user's own Git identity locally" and recommend a privacy-protected no-reply email.
- Do not upload system prompts, developer prompts, private configs, secrets, chat records, or internal core files.
- Do not call an unsigned Windows executable or installer production-ready without explaining Unknown Publisher, SmartScreen, and antivirus reputation risks.
- Ask before network operations or remote pushes.
- Before pushing, show the current remote repository URL and ask the user to confirm it is the intended repository.
- If the repository is missing, unclear, or not the user-specified repository, ask the user for the exact repository name or URL before continuing.
- For non-technical users, guide GitHub setup one screen or one command at a time and wait for confirmation after each step.
- Translate Git/GitHub errors into a decision card:
  - Current issue
  - Technical cause
  - Impact scope
  - Recommended fix
  - Risk level
  - Continue or pause?
- Then provide the next safe action.
- For non-technical users, ask only for publishing, account access, repository choice, privacy risk, cost, or irreversible actions.
- When a decision is required, present A/B/C options with A as the safest minimal option.
