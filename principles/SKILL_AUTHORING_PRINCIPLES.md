# Skill Authoring Principles

Mythos-Skills uses 8 principles to turn skills from long prompts into reusable engineering units.

## P1: Concise Is Key

The context window is a shared resource. A skill should activate with the smallest useful surface and load detail only when needed.

## P2: Progressive Disclosure

Do not preload everything. Keep `SKILL.md` as the entry point and move deeper guidance into local `references/` files.

## P3: Self-Contained

Every skill should be portable. Copying its directory should preserve behavior, references, scripts, and operational metadata.

## P4: Match Freedom

Fragile operations need narrow instructions and explicit constraints. Creative work can allow more freedom.

## P5: Trigger Over Description

A skill description should tell the agent when to use the skill. "What it does" is secondary.

## P6: Gotchas Are Gold

Known failure modes are high-value context. A compact anti-pattern can prevent repeated mistakes better than a long idealized guide.

## P7: Code Over Instructions

For repeatable work, provide scripts, structured operations, or templates. Let the agent orchestrate known machinery instead of rebuilding it from prose.

## P8: Externalize Memory

Durable state belongs in files, not in the conversation. Long-running work should survive context resets and handoffs.

## Standard Three-Layer Shape

```text
skill-name/
|-- SKILL.md          # compact entry point
|-- references/       # details loaded only when needed
`-- operations.json   # machine-readable operation index
```
