---
name: requesting-code-review-optimized
description: Use before finalizing a non-trivial code change, especially when behavior, security, data, or public API contracts may be affected.
---

# Requesting Code Review Optimized

Ask for review with evidence, not vibes.

## Flow

1. Summarize the change and why it exists.
2. List files changed and risk areas.
3. Include tests or verification commands run.
4. Ask reviewers to focus on specific concerns.
5. Do not merge unresolved correctness or safety questions.

## Gotchas

- Do not ask for review without a test story.
- Do not bury risky changes in formatting noise.
- Do not treat approval as a substitute for verification.
