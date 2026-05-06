# Mythos-Skills Workspace

这是 Mythos-Skills 的本地工作区，不是对外发布仓库。

## 仓库边界

- 根目录 Git 只做本地保存，不推送到远程。
- `docs/` 保存项目蓝图、迁移清单、调研结论和内部决策记录。
- `pub/` 是独立开源仓库，里面维护自己的 `.git/`，远程目标为 `git@github.com:tayiic/Mythos-Skills.git`。
- 对外发布、开源协作、GitHub README、License、贡献指南等都放在 `pub/` 下。
- `pub/` 的发布设计、README 策略、增长策略统一沉淀到 `docs/PUB_REPOSITORY_DESIGN.md`；后续设计文档不要求同步到 `pub/docs/`。

## 当前定位

Mythos-Skills 不是普通 skill 集合，而是 AI Agent Skill Engineering 的方法论仓库。它基于对大量 skill 仓库的调研，聚焦一个更高层级的问题：

> 如何让人类和 AI 都能稳定写出 production-grade skills?

核心叙事围绕三件事：

- 8 条 P1-P8 核心原则，回答什么是好 skill。
- 原则驱动的 `skill-creator`，把方法论变成可执行流程。
- before/after gallery，用真实 skill 重构展示 token、触发、依赖和安全性的提升。

## 设计文档

- [项目蓝图](docs/MYTHOS_SKILLS_PROJECT_BLUEPRINT.md)
- [迁移清单](docs/MYTHOS_SKILLS_MIGRATION_CHECKLIST.md)
- [pub 开源仓库设计方案](docs/PUB_REPOSITORY_DESIGN.md)
- [v002 方法论扩展参考](docs/v002参考.md)

## 更新记录

### v0.2 (2026-05-06)

- **蓝图新增第十节**：v002 方法论扩展 — M7 计划驱动开发、M8 代码审查框架、M9 验证三角，以及 8 Skills 生命周期覆盖计划 (S1-S8)
- **新增 P1-P8 核心原则文档**：`principles/SKILL_AUTHORING_PRINCIPLES.md`，每条原则含权威来源、核心规则、反模式、Before/After 对比
- **新增 S1 plan-forge Skill**：v002 优先级 #1 的新建 Skill，三层架构 (SKILL.md 39行 + references/ + operations.json)，严格遵循 P1-P8
- **已有项目优化洞察**：审查 trae_standard_harness 中 6 大系统性问题，映射到 P1-P8 违规项

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
