---
name: systematic-debugging-optimized
description: Use when a bug is unclear, recurring, high-risk, or already resisted a quick fix, and you need root-cause debugging before changing code.
---

# Systematic Debugging Optimized

Do not patch symptoms. Prove the cause.

## Flow

1. Reproduce the failure or capture the exact observed evidence.
2. State the smallest hypothesis that explains it.
3. Add instrumentation or a focused test to confirm or falsify.
4. Fix only after the cause is proven.
5. Keep the regression test or verification artifact.

## Gotchas

- Do not change multiple variables at once.
- Do not trust logs without checking timestamps and inputs.
- Do not stop at "works now"; explain why.
