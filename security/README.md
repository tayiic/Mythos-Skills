# Security Model

Mythos-Skills treats command safety as part of skill quality, not as an afterthought.

The public model has three layers:

| Layer | Purpose |
|---|---|
| L0: Authoring rules | How a skill should describe dangerous operations |
| L1: Command rules | How shell commands are classified and constrained |
| L2: Project constraints | What must stay local, protected, or human-reviewed |

## Design Goals

- Keep dangerous operations explicit.
- Prefer narrow, reviewable commands over broad shell wrappers.
- Make copyable skills safer by default.
- Separate reusable public rules from machine-local secrets and approvals.

## Documents

- [COMMAND_RULES.md](COMMAND_RULES.md): public command-rule model
- [GLOBAL_CONSTRAINTS.md](GLOBAL_CONSTRAINTS.md): protected-file and config constraints

## Rule Philosophy

Good skills should not hide risk behind convenience.

If a workflow can delete, overwrite, publish, install, execute arbitrary code, or access the network, the skill should say so clearly and route that behavior through explicit steps, checks, or user approval.
