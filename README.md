# Mythos-Skills

> The next layer of AI agent work: skill engineering.

Languages: [English](README.md) | [简体中文](README.zh-CN.md)

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

The core promise is measurable improvement, not nicer wording. The first gallery entries will optimize well-known skills and show the exact delta:

| Case | Before | After | Proof |
|---|---|---|---|
| TDD workflow | Long activation file, mixed process and detail | Compact trigger layer plus references | Activation lines and token estimate |
| Debugging workflow | Hidden cross-skill assumptions | Self-contained package | Portability checklist |
| Planning workflow | Generic "what it does" description | Trigger-first description | Activation rubric |

Each case should include `ORIGINAL.md`, optimized `SKILL.md`, `DIFF.md`, local `references/`, and an improvement table. The gallery is where Mythos-Skills earns trust.

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

- A TDD workflow skill.
- A systematic debugging skill.
- A planning or implementation workflow skill.

The goal is not to claim magic. The goal is to show smaller activation context, clearer triggers, fewer hidden dependencies, and better failure-mode coverage.

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

**Star this repository if you believe skills should be engineered, not merely written.**
