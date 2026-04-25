---
name: skill-creator-lite
description: Use when creating or reviewing an AI agent skill and the user wants the simplest possible Mythos-Skills workflow: one copyable SKILL.md with no bundled references required.
---

# Skill Creator Lite

Create skills as reusable engineering units, not long prompt files.

## Output Shape

Prefer a folder:

```text
skill-name/
|-- SKILL.md
|-- references/
`-- operations.json
```

Minimal mode: a single `SKILL.md` is allowed if the skill is small and self-contained.

## Workflow

1. Write the trigger first: when should the agent use this skill?
2. Keep the entry compact: only activation-critical guidance belongs in `SKILL.md`.
3. Move long examples, commands, pitfalls, and background to `references/` when available.
4. Add `operations.json` for repeatable scripts or command flows when available.
5. Review the skill against P1-P8 before calling it done.

## P1-P8 Gate

| # | Gate | Pass condition |
|---|---|---|
| P1 | Concise | `SKILL.md` is small enough to load often |
| P2 | Progressive | Detail loads only when needed |
| P3 | Self-contained | The skill folder can be copied alone |
| P4 | Freedom matched | Fragile operations are tightly constrained |
| P5 | Trigger-first | Description says when to use it |
| P6 | Gotchas | Known failure modes are captured |
| P7 | Code over prose | Repeatable work uses scripts/templates where possible |
| P8 | Memory externalized | Durable state lives in files |

## Done Means

- The trigger is specific.
- The instructions are portable.
- Hidden dependencies are removed.
- Gotchas are visible.
- A future agent can use it without reading the whole project.
