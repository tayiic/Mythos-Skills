# Plan Quality Criteria

## What Makes a Plan "Good"

A plan is a spec for a zero-context executor. Quality is measured by executability, not comprehensiveness.

### Mandatory Criteria

| # | Criterion | Check | Pass If |
|---|-----------|-------|---------|
| 1 | **Atomicity** | Each task touches ≤ 2 files | One file change + one test file |
| 2 | **Specificity** | Each task names exact file path | `src/auth/login.py` not "the auth file" |
| 3 | **Testability** | Each task has a verification step | `→ pytest tests/auth/test_login.py` |
| 4 | **Independence** | Each task is self-describing | No "as discussed above" references |
| 5 | **Boundedness** | Plan has ≤ 7 tasks | Split into sub-plans if more needed |

### Task Format

```
- [ ] T<n>: <verb> <what> in <file> → <verification> [∥]
```

Components:
- `<verb>`: CREATE / MODIFY / DELETE / REFACTOR / FIX
- `<what>`: specific change description (≤ 10 words)
- `<file>`: exact relative path
- `<verification>`: command or check to confirm success
- `∥`: optional marker meaning "parallelizable with other ∥ tasks"

### Good vs Bad Examples

**Bad (❌):**
```
- [ ] T1: Implement the authentication system
- [ ] T2: Add tests
- [ ] T3: Update the docs
```
Problems: T1 is not atomic, T2 has no specific test file, T3 is vague.

**Good (✅):**
```
- [ ] T1: CREATE login handler in src/auth/login.py → pytest tests/auth/test_login.py::test_login_success ∥
- [ ] T2: CREATE token validator in src/auth/token.py → pytest tests/auth/test_token.py::test_expired_token ∥
- [ ] T3: MODIFY router to add /auth/* routes in src/router.py → pytest tests/test_routes.py::test_auth_routes
```

## Plan Size Guidance

| Scope | Tasks | Strategy |
|-------|-------|----------|
| Bug fix | 1-3 | Single plan |
| Feature | 3-7 | Single plan |
| Epic | 7+ | Split into sub-plans (each ≤ 7 tasks) |

Sub-plans are linked via `.plan/subplans/` directory:
```
.plan/
├── plan.md              # Master plan with sub-plan references
└── subplans/
    ├── 01-auth.md       # Sub-plan: authentication
    └── 02-rbac.md       # Sub-plan: role-based access
```
