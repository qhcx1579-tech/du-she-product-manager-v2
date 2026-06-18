# Windows Install Troubleshooting

## Purpose

Use this document when a Windows `.exe`, `setup.exe`, `installer.exe`, Inno Setup package, or other Windows executable package is blocked, cannot open, or appears to do nothing after double-clicking.

The goal is to separate real application defects from Windows packaging, signing, reputation, and security-policy issues.

## Symptoms

- The exe cannot open.
- Windows blocks the installer.
- Windows says the app is not allowed to install.
- Microsoft Defender SmartScreen shows a warning.
- Windows 11 Smart App Control blocks the app.
- Microsoft Defender or another antivirus quarantines the package.
- Double-clicking the installer does nothing.
- The installer works only after Smart App Control is turned off.

## Likely Causes

- The installer is unsigned.
- The installer has no SmartScreen reputation.
- A new build changed the file hash and reset reputation.
- Windows 11 Smart App Control does not trust the executable.
- Microsoft Defender or another antivirus produced a false positive.
- The file has a Mark-of-the-Web source marker from browser, email, chat, or downloaded archive extraction.
- Publisher or version metadata is missing.
- Inno Setup `.iss` metadata is incomplete.
- The package requests elevated privileges or modifies sensitive locations.
- The package writes to system directories, creates startup entries, installs services, modifies the registry, or bundles unknown `.exe` / `.dll` files.
- The binary is packed, obfuscated, or compressed in a way that looks suspicious.
- The installer is being run from a network location, downloads folder, or chat-app cache.

## Diagnostic Order

1. Confirm the exact Windows message or screenshot.
2. Check whether Smart App Control blocked the file.
3. Check whether Microsoft Defender SmartScreen blocked the file.
4. Check whether Microsoft Defender or antivirus quarantined the file.
5. Check whether the file has Mark-of-the-Web.
6. Check whether the installer is code signed.
7. Check whether publisher and version information are present.
8. Check the Inno Setup `.iss` file, if one exists.
9. Check whether the installer bundles unknown binaries.
10. Check whether the installer performs high-risk actions such as services, startup entries, registry writes, silent downloads, or system-directory writes.

## Development Testing

Temporary security bypasses are diagnostic tools only.

Only mention temporary disabling of Smart App Control, SmartScreen, Defender, or firewall when all of the following are true:

- the user is testing in a development environment
- the user confirms the installer source is trusted
- the goal is to identify whether Windows security reputation is the blocker
- the agent clearly states this is not a release solution

Do not ask non-technical users to disable Windows security features without explaining the risk and confirming the installer source.

## Public Release

For public Windows releases:

- sign the installer with a code-signing certificate
- include publisher information
- include version information
- keep the Inno Setup `.iss` metadata complete and project-specific
- calculate and publish a SHA256 checksum
- retain the build log
- distribute through GitHub Releases, an official website, or another trusted channel
- avoid distributing unsigned installers through chat apps, cloud drives, or unclear download links
- document expected SmartScreen / Smart App Control warnings if the package is unsigned

An unsigned installer may be acceptable for local testing. It should not be called production-ready or ready for public distribution unless the release notes clearly explain the Windows security-warning risk.

## Inno Setup Checklist

If the project uses an Inno Setup `.iss` file, read the local file before modifying it. Do not copy a generic template without checking the real project name, version, output directory, and included files.

Check whether `[Setup]` includes the project-appropriate values for:

- `AppName`
- `AppVersion`
- `AppPublisher`
- `AppPublisherURL`
- `AppSupportURL`
- `AppUpdatesURL`
- `DefaultDirName`
- `DefaultGroupName`
- `OutputBaseFilename`
- `Compression`
- `SolidCompression`
- `WizardStyle`
- `VersionInfoVersion`
- `VersionInfoCompany`
- `VersionInfoDescription`
- `VersionInfoCopyright`

Also check whether the installer includes files that should not ship, such as `.env`, tokens, caches, logs, private configs, prompts, local paths, cookies, sessions, or database dumps.

## What Not To Do

- Do not treat "works after disabling Smart App Control" as proof that the package is release-ready.
- Do not tell public users to disable Windows security features as the fix.
- Do not claim Windows security warnings always mean the app has a virus.
- Do not claim warnings are harmless without checking signing, reputation, package contents, and installer behavior.
- Do not modify `.iss` files without reading the local project structure first.
