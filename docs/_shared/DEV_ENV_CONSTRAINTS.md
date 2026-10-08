---
schema_version: shared-doc.v1
category: dev_env_constraints
applies_to: all-projects-with-docker
sync_source: codex_standard/templates/shared-docs/DEV_ENV_CONSTRAINTS.md
---

# 开发环境约束

> 本文件由 sync-engine 自动同步，禁止项目手动修改。

## 标准模式：后端容器 + 前端本地

| 组件 | 运行位置 | 理由 |
|---|---|---|
| 后端 | Docker 容器 | 环境隔离，依赖锁定 |
| 前端 | 宿主机本地 | HMR 快，调试方便 |
| 数据库 | Docker 容器 | 环境隔离 |

## 容器内必须工具

| 工具 | 用途 | 检查命令 |
|---|---|---|
| pytest | 后端测试 | `docker exec <c> pytest --version` |
| ruff | 代码检查 | `docker exec <c> ruff --version` |
| mypy | 类型检查 | `docker exec <c> mypy --version` |
| ps | 进程检查 | `docker exec <c> ps aux` |
| curl | 健康检查 | `docker exec <c> curl -s localhost:PORT/health` |

## 前端必须工具

| 工具 | 用途 |
|---|---|
| pnpm | 包管理 |
| vitest | 单元测试 |
| playwright | E2E 测试 |

## 版本约束

| 运行时 | 版本 | 例外 |
|---|---|---|
| Node.js | 22 | RC 项目使用 16 |
| Python | 3.12 | — |

## 关联

- Docker 铁律 → [DOCKER_IRON_LAWS.md](./DOCKER_IRON_LAWS.md)
- 全局红线 G9 → [RED_LINES_CATALOG.md](./RED_LINES_CATALOG.md)
