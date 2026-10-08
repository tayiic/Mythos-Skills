---
schema_version: shared-doc.v1
category: init_template
applies_to: docs-skills-research-projects
sync_source: codex_standard/templates/shared-docs/INIT_TEMPLATE_DOCS_SKILLS.md
---

# 文档 / 技能 / 研究型项目初始化模板

适用: 规范仓库、技能仓库、论文/实验项目、资料库、纯文档项目、轻量脚本项目。

## 必检文件

| 文件 | 必检内容 |
|------|----------|
| `README.md` | 项目目的、目录导航、主要任务 |
| `AGENTS.md` / `CLAUDE.md` | AI 执行边界、文档更新规则、验证方式 |
| `project-preset.json` | 标准同步身份，即便无 runtime 也要声明 |
| `docs/INDEX.md` / `MASTER_PROGRESS.md` | 文档导航和当前进度 |
| `pyproject.toml` / `package.json` | 若有脚本或构建工具，必须记录命令 |
| `.archive/` / `.trash/` | 历史与废弃内容边界 |

## 初始化步骤

1. 确认唯一权威入口: README、docs/INDEX、MASTER_PROGRESS 或项目约定文件。
2. 确认文档状态: current、draft、archive、raw、reference-assets 分层。
3. 确认生成物边界: 输出、缓存、实验结果、论文编译产物是否入库。
4. 确认验证方式: 链接检查、格式检查、脚本 smoke、渲染/编译检查。
5. 确认知识沉淀规则: 新经验写入项目 docs、skill、runbook 或记忆索引。

## 文档治理红线

- 不保留多个互相竞争的“最新版”。
- 历史事实保留在 archive/raw/reference-assets，不为当前口径随意改写。
- 当前执行路径、标准源、脚本命令必须指向当前真实位置。
- 生成产物不得冒充源文档。

## 常见证据

- `git status --short --branch`
- `rg -n "<旧名>|<旧路径>|<旧命令>" docs AGENTS.md CLAUDE.md README.md`
- `git diff --check`
- 项目自带渲染、构建或链接检查命令
