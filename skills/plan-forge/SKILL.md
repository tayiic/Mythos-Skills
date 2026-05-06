---
name: "plan-forge"
description: "当需求模糊、任务复杂度超过单次实现、或需要将大目标拆解为可执行步骤时触发。将模糊想法锻造为 bite-sized 行动计划。"
version: "1.0"
---

# Plan Forge (计划锻造)

## Activation
- **Role**: Senior Staff Engineer — plans are specs for zero-context executors
- **Philosophy**: A plan is only good if a tired, context-free developer can execute each step in 2-5 minutes

## Execution Flow
1. **Clarify Intent** → Ask up to 5 Socratic questions; stop when goal is unambiguous
2. **Decompose** → Break into tasks where each task = one file change + one test
3. **Sequence** → Order by dependency; mark parallelizable tasks with `∥`
4. **Write Plan** → Output to `.plan/plan.md` following the template below
5. **Validate** → Self-check: can each task be done without reading other tasks?

## Plan Template (`.plan/plan.md`)
```markdown
# Plan: <goal-in-10-words>
## Context (≤3 lines)
## Tasks
- [ ] T1: <verb> <what> in <file> → <test> ∥
- [ ] T2: ...
## Gotchas
- <known pitfall>
```

## Constraints
- Max 7 tasks per plan (P1: concise); split into sub-plans if more
- Each task must specify exact file path (P7: code over instructions)
- Plan state persists in `.plan/` (P8: externalize memory)
- No task may depend on implicit context (P3: self-contained)

## References
- See [plan_quality_criteria.md](references/plan_quality_criteria.md) for what makes a plan "good"
- See [gotchas.md](references/gotchas.md) for common planning anti-patterns
