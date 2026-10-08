---
schema_version: shared-doc.v1
category: test_deploy_template
applies_to: all-projects-with-docker
sync_source: codex_standard/templates/shared-docs/TEST_DEPLOY_TEMPLATE.md
---

# 测试与部署模板

> 包含生产测试部署和开发测试部署两个模板。

## 生产测试与部署模板

> 复制到项目 docs/TEST_DEPLOY-PROD.md

```markdown
# {{PROJECT_NAME}} 生产测试与部署

## 红线

- 生产镜像 tag 禁止 :latest
- 改库必 dry-run
- 容器 runtime 必须 offline
- 后端测试必须在容器内

## 部署流程

1. 确认基线文档 tag 已更新
2. docker compose build
3. docker compose up -d
4. 健康检查：curl -s localhost:PORT/health
5. 冒烟测试：docker exec <c> pytest tests/smoke/

## 回滚流程

1. docker compose down
2. 切换到上一版本 tag
3. docker compose up -d
4. 验证健康检查
```

## 开发测试与部署模板

> 复制到项目 docs/TEST_DEPLOY-DEV.md

```markdown
# {{PROJECT_NAME}} 开发测试与部署

## 红线

- 后端容器 + 前端本地
- 容器 runtime 必须 offline
- 后端测试必须在容器内

## 开发启动

1. docker compose up -d
2. 前端：pnpm dev
3. 验证：curl -s localhost:PORT/health

## 测试

- 单元测试：docker exec <c> pytest tests/ -v
- 单个测试：docker exec <c> pytest tests/test_xxx.py -v
- 前端测试：pnpm test

## 重建镜像

1. 修改依赖后：docker compose build --no-cache
2. 更新基线文档 tag
```

## 关联

- 基线模板 → [BASELINE_TEMPLATE.md](./BASELINE_TEMPLATE.md)
- Docker 铁律 → [DOCKER_IRON_LAWS.md](./DOCKER_IRON_LAWS.md)
