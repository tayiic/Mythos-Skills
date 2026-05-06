# Skill Authoring Principles (P1-P8)

> The 8 iron principles that separate production-grade AI agent skills from broken ones.
> Derived from Anthropic official guides, Karpathy's context engineering, Thariq's progressive disclosure, and production practice.

---

## P1: Concise is Key (简洁即正义)

**Context window is a public good. Every token you waste is a token the agent can't use for reasoning.**

| Aspect | Detail |
|--------|--------|
| Authority | Anthropic: "Skills should be concise — the agent loads them into context every activation" |
| Rule | SKILL.md ≤ 55 lines. Everything else goes to `references/` |
| Anti-pattern | SKILL.md bloated to 200+ lines → context pollution, slower reasoning, higher cost |
| Consequence | Activation cost scales linearly with SKILL.md size; 200-line skill = 4x the token waste of a 50-line skill |

**Before (❌):**
```
SKILL.md: 180 lines of inline documentation, examples, edge cases, scripts...
→ Agent loads 180 lines every single activation, even for simple tasks
```

**After (✅):**
```
SKILL.md: 42 lines (entry point only)
references/: detailed docs loaded on demand
→ Agent loads 42 lines on activation, reads references only when needed
```

---

## P2: Progressive Disclosure (渐进式披露)

**Load on demand, never preload. The agent should see the skeleton first, details only when it asks.**

| Aspect | Detail |
|--------|--------|
| Authority | Thariq (Anthropic Internal): "The best skills use progressive disclosure — MINI files that expand" |
| Rule | Three-layer architecture: SKILL.md (skeleton) → references/ (details) → operations.json (machine index) |
| Anti-pattern | Everything in one file → agent can't skip irrelevant sections |
| Consequence | DataCamp research shows optimal instruction budget is 150-200 items; exceeding this degrades performance |

**Three-Layer Model:**
```
Layer 1: SKILL.md        → ~55 lines, the only file loaded on activation
Layer 2: references/*.md  → loaded only when the agent needs specific details
Layer 3: operations.json  → machine-readable command index for tool integration
```

---

## P3: Self-Contained (自包含独立)

**Each skill is an independent, portable atom. Zero external dependencies.**

| Aspect | Detail |
|--------|--------|
| Authority | Anthropic Skill Guide: "Skills should work when copied to any project" |
| Rule | No cross-directory references (`../other-skill/references/`), no project-specific paths, no external scripts |
| Anti-pattern | Skill references `../GLOBAL_SKILL_PROTOCOL.md` → breaks when copied alone |
| Consequence | Non-portable skills create hidden dependency chains; copy-paste silently breaks them |

**Violation Detection:**
```bash
# Any of these in SKILL.md = P3 violation
grep -r '\.\./' SKILL.md
grep -r '<other-skill>/' SKILL.md
grep -r 'harness_guard\|GLOBAL_SKILL' SKILL.md
```

---

## P4: Match Freedom to Fragility (自由度匹配)

**Fragile operations get low freedom; creative tasks get high freedom.**

| Aspect | Detail |
|--------|--------|
| Authority | Anthropic: "Constrain dangerous operations, allow flexibility for creative ones" |
| Rule | Destructive ops (delete, deploy, merge) → explicit confirmation + narrow scope. Creative ops (draft, brainstorm) → open-ended freedom |
| Anti-pattern | Same freedom level for `rm -rf` and `draft a README` |
| Consequence | Over-constraining creative tasks produces rigid output; under-constraining destructive ops causes damage |

**Freedom Spectrum:**
```
Low Freedom ←────────────────────────────────→ High Freedom
  DELETE files    RUN tests    REFACTOR code    DRAFT docs    BRAINSTORM ideas
  (confirm each)  (auto-run)   (show plan)      (auto-draft)  (open-ended)
```

---

## P5: Trigger > Description (触发优于描述)

**Write "when to use" in description, not "what it does". The agent needs to know WHEN to activate, not WHAT happens after.**

| Aspect | Detail |
|--------|--------|
| Authority | Anthropic: "description should help the agent decide whether to activate this skill" |
| Rule | description = trigger condition (when/where/scenario), not capability list |
| Anti-pattern | `description: "Code review skill that checks security, style, and tests"` → agent doesn't know WHEN to use it |
| Consequence | Vague descriptions cause wrong activations or missed activations |

**Before (❌):**
```yaml
description: "审查机制。由各领域专家对代码与产物进行并行审查。"
```

**After (✅):**
```yaml
description: "当任务进入交付阶段、PR 已提交、或代码变更超过 50 行时触发审查。"
```

---

## P6: Gotchas are Gold (踩坑点即金矿)

**Repeated failure patterns are more valuable than success guides. Document what goes wrong, not just what should go right.**

| Aspect | Detail |
|--------|--------|
| Authority | Thariq: "The most valuable part of a skill is the list of things that repeatedly break" |
| Rule | Every skill must include a `gotchas` or `anti-patterns` section in references/ |
| Anti-pattern | Skill only documents the happy path → agent repeats the same mistakes |
| Consequence | Without gotchas, each new agent session re-discovers the same failures |

**Gotcha Template:**
```markdown
## Gotchas
- **Async context loss**: React/Vue async callbacks must check `isMounted()` / `isCurrent()`
- **Silent failure**: External calls without try-catch swallow errors silently
- **State in context**: FSM state stored in conversation is lost after 10+ turns
```

---

## P7: Code over Instructions (脚本优于指令)

**Give the agent executable scripts, let it orchestrate — don't make it construct boilerplate from prose.**

| Aspect | Detail |
|--------|--------|
| Authority | Thariq: "Provide scripts, not instructions to write scripts" |
| Rule | Prefer `operations.json` with command templates over prose descriptions of what to run |
| Anti-pattern | "Run pytest with coverage flags" → agent constructs the command, may get flags wrong |
| Consequence | Prose instructions waste tokens + introduce uncertainty; scripts are deterministic |

**Before (❌):**
```markdown
Run the test suite with coverage enabled, then check if coverage is above 80%.
```

**After (✅):**
```json
{
  "commands": {
    "test_with_coverage": "pytest --cov=src --cov-fail-under=80 --tb=short"
  }
}
```

---

## P8: Externalize Memory (记忆外置)

**State belongs in files, not in conversation context. The agent should be able to resume from files after context reset.**

| Aspect | Detail |
|--------|--------|
| Authority | Phil Schmid / SCOFI: "Single Context of Focus and Intent — persist state externally" |
| Rule | All mutable state (FSM phase, task progress, decisions) must be written to files |
| Anti-pattern | "Remember that we decided to use PostgreSQL" → lost after context window fills |
| Consequence | Context-only state creates fragile sessions; any interruption loses all progress |

**State File Pattern:**
```
.plan/state.json    → current phase, active tasks, completed steps
.plan/decisions.md  → key decisions with rationale
```

---

## Quick Reference Card

| # | Principle | One-Liner | Key Metric |
|---|-----------|-----------|------------|
| P1 | Concise is Key | Context window is a public good | SKILL.md ≤ 55 lines |
| P2 | Progressive Disclosure | Load on demand, never preload | 3-layer architecture |
| P3 | Self-Contained | Each skill is an independent atom | Zero external refs |
| P4 | Match Freedom | Fragile ops = low freedom | Freedom spectrum |
| P5 | Trigger > Description | Write "when to use" | description = trigger |
| P6 | Gotchas are Gold | Failure patterns > success guides | gotchas section required |
| P7 | Code over Instructions | Give scripts, not prose | operations.json |
| P8 | Externalize Memory | State in files, not context | State file pattern |
