# Release

## Release Scope

Initial public repository for 毒舌产品经理V2.0.

Included:

- Workflow documents
- 12 specialist skills
- Review and release gates
- Self-evolution rules
- Public project README

## Privacy Audit

No secrets, tokens, accounts, cookies, private certificates, chat logs, or system/developer prompts are intentionally included.

## Excluded Files

The `.gitignore` excludes:

- `.env` files
- private keys and certificates
- local caches
- logs
- dependency folders
- build outputs
- private artifact drafts and local notes

## GitHub Authorship

Use the user's own Git identity locally, but do not write the user's personal name, email address, account handle, or repository URL into public release documents.

Do not attribute authorship to GPT, Codex, or AI unless the user explicitly requests it.

For public repositories, prefer a privacy-protected Git author email such as a GitHub no-reply email.

## Upload Steps

1. Initialize Git locally.
2. Commit the project.
3. Create a new empty GitHub repository in the user's GitHub account.
4. Add the repository URL as `origin`.
5. Show the target repository URL to the user and ask for confirmation.
6. If the URL is missing, unclear, or not the user-specified repository, ask the user for the exact repository name or URL.
7. Push the local `main` branch to GitHub only after confirmation.

## Windows Package Release Standard

This repository does not currently include a Windows installer or Inno Setup `.iss` file.

For projects built with this agent system, if a Windows `.exe`, `setup.exe`, `installer.exe`, Inno Setup package, or other executable package is produced, the release must include:

- code-signing status
- publisher and version information status
- SmartScreen / Smart App Control risk assessment
- Defender / antivirus risk assessment
- SHA256 checksum
- retained build log
- distribution channel recommendation

Unsigned installers may be used for local testing, but they must not be described as production-ready or suitable for public release without explaining possible Unknown Publisher, SmartScreen, Smart App Control, and antivirus reputation warnings.

Do not ask public users to disable Windows security features as the release solution.
