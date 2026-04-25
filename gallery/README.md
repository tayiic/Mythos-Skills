# Gallery

The gallery shows how skills improve when rewritten through P1-P8.

## Where Optimized Famous Skills Go

Use this path for the first batch of famous skills:

```text
gallery/famous/<source-slug>/<skill-slug>/
|-- ORIGINAL.md
|-- SKILL.md
|-- DIFF.md
|-- BENCHMARK.md
|-- references/
`-- operations.json
```

Examples:

```text
gallery/famous/anthropic/skill-creator/
gallery/famous/anthropic/claude-api/
gallery/famous/superpowers/systematic-debugging/
```

Each optimized skill should be reviewable:

```text
example-optimized/
|-- ORIGINAL.md
|-- SKILL.md
|-- DIFF.md
|-- references/
`-- operations.json
```

## Optimization Standard

- Preserve license and attribution.
- Keep the optimized `SKILL.md` compact.
- Remove hidden cross-directory dependencies.
- Explain each major change in `DIFF.md`.
- Tie each change to one or more P1-P8 principles.
- Estimate token and reliability impact when possible.

## Current Status

The first famous gallery batch is available at [famous/](famous/).
