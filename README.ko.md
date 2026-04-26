# Mythos-Skills

> AI Agent 를 위한 Skill Engineering.

Languages: [English](README.md) | [简体中文](README.zh-CN.md) | [日本語](README.ja.md) | [한국어](README.ko.md) | [Español](README.es.md)

Mythos-Skills 는 skill 을 긴 프롬프트 파일이 아니라 재사용 가능한 엔지니어링 단위로 다룹니다.

## Why It Matters

많은 공개 skill 은 유용하지만 재사용하기 어렵습니다. `SKILL.md` 가 너무 길거나, trigger 가 모호하거나, 숨은 의존성이 있거나, 실패 패턴이 빠져 있습니다.

Mythos-Skills provides:

- Production-grade skill 을 위한 8 principles.
- 한 파일로 복사 가능한 `skill-creator-lite`.
- 표준 `skill-creator` 폴더 워크플로.
- 유명 skill 의 before/after benchmark gallery.

## Proof First

첫 benchmark 는 Anthropic `skill-creator`, `claude-api`, `xlsx`, Superpowers `systematic-debugging`, `test-driven-development` 같은 유명 skill 을 대상으로 합니다.

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

## ⚡ Early Supporters

**First 100 stargazers get:**
- Free 1-on-1 AI coding workflow consultation
- Priority access to new skills before public release
- Direct Q&A with the maintainer (X DM or GitHub Discussion)

⭐ Star now → DM me on [X](https://x.com/tayiic) to claim

## 🎯 Star Milestones

| Stars | Unlock |
|-------|--------|
| 100 | `skill-creator-lite` single-file edition |
| 500 | Video walkthrough: P1-P8 in practice |
| 1,000 | `plan-forge` skill (Tier 1, early access) |
| 2,500 | Chinese deep-dive series (8 articles) |
| 5,000 | Public eval harness & compatibility matrix |

Your star directly shapes what gets built next.

## 🙏 Supporters

<!-- Stargazers Hall of Fame will be auto-generated -->

### Sponsors

Support this project via [GitHub Sponsors](https://github.com/sponsors/tayiic)

| Sponsor | Tier |
|---------|------|
| *Your name here* | ☕ Coffee |

**Skill 은 쌓는 것이 아니라 단련하는 것입니다. Star 를 부탁드립니다 ⚡**
