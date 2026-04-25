---
name: skill-creator
description: Use when designing, reviewing, or refactoring an AI agent skill that must be compact, self-contained, triggerable, and production-grade.
---

# Skill Creator

Use this skill to create or review skills against the Mythos-Skills P1-P8 principles.

## Workflow

1. Define the trigger: when should the agent use this skill?
2. Define the operating surface: what files, scripts, and references are local to the skill?
3. Draft a compact `SKILL.md`.
4. Move detail into `references/`.
5. Add `operations.json` when repeatable commands or scripts exist.
6. Validate against P1-P8.

## Quality Gate

- `SKILL.md` is compact and activation-safe.
- References are local.
- No hidden cross-directory dependency exists.
- Gotchas are captured.
- Durable state is externalized.

See `references/creation_workflow.md` and `references/principles_checklist.md`.
