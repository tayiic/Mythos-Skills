# Famous Skill Gallery Plan

Optimized famous skills live under:

```text
gallery/famous/<source-slug>/<skill-slug>/
|-- ORIGINAL.md
|-- SKILL.md
|-- DIFF.md
|-- BENCHMARK.md
|-- references/
`-- operations.json
```

Use `gallery/famous/` for recognizable public skills. Use `gallery/community/` later for smaller community submissions.

## First Batch: 20 Candidates

Prioritize 10 first, then expand to 20.

| Priority | Source | Skill | Why it matters | Target optimization |
|---:|---|---|---|---|
| 1 | Anthropic | `skill-creator` | Canonical skill authoring reference | Smaller activation, Mythos P1-P8 gate |
| 2 | Anthropic | `claude-api` | High-value developer workflow | Split provider rules into references |
| 3 | Anthropic | `xlsx` | Complex production document skill | Move formatting/formula detail into refs |
| 4 | Anthropic | `pptx` | Visually rich production skill | Trigger layer + design/QA refs |
| 5 | Anthropic | `pdf` | Common file automation skill | Route tasks to focused references |
| 6 | Anthropic | `docx` | Common enterprise document skill | Compact task router |
| 7 | Superpowers | `systematic-debugging` | Famous root-cause workflow | Keep iron law, move phases/gotchas to refs |
| 8 | Superpowers | `test-driven-development` | Famous TDD enforcement workflow | Keep red/green/refactor gate, split examples |
| 9 | Superpowers | `writing-plans` | Planning workflow is broadly reusable | Trigger-first entry + plan template refs |
| 10 | Superpowers | `requesting-code-review` | Review workflow is broadly reusable | Compact checklist + review rubric refs |
| 11 | Superpowers | `brainstorming` | Front-loaded design workflow | Short Socratic trigger + interview refs |
| 12 | Superpowers | `verification-before-completion` | Common agent failure prevention | Compact completion gate |
| 13 | Playwright Skill | browser automation | Concrete tool skill with scripts | Compare script-first structure |
| 14 | Awesome Agent Skills | frontend design | High-demand coding agent skill | Trigger accuracy + visual QA refs |
| 15 | Awesome Agent Skills | deploy/Vercel | Common production workflow | Command safety + env gotchas |
| 16 | Awesome Agent Skills | Supabase | Popular app stack | Self-contained setup refs |
| 17 | Awesome Agent Skills | Stripe | High-risk API workflow | Low-freedom payment constraints |
| 18 | Awesome Agent Skills | Cloudflare | Deployment/infra skill | Safety and rollback structure |
| 19 | Awesome Agent Skills | Sentry | Debugging/observability skill | Incident workflow refs |
| 20 | Awesome Agent Skills | Figma/design handoff | Cross-modal design workflow | Asset and QA routing |

## Release Standard

Do not merge an optimized famous skill until:

- License and attribution are clear.
- `ORIGINAL.md` preserves the source baseline.
- `SKILL.md` is <=55 lines unless an exception is documented.
- `DIFF.md` maps changes to P1-P8.
- `BENCHMARK.md` lists activation size and estimated token delta.
- Cross-directory references are removed.
- The skill can be copied alone.
