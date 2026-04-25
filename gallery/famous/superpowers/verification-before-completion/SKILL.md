---
name: verification-before-completion-optimized
description: Use before saying work is complete, especially after code, docs, tests, generated assets, or repository state changed.
---

# Verification Before Completion Optimized

Done means checked.

## Flow

1. Identify the promised outcome.
2. Run the narrowest meaningful verification.
3. Inspect generated or user-facing artifacts.
4. Report exact checks performed and any gaps.
5. Do not claim success if verification failed or was skipped.

## Gotchas

- Do not rely on intuition after edits.
- Do not hide unrun tests.
- Do not call a visual artifact done without visual inspection.
