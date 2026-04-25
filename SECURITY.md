# Security Policy

## Supported Versions

The repository is pre-1.0. Security fixes apply to the current `main` branch.

## Reporting A Vulnerability

Please report sensitive security issues privately to the maintainer instead of opening a public issue.

Include:

- A short description of the issue.
- Affected files or skills.
- Reproduction steps.
- Potential impact.

## Scope

Security-sensitive areas include:

- Scripts invoked by skills.
- Command rules and allowlists.
- Generated operations in `operations.json`.
- Instructions that could cause destructive filesystem, network, or credential behavior.

## Design Rule

Skills should make dangerous operations explicit, reviewable, and narrow. If an operation can delete, overwrite, exfiltrate, or publish data, the skill must state the constraints clearly.
