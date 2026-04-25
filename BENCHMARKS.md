# Benchmarks

This page is the evidence board for Mythos-Skills.

The goal is not to claim magic. The goal is to make every optimization reviewable: before size, after size, activation context, portability, trigger quality, and measured task results.

## Measurement Method

| Metric | Meaning | How to measure |
|---|---|---|
| Activation lines | Lines loaded when the skill triggers | `SKILL.md` line count |
| Activation size | Approximate prompt weight | `SKILL.md` bytes and estimated tokens |
| Estimated tokens | Rough planning number | `bytes / 4`, rounded |
| Trigger quality | Whether description says when to use it | P5 review rubric |
| Portability | Whether the folder works when copied alone | P3 checklist |
| Runtime speed | Task duration in evals | `duration_ms` from benchmark runs |
| Task token cost | Total run cost in evals | `total_tokens` from benchmark runs |

All final claims must be backed by an `ORIGINAL.md`, optimized `SKILL.md`, `DIFF.md`, and benchmark notes.

## Headline Board

These are the first famous skills to benchmark. Baseline public data comes from GitHub pages and public skill indexes. Mythos targets are release gates for the first optimized pass, not final claims until the optimized folders land in `gallery/famous/`.

| Famous skill | Source signal | Baseline activation | Mythos target | Expected impact |
|---|---:|---:|---:|---|
| Anthropic `skill-creator` | `anthropics/skills`, 120k-star repo | 485 lines, 32.4 KB | <=55 lines entry + refs | ~85-90% less activation context |
| Anthropic `claude-api` | `anthropics/skills`, 120k-star repo | 324 lines, 32.2 KB | <=55 lines entry + refs | ~80-88% less activation context |
| Anthropic `xlsx` | `anthropics/skills`, 120k-star repo | 292 lines, 11.2 KB | <=55 lines entry + refs | ~70-82% less activation context |
| Superpowers `systematic-debugging` | Famous workflow skill | Long workflow file | <=55 lines entry + refs | Faster trigger, same root-cause discipline |
| Superpowers `test-driven-development` | Famous workflow skill | Long workflow file | <=55 lines entry + refs | Faster trigger, same TDD enforcement |

## Current Mythos Creator Comparison

The current Mythos `engine/skill-creator/SKILL.md` is a scaffold, not yet feature-parity with the Anthropic skill creator. It proves the shape:

| Creator | Entry file | Activation model | Status |
|---|---:|---|---|
| Anthropic `skill-creator` | 485 lines / 32.4 KB | Large single entry | Public baseline |
| Mythos `skill-creator` | 27 lines | Compact entry + references + `operations.json` | Scaffold |
| Mythos `skill-creator-lite` | Single self-contained file | Copy one `SKILL.md` | Minimal mode |

The full benchmark target is to preserve useful creation behavior while keeping the always-loaded entry below 55 lines.

## Required Case Format

Every optimized famous skill must include this table in its `DIFF.md`:

| Metric | Original | Mythos optimized | Delta |
|---|---:|---:|---:|
| `SKILL.md` lines | TBD | TBD | TBD |
| `SKILL.md` bytes | TBD | TBD | TBD |
| Estimated activation tokens | TBD | TBD | TBD |
| External references | TBD | Local only | TBD |
| Trigger rubric score | TBD | TBD | TBD |
| Portability checklist | TBD | Pass | TBD |
| Eval pass rate | TBD | TBD | TBD |
| Mean duration | TBD | TBD | TBD |
| Mean total tokens | TBD | TBD | TBD |

## Source Notes

- `anthropics/skills` is a 120k-star public repository for Agent Skills and includes document, API, and skill-creation examples.
- GitHub reports Anthropic `skill-creator` at 485 lines / 327 LOC / 32.4 KB.
- GitHub reports Anthropic `claude-api` at 324 lines / 209 LOC / 32.2 KB.
- GitHub reports Anthropic `xlsx` at 292 lines / 224 LOC / 11.2 KB.
- Superpowers' public debugging skill states a systematic approach can take 15-30 minutes versus 2-3 hours for random fixes, with first-time fix rate 95% versus 40%. Mythos should preserve that discipline while reducing activation load.
