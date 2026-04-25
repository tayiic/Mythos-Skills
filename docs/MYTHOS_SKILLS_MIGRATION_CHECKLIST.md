# Mythos-Skills Migration Checklist

> 从 WorkflowTemplate 迁移到独立 GitHub 仓库的完整检查清单。
> 每完成一项打 ✅。

---

## Phase 1: 仓库初始化

- [ ] 在 GitHub 创建新仓库 `Mythos-Skills` (Public, MIT License)
- [ ] 克隆到本地
- [ ] 复制 `LICENSE` (MIT) 到根目录
- [ ] 创建 `.gitignore` (Node/Python/IDE 通用)
- [ ] 创建 `DISCLAIMER.md` (免责声明)
- [ ] 创建 `THIRD_PARTY_LICENSES.md` (第三方许可证)

## Phase 2: 核心方法论

- [ ] 复制 `SKILL_AUTHORING_PRINCIPLES.md` → `principles/SKILL_AUTHORING_PRINCIPLES.md`
  - [ ] 更新内部链接为相对路径
  - [ ] 确认无 WorkflowTemplate 特有引用
- [ ] 验证原则文档完整性 (8 条原则 + 权威来源 + 模板)

## Phase 3: 创建引擎

- [ ] 复制 `skill-creator/SKILL.md` → `engine/skill-creator/SKILL.md`
- [ ] 复制 `skill-creator/references/` → `engine/skill-creator/references/`
  - [ ] `creation_workflow.md`
  - [ ] `principles_checklist.md`
- [ ] 复制 `skill-creator/operations.json` → `engine/skill-creator/operations.json`
- [ ] 验证 skill-creator 三层结构完整
- [ ] 验证零跨目录引用
- [ ] 验证 SKILL.md ≤ 55 行

## Phase 4: 示例 Skills

### implement-standard
- [ ] 复制整个目录 → `skills/implement-standard/`
- [ ] 验证 SKILL.md + references/ + operations.json 完整
- [ ] 验证 operations.json 引用路径正确 (`references/tdd_iron_law.md`)
- [ ] 验证 SKILL.md 文档索引指向本地文件

### fs-defensive-fix
- [ ] 复制整个目录 → `skills/fs-defensive-fix/`
- [ ] 验证已包含本地 `references/command_discipline.md` (非跨目录)
- [ ] 验证 operations.json 引用路径正确
- [ ] 验证 SKILL.md 无 `implement-standard/references/` 引用

### orchestrator
- [ ] 复制整个目录 → `skills/orchestrator/`
- [ ] 验证 operations.json 包含 governance_profiles
- [ ] 验证 SKILL.md 文档索引指向本地 references/

## Phase 5: 安全体系

- [ ] 复制 `AGENTS.md` → `security/AGENTS.md`
  - [ ] 提取 Command Discipline 区块 (L0 约束)
  - [ ] 移除 WorkflowTemplate 特有规则
- [ ] 复制 `_gen_default2.ps1` → `security/_gen_default2.ps1`
- [ ] 复制 `default2.rules` → `security/default2.rules`
- [ ] 复制 `codex_rules_setup_guide.md` → `docs/codex_rules_setup_guide.md`

## Phase 6: Gallery (优化画廊)

### 基础设施
- [ ] 创建 `gallery/README.md` (画廊说明 + 优化标准)
- [ ] 创建 `gallery/from-superpowers/LICENSE` (MIT 副本)

### 第一个优化 Skill: TDD
- [ ] 从 superpowers 获取原始 test-driven-development SKILL.md
- [ ] 保存为 `gallery/from-superpowers/tdd-optimized/ORIGINAL.md`
- [ ] 应用 P1-P8 重构，产出 `SKILL.md` (≤55行)
- [ ] 创建 `DIFF.md` (优化清单 + token 节省数据)
- [ ] 创建 `references/` 和 `operations.json`
- [ ] 验证通过 P1-P8 全量校验

### 第二个优化 Skill: Systematic Debugging
- [ ] 同上流程

## Phase 7: README 与文档

- [ ] 编写 `README.md` (使用蓝图中的骨架)
  - [ ] 添加 badges (License / Stars / Forks / Principles)
  - [ ] 免责声明区块
  - [ ] 8 Principles 表格
  - [ ] Quick Start 代码块
  - [ ] 目录结构图
  - [ Works With 徽章
  - [ Credits 列表
- [ ] 复制本蓝图文档 → `docs/PROJECT_BLUEPRINT.md`
- [ ] 创建本文档 → `docs/MIGRATION_CHECKLIST.md`

## Phase 8: 最终验证

### 结构验证
- [ ] 目录结构与蓝图一致
- [ ] 每个 SKILL.md ≤ 55 行
- [ ] 每个 Skill 有 operations.json
- [ ] 零跨目录引用 (grep `\.\./` 或 `<other-skill>/`)
- [ ] 所有 references/ 内的 md 文件可独立阅读

### 内容验证
- [ ] 8 条原则文档完整
- [ ] skill-creator 包含 P1-P8 质量门禁
- [ ] gallery 中每个 Skill 有 ORIGINAL.md + DIFF.md
- [ ] THIRD_PARTY_LICENSES.md 包含所有来源
- [ ] DISCLAIMER.md 存在且内容完整

### 法律验证
- [ ] MIT License 文件存在
- [ ] gallery 中每个来源有 LICENSE 副本
- [ ] README 有 non-affiliated 免责声明
- [ ] 无移除的版权声明

### Git 验证
- [ ] `.gitignore` 配置合理
- [ ] 初始 commit 包含所有必要文件
- [ ] 推送到 GitHub

---

## 快速命令参考

```powershell
# 验证 SKILL.md 行数
Get-ChildItem -Recurse -Filter "SKILL.md" | ForEach-Object { $lines = (Get-Content $_.FullName).Count; if ($lines -gt 55) { "$($_.FullName): $lines lines ⚠️" } }

# 验证跨目录引用
Get-ChildItem -Recurse -Filter "SKILL.md" | ForEach-Object { $content = Get-Content $_.FullName -Raw; if ($content -match '\.\./|<skill>-\w+/references') { "$_: CROSS-REF FOUND ⚠️" } }

# 验证三层结构完整性
Get-ChildItem -Directory -Recurse | Where-Object { $_.Name -eq "skills" -or $_.Name -match "^skill-" } | ForEach-Object { $hasSkill = Test-Path "$($_.FullName)/SKILL.md"; $hasOps = Test-Path "$($_.FullName)/operations.json"; $hasRef = Test-Path "$($_.FullName)/references"; "$($_.Name): SKILL=$hasSkill OPS=$hasOps REF=$hasRef" }
```
