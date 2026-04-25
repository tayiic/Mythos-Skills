---
name: test-driven-development-optimized
description: Use when implementing behavior that can be specified with tests, especially bug fixes, refactors, and user-visible logic changes.
---

# TDD Optimized

No production change before a failing test.

## Flow

1. Write the smallest failing test for the desired behavior or bug.
2. Run it and confirm it fails for the right reason.
3. Implement the smallest change that passes.
4. Run the relevant test set.
5. Refactor only with tests green.

## Gotchas

- Do not write tests after implementation and call it TDD.
- Do not overfit to mocks if behavior can be tested directly.
- Do not skip the failing-test proof.
