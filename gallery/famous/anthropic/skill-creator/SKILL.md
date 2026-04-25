---
name: skill-creator-optimized
description: Use when creating or reviewing an AI agent skill that must be compact, self-contained, triggerable, and benchmarkable.
---

# Optimized Skill Creator

Create skills as engineering units: compact entry, local references, optional operations, measurable quality gates.

## Workflow

1. Define the trigger in one sentence: when should the agent use this skill?
2. Draft a <=55-line `SKILL.md` with only activation-critical rules.
3. Move examples, edge cases, and long procedures into `references/`.
4. Add `operations.json` for repeatable commands, scripts, or validation flows.
5. Fill `BENCHMARK.md` with line count, size, estimated tokens, and portability checks.
6. Reject the skill if it depends on hidden external files.

## P1-P8 Gate

Pass only if it is concise, progressive, self-contained, freedom-matched, trigger-first, gotcha-aware, script-friendly, and memory-externalized.

## Outputs

- `SKILL.md`
- `references/`
- `operations.json`
- `DIFF.md`
- `BENCHMARK.md`
