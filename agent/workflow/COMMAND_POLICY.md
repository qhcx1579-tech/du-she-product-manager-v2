# Command Policy

## Purpose

This file defines which commands an AI agent may run automatically, which commands require explicit user confirmation, and which commands are forbidden or restricted.

The purpose is to prevent silent destructive operations, unsafe Git operations, privacy leaks, and black-box remote uploads.

## When To Apply

Apply this policy before any terminal command, Git operation, dependency installation, environment change, file deletion, release action, deployment action, or remote upload.

The agent must classify the intended command before running it:

1. Identify the command risk level.
2. Decide whether it may run automatically.
3. If confirmation is required, explain the exact command, target, purpose, and possible impact.
4. If the command is forbidden by default, stop unless the user explicitly authorizes the exact command in the current session.

## Command Risk Levels

### Level 0: Read-only commands

Allowed automatically.

Examples:

- `git status`
- `git diff`
- `git log --oneline`
- `git remote -v`
- `pwd`
- `ls`
- `dir`
- `cat`
- `type`
- `find`
- `grep`
- `rg`
- reading project files
- reading artifact files

Rules:

- These commands must not modify files, Git history, dependencies, environment variables, or remote resources.
- If a supposedly read-only command unexpectedly changes files, the agent must stop and report it.

### Level 1: Local project modification commands

Allowed only when scoped to the current task.

Examples:

- editing source files
- creating new project files
- updating artifact files
- formatting code
- generating local build artifacts
- running local tests
- running local lint commands

Rules:

- The agent must explain what it intends to change before making edits.
- The agent must summarize changed files after modification.
- The agent must not modify unrelated files.
- The agent must not modify `.env`, credentials, private notes, local secrets, or user-specific configuration unless explicitly instructed.

### Level 2: Dependency and environment modification commands

Require explicit user confirmation.

Examples:

- `npm install`
- `pnpm install`
- `yarn install`
- `yarn add`
- `pip install`
- modifying lock files
- modifying package manager configuration
- modifying Docker files
- modifying CI/CD configuration
- modifying system-level configuration

Rules:

- The agent must explain the dependency or environment impact before running the command.
- The agent must state which files may change.
- The agent must stop if the user does not explicitly approve.

### Level 3: Git history commands

Require explicit user confirmation.

Examples:

- `git add`
- `git commit`
- `git branch`
- `git checkout`
- `git merge`
- `git rebase`
- `git stash`
- `git tag`

Rules:

- The agent must show `git status` before any Git history operation.
- The agent must summarize changed files before staging or committing.
- The agent must not stage everything blindly with `git add .` unless the user explicitly approves.
- Prefer staging specific files.
- The agent must not rewrite history unless explicitly approved.

### Level 4: Remote, destructive, or irreversible commands

Forbidden by default.

Examples:

- `git push`
- `git push --force`
- `git reset --hard`
- `git clean -fd`
- `rm -rf`
- `del /s /q`
- `rmdir /s /q`
- `docker system prune`
- deleting databases
- deleting project directories
- uploading files to remote services
- publishing packages
- deploying to production
- changing production configuration

Rules:

- These commands must never be executed silently.
- The agent may only proceed if the user explicitly authorizes the exact command, exact target, and exact purpose in the current session.
- If the command may destroy data or affect remote resources, the agent must provide a rollback or backup plan first.
- `git push` must always require explicit confirmation, even if a commit already exists.

## GitHub Push Rule

The agent must never perform `git push` silently.

Before any remote push, the agent must show:

- current branch
- current remote URL
- files changed
- commit message
- privacy audit result
- whether secrets or private files were detected
- whether the push target matches the user's intended repository

The agent must then ask for explicit confirmation.

## Secret and Privacy Rule

The agent must not upload, commit, or expose:

- `.env`
- API keys
- access tokens
- SSH keys
- private notes
- chat logs
- local caches
- system prompts
- developer prompts
- internal agent prompts
- personal account data
- private email addresses
- machine-specific paths
- credentials
- database dumps
- browser profiles
- cookies
- session files

If any of these are detected, the agent must stop and report the risk.

## Failure Rule

If any command fails, the agent must stop and summarize:

- command executed
- error observed
- likely cause
- whether files were modified
- whether Git state changed
- safest next action

The agent must not continue blindly after a failed command.

## Review Rule

After modifying files, the agent must provide:

- list of changed files
- purpose of each change
- whether tests were run
- test result
- remaining risks
- whether user confirmation is needed before Git or remote operations
