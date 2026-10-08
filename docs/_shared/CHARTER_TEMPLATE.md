---
schema_version: shared-doc.v1
category: charter_template
applies_to: all-projects
sync_source: codex_standard/templates/shared-docs/CHARTER_TEMPLATE.md
---

# 功能宪章模板

> 复制到项目根目录为 CHARTER.md，填充项目特有内容后交互式确认。

```markdown
# {{PROJECT_NAME}} 功能宪章

> status: draft → confirmed（交互式确认后锁定）
> confirmed_at: YYYY-MM-DD
> confirmed_by: user

## 使命

一句话描述项目存在的目的。

## 核心功能（MVP 范围）

1. 功能 A — 简述
2. 功能 B — 简述
3. 功能 C — 简述

## 明确不做

- 不做 X
- 不做 Y
- 不做 Z

## 架构约束

- 约束 1（如：单容器架构）
- 约束 2（如：后端容器 + 前端本地）

## 技术栈

| 层 | 选型 | 版本 |
|---|---|---|
| 后端 | FastAPI | 0.110+ |
| 前端 | Vue3 + TypeScript | 3.4+ |
| 数据库 | PostgreSQL | 16 |
| 容器 | Docker | 24+ |

## 验收标准

- [ ] 核心功能 1 可运行
- [ ] 核心功能 2 可运行
- [ ] 容器 offline 启动
- [ ] 后端测试在容器内通过
```

## 确认流程

1. AI 使用 AskUserQuestion 逐项确认
2. 用户确认后 status → confirmed
3. confirmed 后任何修改需用户再次确认
4. CHARTER.md 的 confirmed_at 时间戳用于漂移检测
