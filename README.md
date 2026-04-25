# Mythos-Skills

> The next layer of AI agent work: skill engineering.

Languages: [English](README.md) | [简体中文](README.zh-CN.md) | [日本語](README.ja.md) | [한국어](README.ko.md) | [Español](README.es.md)

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Stars](https://img.shields.io/github/stars/tayiic/Mythos-Skills?style=social)](https://github.com/tayiic/Mythos-Skills/stargazers)
[![Forks](https://img.shields.io/github/forks/tayiic/Mythos-Skills?style=social)](https://github.com/tayiic/Mythos-Skills/forks)
[![Principles](https://img.shields.io/badge/Principles-8%20Iron%20Rules-blue.svg)](principles/SKILL_AUTHORING_PRINCIPLES.md)
[![Agent Skills](https://img.shields.io/badge/Agent%20Skills-Production%20Grade-black.svg)](skills)
[![Gallery](https://img.shields.io/badge/Gallery-Before%20to%20After-green.svg)](gallery)

I audited hundreds of AI agent skill repositories and thousands of registered skills. The pattern was impossible to ignore: the ecosystem is exploding, but most skills are still written like long prompts, fragile snippets, or one-off notes.

Mythos-Skills is built around a higher-level claim:

**Skills are not prompt files. They are reusable engineering units.**

This repository distills that idea into 8 iron principles, a principle-driven creation engine, production-grade examples, and a before/after gallery that shows how weak skills become reliable ones.

## Show Me The Proof

The core promise is measurable improvement, not nicer wording. The first gallery entries target famous skills and show the exact delta.

| Famous skill | Public baseline | Mythos target | Impact to prove |
|---|---:|---:|---|
| Anthropic `skill-creator` | 485 lines / 32.4 KB | <=55-line entry | ~85-90% less activation context |
| Anthropic `claude-api` | 324 lines / 32.2 KB | <=55-line entry | ~80-88% less activation context |
| Anthropic `xlsx` | 292 lines / 11.2 KB | <=55-line entry | ~70-82% less activation context |
| Superpowers `systematic-debugging` | Long workflow file | <=55-line entry | Faster trigger, same root-cause discipline |
| Superpowers `test-driven-development` | Long workflow file | <=55-line entry | Faster trigger, same TDD enforcement |

See [BENCHMARKS.md](BENCHMARKS.md) for the measurement board. Each case must include `ORIGINAL.md`, optimized `SKILL.md`, `DIFF.md`, local `references/`, and benchmark notes. The gallery is where Mythos-Skills earns trust.

## Complexity Escape Hatch

You do not need to adopt the whole repository.

Use the smallest layer that helps:

| Mode | What to copy | Best for |
|---|---|---|
| Lite | `engine/skill-creator-lite/SKILL.md` | One-file method, Karpathy-style minimalism |
| Standard | `engine/skill-creator/` | Full P1-P8 workflow with references |
| Gallery | `gallery/famous/<source>/<skill>/` | Drop-in optimized famous skills |

The repository can be deep. The starting point should be tiny.

## Why This Exists

The first wave of agent work was about prompts.

The second wave was about tools.

The next wave is about skills: portable packets of judgment, workflow, scripts, constraints, examples, and memory that an agent can activate at the right moment.

But the current skill ecosystem has recurring failure modes:

| Failure mode | What breaks |
|---|---|
| Bloated `SKILL.md` files | Every activation pollutes the context window |
| Cross-directory dependencies | Copying a skill breaks hidden references |
| Descriptions that say "what" | Agents fail to trigger skills at the right time |
| No anti-patterns | Agents repeat known mistakes forever |
| State kept in conversation | Long tasks lose continuity |
| Instructions without scripts | Agents spend tokens reconstructing boilerplate |

Mythos-Skills turns those failures into a design system.

## The 8 Iron Principles

| # | Principle | Rule |
|---|---|---|
| P1 | Concise is Key | The context window is a shared resource |
| P2 | Progressive Disclosure | Load detail only when needed |
| P3 | Self-Contained | Every skill must be portable as an atom |
| P4 | Match Freedom | Fragile operations need low freedom; creative work needs high freedom |
| P5 | Trigger Over Description | Write when to use the skill, not what it does |
| P6 | Gotchas Are Gold | Repeated failure patterns are more valuable than happy-path advice |
| P7 | Code Over Instructions | Give agents scripts and structured operations, not vague construction work |
| P8 | Externalize Memory | Put state in files, not in the conversation |

These principles are distilled from official skill-authoring guidance, context engineering, production agent practice, and the failures found across real community skills.

## What Makes This Different

Most repositories answer: "Which skills can I copy?"

Mythos-Skills answers: "What makes a skill worth copying?"

You get:

- A compact authoring doctrine for skill engineering.
- A `skill-creator` engine that validates new skills against P1-P8.
- Production-grade example skills with a three-layer structure.
- A gallery of optimized community skills with original, diff, and token-impact notes.
- A command-safety model for skills that can run real operations.

## Repository Map

```text
Mythos-Skills/
|-- principles/        # The P1-P8 authoring doctrine
|-- engine/            # Principle-driven skill creation engine
|-- skills/            # Production-grade original example skills
|-- gallery/           # Before/after optimized community skills
|-- security/          # Command safety and operating constraints
|-- docs/              # Deep dives, migration notes, and setup guides
|-- DISCLAIMER.md      # Non-affiliation and usage disclaimer
|-- CONTRIBUTING.md    # How to contribute optimized skills
|-- SECURITY.md        # Security policy
`-- LICENSE            # MIT
```

## Quick Start

Clone the repository:

```bash
git clone git@github.com:tayiic/Mythos-Skills.git
cd Mythos-Skills
```

Install the creation engine into an agent skill directory:

```bash
mkdir -p .codex/skills
cp -r engine/skill-creator .codex/skills/skill-creator
```

Then ask your agent:

```text
Use skill-creator to design a production-grade skill for my workflow.
```

The engine should guide the skill through P1-P8 instead of leaving the agent to improvise.

Minimal one-file mode:

```bash
mkdir -p .codex/skills/skill-creator-lite
cp engine/skill-creator-lite/SKILL.md .codex/skills/skill-creator-lite/SKILL.md
```

## Gallery: Before To After

The gallery is the proof surface. It is intentionally designed for famous or widely copied skills first, because trust grows faster when the comparison is recognizable.

Each optimized skill should include:

- `ORIGINAL.md`: the source skill or prompt before optimization.
- `SKILL.md`: the P1-P8 version, kept compact.
- `DIFF.md`: what changed, why it changed, and which principle required it.
- `references/`: details loaded on demand.
- `operations.json`: machine-readable operation index when useful.

This makes optimization reviewable instead of vibes-based.

Recommended first cases:

- Anthropic `skill-creator`, `claude-api`, `xlsx`, `pptx`, `pdf`.
- Superpowers `systematic-debugging`, `test-driven-development`, `writing-plans`, `requesting-code-review`, `brainstorming`.
- Playwright/browser automation and other widely copied practical skills.

The goal is not to claim magic. The goal is to show smaller activation context, clearer triggers, fewer hidden dependencies, and better failure-mode coverage.

Optimized famous skills belong in `gallery/famous/<source-slug>/<skill-slug>/`. See [GALLERY_PLAN.md](GALLERY_PLAN.md).

## Works With

Mythos-Skills is designed for any agent platform that supports skill-like behavior:

Claude Code, Codex, Cursor, OpenCode, Gemini CLI, custom agent harnesses, and internal coding agents.

## Naming And Affiliation

Mythos means a foundational narrative, origin story, or body of principles. This project uses the word in that sense: the foundational mythology of skill engineering.

Mythos-Skills is not affiliated with, endorsed by, or connected to Anthropic or any other model provider. See [DISCLAIMER.md](DISCLAIMER.md).

## Roadmap

- Publish the complete P1-P8 principles document.
- Migrate `skill-creator` into `engine/`.
- Add three production-grade original example skills.
- Add the first optimized gallery entries with before/after analysis.
- Add validation scripts for line count, cross-reference checks, and three-layer structure.

## Contributing

The best contribution is not "one more skill." The best contribution is a skill that teaches the ecosystem how to write better skills.

Start with [CONTRIBUTING.md](CONTRIBUTING.md), then submit:

- A compact `SKILL.md`.
- Local references only.
- A `DIFF.md` if optimizing an existing skill.
- License and attribution notes for any third-party source.

## License

Original Mythos-Skills content is released under the [MIT License](LICENSE). Third-party content keeps its original license and attribution. See [THIRD_PARTY_LICENSES.md](THIRD_PARTY_LICENSES.md).

## Quick Links

Use these when you want the shortest path instead of browsing the whole repository.

| Need | Link |
|---|---|
| Download everything | [main.zip](https://github.com/tayiic/Mythos-Skills/archive/refs/heads/main.zip) |
| Download v002 branch | [v002.zip](https://github.com/tayiic/Mythos-Skills/archive/refs/heads/v002.zip) |
| One-file creator | [skill-creator-lite/SKILL.md](engine/skill-creator-lite/SKILL.md) |
| Standard creator folder | [engine/skill-creator](engine/skill-creator/) |
| Famous skill gallery | [gallery/famous](gallery/famous/) |
| Benchmarks | [BENCHMARKS.md](BENCHMARKS.md) |
| Gallery plan | [GALLERY_PLAN.md](GALLERY_PLAN.md) |
| Anthropic skill-creator optimized | [gallery/famous/anthropic/skill-creator](gallery/famous/anthropic/skill-creator/) |
| Anthropic claude-api optimized | [gallery/famous/anthropic/claude-api](gallery/famous/anthropic/claude-api/) |
| Anthropic xlsx optimized | [gallery/famous/anthropic/xlsx](gallery/famous/anthropic/xlsx/) |
| Superpowers systematic-debugging optimized | [gallery/famous/superpowers/systematic-debugging](gallery/famous/superpowers/systematic-debugging/) |
| Superpowers TDD optimized | [gallery/famous/superpowers/test-driven-development](gallery/famous/superpowers/test-driven-development/) |

**Star this repository if you believe skills should be engineered, not merely written.**
