# Command Rules

This document describes the public command-safety model behind Mythos-Skills.

It is adapted from the stricter WorkflowTemplate ruleset, but simplified for external readers and skill authors.

## Core Command Shape

### 1. Use one shell consistently

Prefer one predictable shell environment for a project so command approval and review are easier to reason about.

### 2. Keep Git commands direct

Preferred:

```text
git <subcommand> [args]
```

Avoid patterns that hide the real command behind wrappers:

```text
git -C <path> <subcommand>
cd <path>; git <subcommand>
cmd /c git ...
bash -c "git ..."
```

### 3. One invocation, one primary command

Preferred:

```text
git add .
git commit -m "..."
git push
```

Avoid:

```text
git add . && git commit -m "..." && git push
```

### 4. Avoid inline environment mutation

Prefer structured configuration or a separate setup step over:

```text
$env:FOO='bar'; command
```

### 5. Avoid shell-escape patterns

Public skills should not rely on patterns such as:

- `Invoke-Expression`
- `iex`
- `Start-Process`
- `Invoke-Command`
- `cmd /c`
- `bash -c`

These patterns make review and rule matching much weaker.

## Risk Tiers

| Tier | Meaning | Examples |
|---|---|---|
| Forbidden | Irreversible destructive actions | `git push --force`, `git reset --hard`, recursive force delete |
| Prompt: High Risk | Data-loss risk | branch deletion, file deletion, stash clear |
| Prompt: State Change | Safe enough to exist, but changes state | `git add`, `git commit`, install/remove deps |
| Prompt: Network | Download, upload, remote actions | `curl -o`, `ssh`, `gh pr create` |
| Prompt: Execution | Runs scripts or arbitrary code | `node`, `python`, `npx`, `go run` |
| Allow: Read Only | Pure inspection | `git status`, `git diff`, `Get-Content`, `Select-String` |

## Default Principle

Unknown commands should not silently pass.

The public rule philosophy is:

```text
explicitly safe = auto-allow
everything else = review or approval
```

## What This Means For Skill Authors

If your skill requires shell work, write it so that:

- the dangerous step is obvious
- the command is small and direct
- the user can review the action
- destructive operations are narrow and justified
- read-only inspection is separated from write actions
