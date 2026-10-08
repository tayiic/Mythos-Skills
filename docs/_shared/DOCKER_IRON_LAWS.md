---
schema_version: shared-doc.v1
category: docker_iron_laws
applies_to: all-projects-with-docker
sync_source: codex_standard/templates/shared-docs/DOCKER_IRON_LAWS.md
---

# Docker 容器铁律（全局强制）

> 本文件由 sync-engine 自动同步到项目 docs/_shared/。项目 docs/DEV_DOCKER_PATTERN.md 引用本文件，不复制内容。

## 铁律 1：源码 bind mount

- 开发容器是「空壳 + 通道」——镜像只装**依赖、init 脚本、默认配置**
- **源码与 dev 配置全部 bind mount 自主机**
- Dockerfile 中禁止 COPY 源码目录（COPY requirements.txt / pyproject.toml 等依赖声明文件除外）

## 铁律 2：容器 runtime 必须 offline

- **所有依赖（含 dev/test）必须在 `docker build` 阶段装进镜像**
- 容器启动后**禁止**任何网络请求安装依赖：
  - `pip install` / `npm install` / `apt-get install` / `apk add` / `go get` / `cargo build`
  - 一律不允许出现在 entrypoint / command / start.sh 中
- 违反此铁律的容器配置必须立即修正

## 验证命令

```powershell
# 检查容器是否 offline（依赖应已预装）
docker exec <container> pip list
docker exec <container> npm list --depth=0

# 检查 entrypoint 是否包含 install 命令
docker inspect <container> --format='{{.Config.Entrypoint}} {{.Config.Cmd}}'
```

## 例外

| 项目 | 例外 | 原因 |
|---|---|---|
| 无 | 无例外 | — |

## 关联

- 开发环境约束 → [DEV_ENV_CONSTRAINTS.md](./DEV_ENV_CONSTRAINTS.md)
- 全局红线目录 → [RED_LINES_CATALOG.md](./RED_LINES_CATALOG.md)
