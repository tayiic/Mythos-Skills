---
name: claude-api-optimized
description: Use when implementing, reviewing, or debugging Claude API calls and you need safe provider-specific guidance without loading a huge API manual.
---

# Claude API Optimized

Treat this as a router, not a manual.

## Flow

1. Identify task type: messages, streaming, tools, files, batches, evals, or migration.
2. Load only the relevant local reference.
3. Check auth, model name, request shape, retries, and error handling.
4. Prefer typed helpers or SDK examples over handwritten JSON.
5. Before completion, verify no secrets, logs, or API keys are exposed.

## Gotchas

- Do not mix old and new request shapes.
- Do not hardcode keys.
- Do not retry unsafe non-idempotent operations blindly.

See `references/workflow.md`.
