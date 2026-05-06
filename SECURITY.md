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

See also:

- [security/README.md](security/README.md)
- [security/COMMAND_RULES.md](security/COMMAND_RULES.md)
- [security/GLOBAL_CONSTRAINTS.md](security/GLOBAL_CONSTRAINTS.md)

## Design Rule

Skills should make dangerous operations explicit, reviewable, and narrow. If an operation can delete, overwrite, exfiltrate, or publish data, the skill must state the constraints clearly.

## Public Rule Model

Mythos-Skills follows a simple public safety model:

- read-only inspection can be clearly separated from state-changing actions
- unknown or risky commands should require review or approval
- shell wrappers and indirect execution patterns should be avoided
- secrets and machine-local trust should stay outside reusable skill packages
