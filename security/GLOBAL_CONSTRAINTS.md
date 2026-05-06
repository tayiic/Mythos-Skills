# Global Constraints

These are the public project-level constraints Mythos-Skills recommends for production-grade skills.

## Protected Inputs

Sensitive values should stay outside the skill package:

- API keys
- passwords
- tokens
- machine-local trust settings
- machine-local provider configuration

Use environment variables or local machine configuration instead of committing secrets into a reusable skill.

## Human Review Boundaries

These file classes should be treated as high-review surfaces:

- `.env` and secret-bearing files
- lockfiles
- CI/CD configuration
- deployment configuration
- database migrations
- production configuration

If a skill touches these files, it should say so explicitly.

## Dependency Discipline

- Prefer existing package managers and lockfiles.
- Do not silently upgrade dependencies.
- Explain new dependency additions and why they are needed.

## Config Discipline

- AI-generated configuration should be reviewable before activation.
- Shared project config should be separated from machine-local config.
- A public skill should not assume access to a user's private local setup.

## Portability Rule

A good public skill should be copyable without dragging private state with it.

That means:

- no hardcoded secrets
- no absolute machine-local paths
- no hidden dependency on untracked local files
- no undocumented reliance on a specific interactive shell profile
