---
schema_version: shared-doc.v1
category: architecture_template
applies_to: all-projects
sync_source: codex_standard/templates/shared-docs/ARCHITECTURE_TEMPLATE.md
---

# 架构文档模板

> 复制到项目 docs/ARCHITECTURE.md，填充项目特有内容。

```markdown
# {{PROJECT_NAME}} 架构文档

> updated: YYYY-MM-DD

## 红线

- （从全局红线目录引用，补充项目特有架构红线）
- 执行稳定性：禁止无边界递归扫描与长时间悬挂命令；搜索优先 `rg` 与精确路径，显式排除 `node_modules`、构建产物和其他大目录；预计超过 30 秒的验证必须拆成更小的单点命令。

## 架构总览

（架构图，描述组件关系和数据流）

## 技术栈

| 层 | 选型 | 版本 |
|---|---|---|
| 后端 | | |
| 前端 | | |
| 数据库 | | |
| 缓存 | | |
| 消息队列 | | |

## 目录结构

（项目目录树及各目录职责）

## 核心模块

### 模块 A

- 职责：
- 入口：
- 依赖：

### 模块 B

- 职责：
- 入口：
- 依赖：

## 数据模型

（核心数据表/模型定义）

## API 设计

（关键 API 端点列表）

## 部署架构

（容器编排、网络拓扑）

## 架构决策记录

| ADR | 决策 | 理由 | 日期 |
|---|---|---|---|
| ADR-001 | | | |

## 关联

- 全局红线 → docs/_shared/RED_LINES_CATALOG.md
- 开发环境约束 → docs/_shared/DEV_ENV_CONSTRAINTS.md
- Docker 铁律 → docs/_shared/DOCKER_IRON_LAWS.md
```

## 关联

- 功能宪章模板 → [CHARTER_TEMPLATE.md](./CHARTER_TEMPLATE.md)
- 基线模板 → [BASELINE_TEMPLATE.md](./BASELINE_TEMPLATE.md)



