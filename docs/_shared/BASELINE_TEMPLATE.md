---
schema_version: shared-doc.v1
category: baseline_template
applies_to: all-projects-with-docker
sync_source: codex_standard/templates/shared-docs/BASELINE_TEMPLATE.md
---

# 生产基线文档模板

> 复制到项目 docs/BASELINE-PROD.md，填充项目特有内容。

```markdown
# {{PROJECT_NAME}} 生产基线

> updated: YYYY-MM-DD
> 镜像构建后必须更新本文档的 tag 和版本链

## 当前交付物

| 组件 | 镜像/版本 | Tag | 端口 |
|---|---|---|---|
| 后端 | {{PROJECT}}:latest | v1.0.0 | 8000 |
| 前端 | 静态文件 | — | 3000 |
| 数据库 | postgres:16 | 16-alpine | 5432 |

## 红线

- 镜像 tag 禁止 :latest（生产环境）
- 改库必 dry-run
- 容器 runtime 必须 offline

## 版本链

| 日期 | Tag | 变更摘要 |
|---|---|---|
| YYYY-MM-DD | v1.0.0 | 初始版本 |

## 配置约束

| 配置项 | 值 | 来源 |
|---|---|---|
| DB_HOST | postgres | docker-compose |
| DB_PORT | 5432 | docker-compose |
| SECRET_KEY | $env:SECRET_KEY | .env |
```

## 关联

- Docker 铁律 → [DOCKER_IRON_LAWS.md](./DOCKER_IRON_LAWS.md)
- 开发环境约束 → [DEV_ENV_CONSTRAINTS.md](./DEV_ENV_CONSTRAINTS.md)
