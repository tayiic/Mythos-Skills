# Contributing

Mythos-Skills is a methodology-first repository. Contributions should make skill engineering more reliable, portable, and reviewable.

## What To Contribute

- New P1-P8 examples.
- Optimized community skills with attribution and before/after analysis.
- Validation scripts for skill structure, references, and line counts.
- Clear documentation that helps authors build production-grade skills.

## Skill Quality Bar

Every contributed skill should follow the 8 principles:

| Principle | Requirement |
|---|---|
| P1 Concise is Key | Keep `SKILL.md` compact, ideally 55 lines or fewer |
| P2 Progressive Disclosure | Move details into local `references/` files |
| P3 Self-Contained | Avoid cross-skill and cross-directory dependencies |
| P4 Match Freedom | Use stricter instructions for fragile operations |
| P5 Trigger Over Description | Explain when to use the skill |
| P6 Gotchas Are Gold | Capture known failure modes |
| P7 Code Over Instructions | Prefer scripts or structured operations for repeatable work |
| P8 Externalize Memory | Store durable state in files |

## Optimized Third-Party Skills

For any optimized third-party skill, include:

- `ORIGINAL.md`
- `SKILL.md`
- `DIFF.md`
- `references/`
- `operations.json` when useful
- Source license copy
- Attribution in `THIRD_PARTY_LICENSES.md`

## Pull Request Checklist

- The skill is self-contained.
- Links are relative and local.
- License requirements are preserved.
- `DIFF.md` explains the optimization.
- No private credentials, internal paths, or unpublished proprietary content are included.
