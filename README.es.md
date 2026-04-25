# Mythos-Skills

> Skill Engineering for AI agents.

Languages: [English](README.md) | [简体中文](README.zh-CN.md) | [日本語](README.ja.md) | [한국어](README.ko.md) | [Español](README.es.md)

Mythos-Skills treats skills as reusable engineering units, not long prompt files.

## Why It Matters

Many public skills are useful but hard to reuse: large `SKILL.md` files, vague triggers, hidden dependencies, missing failure patterns, and too much state kept in conversation.

Mythos-Skills provides:

- 8 principles for production-grade skills.
- A copyable `skill-creator-lite` single-file method.
- A standard `skill-creator` folder workflow.
- A famous-skill gallery with before/after benchmarks.

## Proof First

The first benchmark set targets famous skills such as Anthropic `skill-creator`, `claude-api`, `xlsx`, and Superpowers `systematic-debugging` / `test-driven-development`.

See [BENCHMARKS.md](BENCHMARKS.md).

## Quick Start

Minimal one-file mode:

```bash
mkdir -p .codex/skills/skill-creator-lite
cp engine/skill-creator-lite/SKILL.md .codex/skills/skill-creator-lite/SKILL.md
```

Standard mode:

```bash
cp -r engine/skill-creator .codex/skills/skill-creator
```

## Gallery

Optimized famous skills belong in:

```text
gallery/famous/<source-slug>/<skill-slug>/
```

See [GALLERY_PLAN.md](GALLERY_PLAN.md).
