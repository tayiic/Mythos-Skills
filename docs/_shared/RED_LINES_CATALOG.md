---
schema_version: shared-doc.v1
category: red_lines_catalog
applies_to: all-projects
sync_source: codex_standard/templates/shared-docs/RED_LINES_CATALOG.md
---

# 全局红线目录

> 所有项目必须遵守的红线。项目特有红线在各项目 `.trae/rules/01-RED_LINES.md` 中补充。
> 本文件由 sync-engine 自动同步，禁止项目手动修改。

| # | 红线 | 检测方法 | 违反后果 |
|---|------|---------|---------|
| G1 | 容器 runtime 必须 offline | entrypoint/command 中出现 install 命令 | 立即终止 |
| G2 | 源码 bind mount（禁止 COPY 源码） | Dockerfile 中 COPY 源码目录 | 立即终止 |
| G3 | 后端测试必须在容器内 | 宿主机执行 pytest | 测试无效 |
| G4 | 镜像 tag 禁止 :latest | docker-compose.yml 中 image: xxx:latest | 部署拒绝 |
| G5 | 禁止 runtime 安装依赖 | start.sh 中出现 install | 立即终止 |
| G6 | git push --force 禁止 | 命令匹配 | 立即终止 |
| G7 | 密钥/Token 禁止入库 | secret scan (12+3 模式) | 立即终止 |
| G8 | 敏感信息需标注 | 无 EXPOSABLE 标注的明文敏感信息 | 审计警告 |
| G9 | Node 版本统一 22（RC 除外 16） | Dockerfile FROM node:XX | 构建拒绝 |
| G10 | 改库必 dry-run | 直接执行 migration | 立即终止 |
| G11 | 禁止 TODO/FIXME/HACK 占位符入库 | grep 扫描 | 提交拒绝 |
| G12 | 依赖锁定（lockfile 必须） | 无 lockfile | 构建拒绝 |
| G13 | 禁止无边界递归扫描与长时间悬挂命令 | 命令审计（扫描大目录、单命令超过 30 秒） | 立即终止 |
| G14 | 多 IDE 同步铁律 | 三端文档语义差异检测（sync-engine -Status --deep） | 立即终止 |
| G15 | 测试命令锁定 | 白名单外测试命令（非 TEST_SCENARIOS.md 声明） | 立即终止 |
| G16 | 宿主脚本壳层规范 | Windows 调用 .sh 脚本未走 pwsh.exe -NoProfile -Command "bash ./..." | 立即终止 |
| G17 | 测试代理隔离 | 主协调线程直接执行 cargo/pytest/npm test/clippy/build/bench/E2E | 立即终止 |
| G18 | 强制留档铁律 | 7 类事件未同回合留档（OBS/INC/DEBT/ADR/RISK/REQ/LESSON） | 立即终止 |
| G19 | Sandbox helper 恢复纪律 | 写入前失败未查 setup/sandbox 日志；用任意 shell 绕过；默认要求重开；未获显式批准修改 ACL | 立即终止并按权限运行手册 §10 恢复 |

## 项目特有红线

各项目在 `.trae/rules/01-RED_LINES.md` 中定义项目特有的红线，编号从 P1 开始。

## 关联

- Docker 铁律 → [DOCKER_IRON_LAWS.md](./DOCKER_IRON_LAWS.md)
- 敏感信息策略 → [SENSITIVE_INFO_POLICY.md](./SENSITIVE_INFO_POLICY.md)
- 开发环境约束 → [DEV_ENV_CONSTRAINTS.md](./DEV_ENV_CONSTRAINTS.md)
- 权限与 Sandbox 恢复 → [CODEX_PERMISSION_APPROVAL_RUNBOOK.md](./CODEX_PERMISSION_APPROVAL_RUNBOOK.md)

