---
schema_version: shared-doc.v1
category: init_template
applies_to: rust-system-projects
sync_source: codex_standard/templates/shared-docs/INIT_TEMPLATE_RUST_SYSTEM.md
---

# Rust / 系统服务初始化模板

适用: Rust 服务、采集器、高性能数据处理、CLI、系统组件、Rust + Docker 项目。

## 必检文件

| 文件 | 必检内容 |
|------|----------|
| `Cargo.toml` | package、edition、features、bin/lib、依赖 |
| `Cargo.lock` | 应用项目必须锁定 |
| `.cargo/config.toml` | registry、offline、target、linker |
| `Dockerfile` | toolchain、vendor、offline build、runtime 镜像 |
| `docker-compose*.yml` | 容器名、挂载、端口、环境变量 |
| `scripts/check_env.*` | 编译、运行、依赖、生产路径检查 |

## 初始化步骤

1. 确认 Rust edition、toolchain、target 和是否要求 offline。
2. 确认 crate 边界: workspace、bin、lib、examples、bench。
3. 确认测试命令: `cargo test`、focused test、integration test、bench、clippy。
4. 确认错误处理红线: 生产路径禁止随意 `unwrap()` / `expect()`，明确 panic 边界。
5. 确认数据路径和挂载: 容器内路径、宿主机路径、只读/读写边界。

## 验证门禁

- 优先运行 `cargo check` 或项目指定 focused test。
- 生产数据采集/录制/回放项目必须区分 parser/sink/publish/drop/ACL 等边界。
- Docker 镜像若声明自包含，必须验证 `docker load` 后无网络依赖。

## 常见证据

- `cargo check`
- `cargo test <module_or_case>`
- `cargo clippy -- -D warnings`
- `docker exec <container> <project-command>`
- `docker inspect <container> --format '{{json .Mounts}}'`
