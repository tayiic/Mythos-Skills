# Benchmarks

This page is the evidence board for Mythos-Skills.

The goal is not to claim magic. The goal is to make every optimization reviewable: before size, after size, activation context, portability, trigger quality, measured task results, and non-regression in speed and understanding.

## Measurement Method

| Metric | Meaning | How to measure |
|---|---|---|
| Activation lines | Lines loaded when the skill triggers | `SKILL.md` line count |
| Activation size | Approximate prompt weight | `SKILL.md` bytes and estimated tokens |
| Estimated tokens | Rough planning number | `bytes / 4`, rounded |
| Trigger quality | Whether description says when to use it | P5 review rubric |
| Portability | Whether the folder works when copied alone | P3 checklist |
| Runtime speed | Task duration in evals | `duration_ms` from benchmark runs |
| First correct action latency | How quickly the agent gets onto the right workflow | time until first correct routed step |
| Task token cost | Total run cost in evals | `total_tokens` from benchmark runs |
| Eval pass rate | Whether the optimized skill still solves the task set | passed evals / total evals |
| Understanding drift | Whether the optimized trigger changes intended behavior | compare routed workflow, chosen tools, and failure pattern handling |
| Behavior parity | Whether core workflow guarantees still hold | checklist against original intent |

All final claims must be backed by an `ORIGINAL.md`, optimized `SKILL.md`, `DIFF.md`, and benchmark notes.

## Non-Regression Rule

Smaller is not enough.

An optimization is only a real win if it improves activation cost without introducing meaningful regression in:

- task completion quality
- time to first correct action
- mean duration
- total task tokens
- trigger correctness
- workflow guarantees such as TDD discipline, root-cause proof, or verification gates

If a skill is smaller but slower, lower quality, or easier to mis-trigger, the package should say so explicitly instead of marketing it as a pure upgrade.

## Headline Board

These are the first famous skills to benchmark. Baseline public data comes from GitHub pages and public skill indexes. Mythos targets are release gates for the first optimized pass, not final claims until the optimized folders land in `gallery/famous/` and pass non-regression checks.

| Famous skill | Source signal | Baseline activation | Mythos target | Expected impact |
|---|---:|---:|---:|---|
| Anthropic `skill-creator` | `anthropics/skills`, 120k-star repo | 485 lines, 32.4 KB | <=55 lines entry + refs | ~85-90% less activation context |
| Anthropic `claude-api` | `anthropics/skills`, 120k-star repo | 324 lines, 32.2 KB | <=55 lines entry + refs | ~80-88% less activation context |
| Anthropic `xlsx` | `anthropics/skills`, 120k-star repo | 292 lines, 11.2 KB | <=55 lines entry + refs | ~70-82% less activation context |
| Superpowers `systematic-debugging` | Famous workflow skill | Long workflow file | <=55 lines entry + refs | Faster trigger, same root-cause discipline |
| Superpowers `test-driven-development` | Famous workflow skill | Long workflow file | <=55 lines entry + refs | Faster trigger, same TDD enforcement |

## First Batch Status

| Skill | Package | Status |
|---|---|---|
| Anthropic `skill-creator` | [gallery/famous/anthropic/skill-creator](gallery/famous/anthropic/skill-creator/) | Optimized package added |
| Anthropic `claude-api` | [gallery/famous/anthropic/claude-api](gallery/famous/anthropic/claude-api/) | Optimized package added |
| Anthropic `xlsx` | [gallery/famous/anthropic/xlsx](gallery/famous/anthropic/xlsx/) | Optimized package added |
| Anthropic `pptx` | [gallery/famous/anthropic/pptx](gallery/famous/anthropic/pptx/) | Optimized package added |
| Anthropic `pdf` | [gallery/famous/anthropic/pdf](gallery/famous/anthropic/pdf/) | Optimized package added |
| Superpowers `systematic-debugging` | [gallery/famous/superpowers/systematic-debugging](gallery/famous/superpowers/systematic-debugging/) | Optimized package added |
| Superpowers `test-driven-development` | [gallery/famous/superpowers/test-driven-development](gallery/famous/superpowers/test-driven-development/) | Optimized package added |
| Superpowers `writing-plans` | [gallery/famous/superpowers/writing-plans](gallery/famous/superpowers/writing-plans/) | Optimized package added |
| Superpowers `requesting-code-review` | [gallery/famous/superpowers/requesting-code-review](gallery/famous/superpowers/requesting-code-review/) | Optimized package added |
| Superpowers `brainstorming` | [gallery/famous/superpowers/brainstorming](gallery/famous/superpowers/brainstorming/) | Optimized package added |
| Superpowers `verification-before-completion` | [gallery/famous/superpowers/verification-before-completion](gallery/famous/superpowers/verification-before-completion/) | Optimized package added |
| Superpowers `using-git-worktrees` | [gallery/famous/superpowers/using-git-worktrees](gallery/famous/superpowers/using-git-worktrees/) | Optimized package added |

## Current Mythos Creator Comparison

The current Mythos `engine/skill-creator/SKILL.md` is a scaffold, not yet feature-parity with the Anthropic skill creator. It proves the shape:

| Creator | Entry file | Activation model | Status |
|---|---:|---|---|
| Anthropic `skill-creator` | 485 lines / 32.4 KB | Large single entry | Public baseline |
| Mythos `skill-creator` | 27 lines | Compact entry + references + `operations.json` | Scaffold |
| Mythos `skill-creator-lite` | Single self-contained file | Copy one `SKILL.md` | Minimal mode |

The full benchmark target is to preserve useful creation behavior while keeping the always-loaded entry below 55 lines.

## What We Still Need To Prove

The current gallery already proves packaging discipline and activation-size reduction. It does not yet prove full runtime non-regression for every skill.

For each famous package, the next benchmark pass should record:

| Question | What counts as evidence |
|---|---|
| Did speed regress? | compare mean duration and first correct action latency |
| Did quality regress? | compare eval pass rate or task-quality rubric |
| Did the agent misunderstand the smaller skill? | compare routed workflow and decision pattern |
| Did total token cost actually drop? | compare run-level total token usage, not just `SKILL.md` size |
| Did core guarantees survive? | checklist for TDD, debugging proof, verification, safety, or document integrity |

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
| First correct action latency | TBD | TBD | TBD |
| Mean duration | TBD | TBD | TBD |
| Mean total tokens | TBD | TBD | TBD |
| Understanding drift | TBD | TBD | TBD |
| Behavior parity | TBD | TBD | TBD |

## Source Notes

- `anthropics/skills` is a 120k-star public repository for Agent Skills and includes document, API, and skill-creation examples.
- GitHub reports Anthropic `skill-creator` at 485 lines / 327 LOC / 32.4 KB.
- GitHub reports Anthropic `claude-api` at 324 lines / 209 LOC / 32.2 KB.
- GitHub reports Anthropic `xlsx` at 292 lines / 224 LOC / 11.2 KB.
- Superpowers' public debugging skill states a systematic approach can take 15-30 minutes versus 2-3 hours for random fixes, with first-time fix rate 95% versus 40%. Mythos should preserve that discipline while reducing activation load.
