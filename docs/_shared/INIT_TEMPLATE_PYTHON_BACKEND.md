---
schema_version: shared-doc.v1
category: init_template
applies_to: python-backend-projects
sync_source: codex_standard/templates/shared-docs/INIT_TEMPLATE_PYTHON_BACKEND.md
---

# Python / 后端服务初始化模板

适用: FastAPI、Flask、Celery、数据同步脚本、服务端 Python、混合 Python + Docker 项目。

## 必检文件

| 文件 | 必检内容 |
|------|----------|
| `pyproject.toml` / `requirements.txt` | Python 版本、依赖来源、测试工具、ruff/mypy/pytest 配置 |
| `backend/Dockerfile` / `Dockerfile` | 基础镜像、依赖安装阶段、运行用户、端口、healthcheck |
| `docker-compose*.yml` | 服务名、端口、volume、env_file、数据库/redis |
| `.env.example` / `.env.dev` | 可提交默认值，不含真密钥 |
| `settings.py` / `config.py` | 环境选择、数据库 URL、生产保护 |
| `scripts/pre_test_safety_check.ps1` | ENV、数据库、容器、镜像、密钥门禁 |

## 初始化步骤

1. 确认 Python 版本和依赖管理方式: `venv`、`pip`、`uv`、`poetry`、容器内依赖。
2. 确认运行边界: 宿主机可运行，还是必须通过 `docker exec` / `docker compose run`。
3. 确认数据库: 类型、主机、端口、库名、迁移工具、dry-run/apply 分界。
4. 确认测试命令: 单测、集成、迁移检查、最小回归集合。
5. 确认生产保护: 生产 ENV、生产 DB、生产写脚本是否有显式 apply/confirm 门。

## 配置记录模板

| 配置项 | 开发值来源 | 生产值来源 | 是否敏感 | 说明 |
|--------|------------|------------|----------|------|
| `ENV` / `APP_ENV` | 环境变量或 `.env.dev` | runtime 注入 | 否 | 测试不得为 production |
| `DB_HOST` | `.env.dev` / compose | runtime 注入 | 否 | 容器访问宿主机常用 `host.docker.internal` |
| `DB_PASSWORD` | `.env` / secret manager | runtime 注入 | 是 | 不入库 |
| `SECRET_KEY` | 本地生成 | secret manager | 是 | 不入库 |

## 测试门禁

- 容器化后端默认禁止宿主机直接 `pytest`，除非项目文档明确允许。
- 数据迁移、同步、清库、生产初始化脚本默认 dry-run；apply 必须显式参数。
- 任何测试必须先确认 ENV、DATABASE_URL、容器名、镜像 tag。

## 常见证据

- `docker ps --filter name=<container>`
- `docker exec <container> python -m pytest ...`
- `docker exec <container> alembic current`
- `python -m pytest <focused-test> -q`（仅限宿主机测试被允许的项目）
