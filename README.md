# Mythos-Skills Workspace

这是 Mythos-Skills 的本地工作区，不是对外发布仓库。

## 仓库边界

- 根目录 Git 只做本地保存，不推送到远程。
- `docs/` 保存项目蓝图、迁移清单、调研结论和内部决策记录。
- `pub/` 是独立开源仓库，里面维护自己的 `.git/`，远程目标为 `git@github.com:tayiic/Mythos-Skills.git`。
- 对外发布、开源协作、GitHub README、License、贡献指南等都放在 `pub/` 下。

## 当前定位

Mythos-Skills 不是普通 skill 集合，而是 AI Agent Skill Engineering 的方法论仓库。它基于对大量 skill 仓库的调研，聚焦一个更高层级的问题：

> 如何让人类和 AI 都能稳定写出 production-grade skills?

核心叙事围绕三件事：

- 8 条 P1-P8 核心原则，回答什么是好 skill。
- 原则驱动的 `skill-creator`，把方法论变成可执行流程。
- before/after gallery，用真实 skill 重构展示 token、触发、依赖和安全性的提升。

## 操作约定

根目录用于规划和本地沉淀：

```powershell
git status
git add README.md docs .gitignore
git commit -m "docs: initialize local Mythos-Skills workspace"
```

`pub/` 用于公开发布：

```powershell
cd pub
git status
git remote -v
git add .
git commit -m "chore: initialize Mythos-Skills"
git push -u origin main
```

不要从根目录把 `pub/` 作为普通目录提交；它是单独项目。
