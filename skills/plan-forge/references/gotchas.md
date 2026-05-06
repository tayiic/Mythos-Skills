# Plan Forge Gotchas

## Common Planning Anti-Patterns

### 1. The "Implement Everything" Task
```
❌ T1: Implement the full user management system
```
This is not a task, it's an epic. Break it down until each task is a single file change.

### 2. The Implicit Dependency
```
❌ T2: Add the validation (same pattern as T1)
```
"Same pattern as T1" requires reading T1. Each task must be self-contained (P3).

### 3. The Vague Verification
```
❌ T3: Make sure it works
```
"Works" is not verifiable. Use specific commands: `pytest tests/test_feature.py::test_happy_path`

### 4. The Context-Dependent Task
```
❌ T4: Fix the issue we discussed earlier
```
Plans outlive conversations. Each task must contain all needed context within itself.

### 5. The Over-Planned Task
```
❌ T5: In src/api/users.py, add a new endpoint POST /users that accepts JSON with
      fields name (string, required), email (string, required, validated), role
      (enum: admin/user, default: user), and returns 201 with the created user...
```
This level of detail belongs in `references/`, not in the task line. Keep tasks ≤ 10 words of description.

### 6. The Missing Gotcha Section
Plans that don't list known pitfalls cause executors to repeat the same mistakes. Always include at least one gotcha, even if it's "None known yet."

### 7. The Unbounded Plan
A plan with 15 tasks is not a plan — it's a backlog. Split into sub-plans of ≤ 7 tasks each. The cognitive limit for holding plan context is roughly 7 items (Miller's Law).
