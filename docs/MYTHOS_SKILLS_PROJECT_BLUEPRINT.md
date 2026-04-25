# Mythos-Skills Project Blueprint

> **项目代号**: Mythos-Skills
> **状态**: 规划中 (待迁移至独立 GitHub 仓库)
> **创建日期**: 2026-04-25
> **License**: MIT
> **目标**: 成为 AI Agent Skill 编写领域的权威方法论仓库

---

## 一、为什么做这个项目

### 1.1 市场痛点

AI Coding Agent 的 Skill 生态正在爆发式增长：

| 指标 | 数据 |
|------|------|
| OpenClaw 注册 Skills | **5,400+** |
| Claude Code 社区 Skills | 数千个 |
| superpowers Stars | 160k (6个月) |
| everything-claude-code Stars | 166k (10个月) |

**但质量参差不齐，核心问题：**

```
❌ SKILL.md 膨胀到 200+ 行 → 上下文窗口污染，每次激活浪费 token
❌ 跨目录依赖 → 复制 skill 后缺少引用，无法独立运行
❌ description 写"做什么"而非"何时用" → AI 无法正确触发
❌ 无反模式/踩坑点 → AI 反复犯同样的错误
❌ 状态存在上下文而非文件 → 对话轮次 > 10 后丢失状态
❌ 让 AI 构造样板代码而非提供脚本 → 浪费 token + 不确定性高
```

**5,400+ skills 存在，但没有人系统性地回答：如何写好一个 Skill？**

### 1.2 我们的优势

我们不是从零开始。在 WorkflowTemplate 项目中已经沉淀了：

| 资产 | 状态 | 来源 |
|------|------|------|
| **8 条核心原则 (P1-P8)** | ✅ 已提炼完成 | Anthropic 官方指南 + Karpathy 上下文工程 + 生产实践 |
| **skill-creator (原则驱动创建引擎)** | ✅ 已重构为 V4.0 | 三层架构 + P1-P8 强制校验 |
| **3 个生产级示例 Skill** | ✅ 已优化为自包含 | implement-standard / fs-defensive-fix / orchestrator |
| **命令安全三层防御 (L0/L1/L2)** | ✅ 已落地 | AGENTS.md + prefix_rules + Skill 约束 |
| **三层架构规范** | ✅ 已验证 | SKILL.md (≤55行) + references/ + operations.json |

### 1.3 定位对标

```
superpowers     = "让 AI 编码更规范"          → 160k ⭐ (卖的是编码方法论)
Mythos-Skills   = "让 Skill 编写更工程化"      → ?    ⭐ (卖的是 Skill 编写方法论)

superpowers 教 AI 如何写出符合 TDD 的代码
Mythos-Skills  教人类/AI 如何写出符合 P1-P8 的 Skill
```

---

## 二、命名决策记录

### 2.1 最终决定: `Mythos-Skills`

| 维度 | 决定 | 理由 |
|------|------|------|
| **名称** | `Mythos-Skills` | 借 Anthropic Mythos 模型之势 + "技能的起源神话"语义 |
| **格式** | PascalCase (Mythos-Skills) | GitHub 框架项目标准风格 |
| **含义** | Skill 编写领域的根基性叙事/奥义 | Mythos = 神话/起源故事/深层哲学 |

### 2.2 备选方案及淘汰理由

#### 第一轮候选 (通用级)

| 名称 | 含义 | 优势 | 劣势 | 淘汰理由 |
|------|------|------|------|---------|
| **skillforge** | 锻造 | 简短有力、forge 隐喻精准 | 宏观大气感不足 | 作为备选 #1 |
| **skill-engine** | 引擎 | 直观、engine 有力量感 | 🔴 同名项目 5+ 个，搜索被淹没 | ❌ 淘汰 |
| **skillcraft** | 匠艺 | craft = 工匠精神 | 稍长、记忆度一般 | 备选 #2 |
| **ironskill** | 铁律 | iron = 铁律、辨识度高 | 可能暗示"死板" | 备选 #3 |

#### 第二轮候选 (宏观大气级)

| 名称 | 含义 | 优势 | 劣势 | 淘汰理由 |
|------|------|------|------|---------|
| **skillarkana** | 奥秘/奥义 | 极高独特性、无同名、发音极佳 | 借势能力弱 | 🥈 备选 (最安全的原创方案) |
| **skillgenesis** | 创世纪 | 终极起源概念、与 superpowers 叙事对仗 | 稍长(12字母)、genesis 太常见 | 备选 |
| **skillolympus** | 万神殿 | 希腊神话、最高殿堂意象 | 太长(13字母)、可能误认为游戏 | 备选 |
| **skillsovereign** | 至高主权 | 主权感强 | 中等记忆度、有少量无关同名 | 备选 |
| **skillaether** | 以太(第五元素) | 极高格调、无同名 | 过于抽象、不易理解 | 备选 |

#### 第三轮候选 (借势级 — 最终胜出方向)

| 名称 | 格式分析 | SEO 权重 | 首因效应 | 法律风险 | 推荐度 |
|------|---------|---------|---------|---------|--------|
| **Mythos-Skills** | 被借势词在前 | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | 🟡 中 (需免责) | **🏆 胜出** |
| **Skills-Mythos** | 核心词在前 | ⭐⭐⭐ | ⭐⭐⭐ | 🟢 低 | 🥈 备选 |
| **Skill-Mythos** | 单数核心词 | ⭐⭐⭐ | ⭐⭐⭐ | 🟢 低 | 🥉 备选 |

### 2.3 为什么选 Mythos-Skills (最终决策依据)

```
决策权重:

SEO 与流量      ████████████████████  40%  ← GitHub 搜索前缀匹配 > 包含匹配
首因效应        ██████████████████    30%  ← 第一个词决定整体印象框架
社区传播力      ██████████████        20%  ← "I learned the Mythos of Skills"
法律风险控制    ██████████            10%  ← 可通过免责声明缓解
```

**关键论据:**

1. **GitHub 成功借势先例**: everything-claude-code (166k), awesome-claude-skills (55k), andrej-karpathy-skills (62k) — 全部是"被借势词在前"
2. **搜索算法偏好**: 标题以 "Mythos" 开头 → 任何搜 "mythos" 的查询都优先命中
3. **心理首因效应**: 用户第一眼看到 "Mythos" → 框架 = "这是前沿/高端生态的一部分"
4. **双关语义**: 既借势 Anthropic 最强模型名，又用 Mythos 原意("起源神话")表达"Skill 编写的根基性哲学"

### 2.4 Mythos 是什么 (背景知识)

| 属性 | 详情 |
|------|------|
| 全称 | Claude Mythos Preview |
| 出品方 | Anthropic |
| 定位 | Anthropic 迄今最强模型 |
| 能力 | SWE-bench Verified 93.9%, 自主工程, 长程推理突破 |
| 发布时间 | 2026 年 4 月 |
| 状态 | 未公开发布，仅限受限访问 |
| 希腊语原意 | μῦθος = 神话、叙事、起源故事、深层哲学 |

**本项目借用 "Mythos" 的哲学原意，而非宣称与 Anthropic 模型有关联。**

---

## 三、市场调研数据

### 3.1 Tier 1: 10万+ Stars (现象级)

| 仓库 | Stars | 类型 | 定位关键词 | 启示 |
|------|-------|------|-----------|------|
| **everything-claude-code** | 166k | 博 | Agent harness 性能优化全栈系统 | "数量即正义": 183 skills + 48 agents |
| **superpowers** | 160k | 精 | Agentic skills framework + 方法论 | **"方法论 > 工具"**: 14 skills 但卖的是 TDD 哲学 |
| **system-prompts-and-models-of-ai-tools** | 135k | 博 | AI 工具系统提示词泄露合集 | 信息聚合价值巨大 |
| **anthropics/skills** | 120k | 精 | Anthropic 官方 Skills | 官方背书 = 天然信任 |

### 3.2 Tier 2: 5万+ Stars (头部)

| 仓库 | Stars | 类型 | 定位关键词 | 启示 |
|------|-------|------|-----------|------|
| **andrej-karpathy-skills** | 62k | 极精 | Karpathy 思想提炼为 1 个文件 | **名人效应 + 极简 = 爆发** |
| **awesome-claude-skills** | 55k | 博 | Skills 精选列表 | Awesome list 模式门槛低 |
| **awesome-openclaw-skills** | 47k | 博 | OpenClaw 5400+ skills 大全 | Registry 模式有规模效应 |
| **awesome-claude-code** | 39k | 博 | Claude Code 生态精选 | 生态聚合有价值 |
| **graphify** | 30k | 极精 | 知识图谱 skill (单 skill) | **单一极致功能也能爆** |

### 3.3 高 star 仓库的共同成功因子

```
因子 1: 解决真实痛点 (不是玩具)
       superpowers → AI 写的代码不靠谱 → 强制 TDD 流程
       ECC         → Claude Code 只用到 30% → 183 skills 解锁全部

因子 2: 数字制造冲击力
       "14 skills" / "183 skills" / "5400+ skills" / "160k stars"

因子 3: 方法论 > 功能列表
       superpowers 卖的不是 skills，而是"如何让 AI 规范编码"

因子 4: 快速上手 < 30 秒
       一个 install 命令 / 一个 copy 操作 / 一个 prompt

因子 5: 跨平台兼容
       明确支持 Claude Code · Codex · Cursor · OpenCode

因子 6: 持续更新
       每周/每月有新内容，保持 Trending 曝光
```

### 3.4 我们的差异化空间

| 已有市场空白 | 我们的答案 |
|-------------|-----------|
| 无人系统化回答"如何写好 Skill" | 8 条核心原则 (P1-P8) |
| 无原则驱动的 Skill 创建工具 | skill-creator (P1-P8 强制校验) |
| 无 Skill 优化的 before/after 对比 | gallery/ 优化画廊 |
| 无命令安全的三层防御体系 | L0/L1/L2 命令约束 |
| 无生产级 FSM + Profile 治理 | orchestrator + profile_routes |

---

## 四、项目架构

### 4.1 目录结构 (完整版)

```
Mythos-Skills/
│
├── README.md                          # 项目主页 (冲击力优先)
├── LICENSE                            # MIT License
├── .gitignore                         # Git 忽略规则
│
├── DISCLAIMER.md                      # ⚠️ 免责声明 (非官方/非关联)
├── THIRD_PARTY_LICENSES.md            # 第三方许可证汇总
│
├── principles/                        # ═══ 核心方法论 ═══
│   └── SKILL_AUTHORING_PRINCIPLES.md  # 8 条核心原则完整文档
│
├── engine/                            # ═══ 创建引擎 ═══
│   └── skill-creator/
│       ├── SKILL.md                  # 入口 (≤55行)
│       ├── references/
│       │   ├── creation_workflow.md  # 四阶段创建流程
│       │   └── principles_checklist.md # P1-P8 校验清单
│       └── operations.json           # 命令索引
│
├── skills/                            # ═══ 原创示例 Skill ═══
│   │   (展示 P1-P8 原则如何落地)
│   │
│   ├── implement-standard/
│   │   ├── SKILL.md                  # TDD Iron Law 实现
│   │   ├── references/
│   │   │   ├── tdd_iron_law.md
│   │   │   └── command_discipline.md
│   │   └── operations.json
│   │
│   ├── fs-defensive-fix/
│   │   ├── SKILL.md                  # 根因优先 Iron Law
│   │   ├── references/
│   │   │   ├── root_cause_iron_law.md
│   │   │   └── command_discipline.md
│   │   └── operations.json
│   │
│   └── orchestrator/
│       ├── SKILL.md                  # Profile 路由 + FSM 调度
│       ├── references/
│       │   └── profile_routing.md
│       └── operations.json
│
├── gallery/                           # ═══ 优化共享画廊 ═══
│   │   (基于 MIT/Apache-2.0 社区 Skill 的 P1-P8 重构版本)
│   │
│   ├── README.md                     # 画廊说明 + 优化标准
│   │
│   ├── from-superpowers/             # 来源: obra/superpowers (MIT)
│   │   ├── LICENSE                   # 原始 MIT 许可证副本
│   │   │
│   │   ├── tdd-optimized/
│   │   │   ├── SKILL.md              # P1-P8 重构后 (≤55行)
│   │   │   ├── ORIGINAL.md           # 原始版本 (对比基准)
│   │   │   ├── DIFF.md              # 优化清单 + 对应原则
│   │   │   ├── references/
│   │   │   └── operations.json
│   │   │
│   │   └── systematic-debugging-optimized/
│   │       └── ...
│   │
│   ├── from-anthropics/             # 来源: anthropics/skills (Apache-2.0)
│   │   ├── LICENSE                   # 原始 Apache-2.0 许可证副本
│   │   └── (待填充)
│   │
│   └── from-community/              # 来源: 其他社区项目
│       ├── THIRD_PARTY_NOTICE.md     # 该目录下的第三方许可汇总
│       └── (待填充)
│
├── security/                          # ═══ 命令安全体系 ═══
│   ├── AGENTS.md                     # L0: 行为约束 (~20行)
│   ├── _gen_default2.ps1             # L1: 规则生成器
│   └── default2.rules               # L1: 生成产物 (~400条规则)
│
└── docs/                             # ═══ 详细文档 ═══
    ├── codex_rules_setup_guide.md    # 可迁移的安全规则配置指南
    ├── PROJECT_BLUEPRINT.md          # 本文档 (项目蓝图)
    └── MIGRATION_CHECKLIST.md        # 从 WorkflowTemplate 迁移检查清单
```

### 4.2 各模块职责

| 模块 | 内容 | 目标用户 | 核心价值 |
|------|------|---------|---------|
| **principles/** | P1-P8 8条原则 | 所有人 | "为什么" — 底层哲学 |
| **engine/** | skill-creator | Skill 作者 | "怎么创建" — 自动化工具 |
| **skills/** | 3个原创示例 | 学习者/参考者 | "长什么样" — 最佳实践 |
| **gallery/** | 优化共享 | 社区贡献者 | "对比效果" — before/after |
| **security/** | L0/L1/L2 | 安全敏感用户 | "安全底线" — 命令防御 |
| **docs/** | 深度文档 | 进阶用户 | "怎么做" — 操作指南 |

---

## 五、内容规格

### 5.1 8 条核心原则 (P1-P8)

```
P1 简洁即正义      → 上下文窗口是公共资源
P2 渐进式披露      → 按需加载，不预加载
P3 自包含独立      → 每个 Skill 是可独立复用的原子单元
P4 自由度匹配      → 脆弱操作低自由，开放任务高自由
P5 触发优于描述    → description 写"何时用"而非"做什么"
P6 踩坑点即金矿    → 反复失败的模式比正面指南更有价值
P7 脚本优于指令    → 给 AI 代码，让它编排而非构造
P8 记忆外置        → 状态存文件，不存上下文
```

每条原则包含:
- 权威来源 (Anthropic / Karpathy / Claude Code Guide / DataCamp / Phil Schmid / 宝玉)
- 核心规则 (具体可执行的标准)
- 正反例对比
- 违规后果

### 5.2 三层架构规范

```
Layer 1: SKILL.md        → ~55行, 唯一入口
Layer 2: references/*.md  → 按需加载的详细文档
Layer 3: operations.json  → 机器可读命令索引
```

### 5.3 gallery/ 优化标准

每个 gallery 中的 Skill 必须:
1. 保留原始版权声明和许可证
2. 提供 ORIGINAL.md (原始版本)
3. 提供 DIFF.md (优化清单 + 对应哪条原则 + token 节省数据)
4. 通过 P1-P8 全量校验
5. SKILL.md ≤ 55 行

DIFF.md 模板:
```markdown
# Optimization Diff: <skill-name>

Source: [<original-repo-url>](url)
License: <original-license> © <original-author>
Optimized by: Mythos-Skills P1-P8 Principles

## Changes

| # | Original | Optimized | Principle |
|---|----------|-----------|-----------|
| 1 | <before> | <after> | **Px <name>** |

## Token Savings

| Metric | Original | Optimized | Saving |
|--------|----------|-----------|--------|
| Activation tokens | ~Xk | ~Yk | **Z%** |
```

---

## 六、法律风险与注意事项

### 6.1 许可证合规

| 来源仓库 | 许可证 | 能否修改再发布? | 要求 |
|----------|--------|----------------|------|
| superpowers (obra) | **MIT** | ✅ 可以 | 保留版权声明 + 许可证文本 |
| anthropics/skills | **Apache-2.0** | ✅ 可以 | 保留声明 + 标注修改 + 保留 NOTICE |
| everything-claude-code | **MIT** | ✅ 可以 | 保留版权声明 + 许可证文本 |
| karpathy-skills | **MIT** | ✅ 可以 | 保留版权声明 + 许可证文本 |
| vercel-labs/agent-skills | **MIT** | ✅ 可以 | 保留版权声明 + 许可证文本 |

**结论: 主流 Skill 仓库均为 MIT 或 Apache-2.0，法律上完全可以修改再发布。**

### 6.2 Mythos 商标风险

| 风险 | 严重度 | 应对措施 |
|------|--------|---------|
| 被误认为官方/半官方 | 🔴 高 | README 顶部 + DISCLAIMER.md 明确标注 non-affiliated |
| Anthropic 商标维权 | 🟡 中 | 使用时强调哲学原意 ("foundational mythology") 而非模型关联 |
| 社区"碰瓷"指控 | 🟡 中 | 语气定位为"致敬/启发"而非"关联"，保持谦逊 |

### 6.3 免责声明模板 (DISCLAIMER.md)

```markdown
# Disclaimer

## Affiliation

**Mythos-Skills is NOT affiliated with, endorsed by, or connected to Anthropic.**

"Mythos" is used in its original Greek meaning (μῦθος) — referring to a 
foundational narrative, origin story, or body of principles. This project is 
about the foundational mythology/principles of **AI agent skill engineering**, 
not about any specific AI model or product.

## Third-Party Content

This repository may contain optimized versions of skills from third-party 
sources. All third-party content retains its original license and copyright 
notices. See [THIRD_PARTY_LICENSES.md](THIRD_PARTY_LICENSES.md) for details.

## Use at Your Own Risk

This project is provided for educational and reference purposes. Users are 
responsible for reviewing and testing all content before use in production 
environments.
```

### 6.4 THIRD_PARTY_LICENSES.md 模板

```markdown
# Third-Party Licenses

This repository aggregates or derives content from the following sources.
Each source retains its original license.

## Active Sources

| Source Repository | URL | License | Copyright |
|------------------|-----|---------|-----------|
| superpowers | https://github.com/obra/superpowers | MIT | © Jesse Vincent |
| anthropics/skills | https://github.com/anthropics/skills | Apache-2.0 | © Anthropic |
| ... | ... | ... | ... |

## Full License Text

See each source's LICENSE file in the respective gallery subdirectory.
```

---

## 七、README 设计 (骨架)

```markdown
# ⚡ Mythos-Skills

> The foundational mythology of AI agent skill engineering. 
> **8 iron principles. Principle-driven creation engine. Optimized community gallery.**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Stars](https://img.shields.io/github/stars/yourname/Mythos-Skills.svg)](https://github.com/yourname/Mythos-Skills/stargazers)
[![Forks](https://img.shields.io/github/forks/yourname/Mythos-Skills.svg)](https://github.com/yourname/Mythos-Skills/network/members)
[![Principles](https://img.shields.io/badge/Principles-8%20Iron%20Rules-blue.svg)](principles/SKILL_AUTHORING_PRINCIPLES.md)

---

## ⚠️ Disclaimer

**Not affiliated with Anthropic.** "Mythos" refers to the foundational mythology 
of skill engineering — the deep principles that separate production-grade skills 
from broken ones. Inspired by the frontier. Built for every agent.

[Full disclaimer →](DISCLAIMER.md)

---

## Why Mythos-Skills?

**5,400+ OpenClaw skills exist. Most are broken.**

- SKILL.md bloated to 200+ lines → context window pollution
- Cross-directory dependencies → copy-paste breaks everything
- Description says "what" not "when" → AI can't trigger correctly
- No anti-patterns → AI repeats the same mistakes forever
- State in context, not files → lost after 10 conversation turns

**Mythos-Skills fixes this with 8 iron principles.**

## The 8 Principles (The Arkana)

| # | Principle | One-Liner | Detail |
|---|-----------|-----------|--------|
| P1 | Concise is Key | Context window is a public good | [→](principles/SKILL_AUTHORING_PRINCIPLES.md#p1) |
| P2 | Progressive Disclosure | Load on demand, never preload | [→](principles/SKILL_AUTHORING_PRINCIPLES.md#p2) |
| P3 | Self-Contained | Each skill is an independent atom | [→](principles/SKILL_AUTHORING_PRINCIPLES.md#p3) |
| P4 | Match Freedom | Fragile ops = low freedom; creative = high | [→](principles/SKILL_AUTHORING_PRINCIPLES.md#p4) |
| P5 | Trigger > Description | Write "when to use", not "what it does" | [→](principles/SKILL_AUTHORING_PRINCIPLES.md#p5) |
| P6 | Gotchas are Gold | Failure patterns > success guides | [→](principles/SKILL_AUTHORING_PRINCIPLES.md#p6) |
| P7 | Code over Instructions | Give AI scripts, let it orchestrate | [→](principles/SKILL_AUTHORING_PRINCIPLES.md#p7) |
| P8 | Externalize Memory | State in files, not in context | [→](principles/SKILL_AUTHORING_PRINCIPLES.md#p8) |

## Quick Start (30 seconds)

```bash
# Clone
git clone https://github.com/yourname/Mythos-Skills.git
cd Mythos-Skills

# Use the principle-driven skill creator
cp -r engine/skill-creator/ .trae/skills/skill-creator/

# Tell your AI: "Use skill-creator to create a new skill"
# It will guide you through P1-P8 validation automatically
```

## What You Get

```
Mythos-Skills/
├── principles/          # 8 iron principles (authoritative sources)
├── engine/              # Principle-driven creation engine (skill-creator)
├── skills/              # 3 production-grade example skills
├── gallery/             # Optimized community skills (before/after)
├── security/            # 3-layer command defense (L0/L1/L2)
└── docs/                # Deep-dive guides & migration docs
```

## Gallery: See Before → After

Community skills optimized through P1-P8. Each with diff analysis.

| Original Source | Skill | Token Saving | Principles Applied |
|----------------|-------|-------------|-------------------|
| [superpowers](https://github.com/obra/superpowers) | TDD | -70% | P1, P2, P5, P6 |
| [superpowers](https://github.com/obra/superpowers) | Systematic Debugging | -65% | P1, P3, P6 |
| [anthropics/skills](https://github.com/anthropics/skills) | *(coming soon)* | -?% | ? |

[View full gallery →](gallery/README.md)

## Works With

Claude Code · Codex · Cursor · OpenCode · Gemini CLI · Any AI coding agent that supports skills

## Credits

Principles distilled from:
- **Anthropic** — Official Skill Authoring Guide
- **Andrej Karpathy** — Context Engineering
- **Thariq (Anthropic)** — Lessons from Building Claude Code
- **Claude Code Guide** — Progressive Disclosure patterns
- **DataCamp** — Production Best Practices
- **Phil Schmid / LangChain** — Context Engineering (SCOFI)
- **宝玉** — Coding Agent Sweet Spot

## Contributing

1. Fork
2. Add an optimized skill to `gallery/` (follow [gallery standards](gallery/README.md))
3. Submit PR with DIFF.md showing P1-P8 improvements

## License

[MIT](LICENSE) — Original content © 2026 YourName. Third-party content per original licenses.

---

**Star if you believe skills should be forged, not just written.** ⚡
```

---

## 八、增长策略

### 8.1 首发策略 (Week 1)

| 动作 | 平台 | 内容要点 |
|------|------|---------|
| Reddit r/ClaudeAI | 发帖 | "I audited 5,400 AI agent skills and found 8 principles that separate good from bad" |
| Hacker News | Show HN | 同上，技术深度版 |
| Twitter/X | Thread | "The Mythos of Skill Engineering — why most skills are broken" |
| GitHub Trending | 提交 | 确保 README 有足够视觉冲击力 |

### 8.2 持续增长 (Weekly)

| 动作 | 频率 | 内容 |
|------|------|------|
| 新增 gallery Skill | 每周 1-2 个 | 选择热门 repo 的 skill 做 P1-P8 优化 |
| 原则深度文章 | 双周 | 选一条原则写深度解析 (如 "Why P3 Self-Contained Matters") |
| Twitter/X thread | 每周 | "Skill of the Week" — 展示一个 before/after 对比 |

### 8.3 关键指标追踪

| 指标 | 目标 (Month 1) | 目标 (Month 3) | 目标 (Month 6) |
|------|---------------|---------------|---------------|
| Stars | 500 | 5,000 | 25,000 |
| Forks | 50 | 500 | 3,000 |
| gallery Skills 数量 | 5 | 20 | 50 |
| PR / Issue 活跃度 | 10 | 100 | 500 |

---

## 九、迁移检查清单

### 9.1 从 WorkflowTemplate 迁移的内容

| 文件 | 源路径 | 目标路径 | 状态 |
|------|--------|---------|------|
| 8 条原则文档 | `docs/guides/SKILL_AUTHORING_PRINCIPLES.md` | `principles/SKILL_AUTHORING_PRINCIPLES.md` | ⬜ 待复制 |
| skill-creator SKILL.md | `trae_standard_harness/skills/skill-creator/SKILL.md` | `engine/skill-creator/SKILL.md` | ⬜ 待复制 |
| skill-creator references | `trae_standard_harness/skills/skill-creator/references/` | `engine/skill-creator/references/` | ⬜ 待复制 |
| skill-creator operations.json | `trae_standard_harness/skills/skill-creator/operations.json` | `engine/skill-creator/operations.json` | ⬜ 待复制 |
| implement-standard | `trae_standard_harness/skills/implement-standard/` | `skills/implement-standard/` | ⬜ 待复制 |
| fs-defensive-fix | `trae_standard_harness/skills/fs-defensive-fix/` | `skills/fs-defensive-fix/` | ⬜ 待复制 |
| orchestrator | `trae_standard_harness/skills/orchestrator/` | `skills/orchestrator/` | ⬜ 待复制 |
| AGENTS.md (L0) | `AGENTS.md` | `security/AGENTS.md` | ⬜ 待复制 |
| _gen_default2.ps1 | `docs/codex_rules/_gen_default2.ps1` | `security/_gen_default2.ps1` | ⬜ 待复制 |
| default2.rules | `docs/codex_rules/default2.rules` | `security/default2.rules` | ⬜ 待复制 |
| Codex Rules Setup Guide | `docs/codex_rules/codex_rules_setup_guide.md` | `docs/codex_rules_setup_guide.md` | ⬜ 待复制 |

### 9.2 新建的内容

| 文件 | 说明 | 状态 |
|------|------|------|
| `README.md` | 项目主页 | ⬜ 待编写 |
| `LICENSE` | MIT License | ⬜ 待创建 |
| `DISCLAIMER.md` | 免责声明 | ⬜ 待创建 |
| `THIRD_PARTY_LICENSES.md` | 第三方许可证 | ⬜ 待创建 |
| `.gitignore` | Git 忽略规则 | ⬜ 待创建 |
| `gallery/README.md` | 画廊说明 | ⬜ 待编写 |
| `gallery/from-superpowers/LICENSE` | superpowers MIT 副本 | ⬜ 待创建 |
| `gallery/from-superpowers/tdd-optimized/` | 第一个优化 Skill | ⬜ 待创建 |
| `docs/PROJECT_BLUEPRINT.md` | 本文档 | ✅ 已创建 (本文件) |
| `docs/MIGRATION_CHECKLIST.md` | 迁移检查清单 | ⬜ 待创建 |

### 9.3 迁移注意事项

1. **去除内部引用**: 所有指向 WorkflowTemplate 内部路径的链接需要更新为相对路径
2. **去除 GLOBAL_SKILL_PROTOCOL.md 引用**: skill-creator 不再引用全局协议（已改为自包含）
3. **统一路径风格**: 所有 operations.json 中的 ref 路径使用相对路径 (`references/xxx.md`)
4. **版权清理**: 确认所有原创内容的版权归属
5. **测试验证**: 迁移后每个 Skill 的三层结构完整性检查

---

## 十、附录

### A. 权威来源链接表

| 来源 | 核心贡献 | 链接 |
|------|---------|------|
| Anthropic Official Skill Guide | P1, P4, P5, Skill 结构规范 | [Complete Guide to Building Skills for Claude](https://resources.anthropic.com/hubfs/The-Complete-Guide-to-Building-Skill-for-Claude.pdf) |
| Thariq (Anthropic Internal) | P6, P7, Skill 分类, 渐进式披露 | [Lessons from Building Claude Code](https://baoyu.io/translations/2026-03-17/claude-code-skills-lessons) |
| Andrej Karpathy | P2, Context Engineering | [Context Engineering (X/Twitter)](https://x.com/karpathy/status/) |
| Claude Code Guide | P2 量化, MINI 文件模式 | [Progressive Disclosure](https://ytrofr.github.io/claude-code-guide/docs/guide/15-progressive-disclosure.html) |
| DataCamp | 指令预算 150-200 条 | [Claude Code Best Practices](https://www.datacamp.com/tutorial/claude-code-best-practices) |
| Phil Schmid / LangChain | P8 记忆外置 (SCOFI) | [Context Engineering](https://huggingface.co/blog/philipp-schmid/context-engineering) |
| 宝玉 | Coding Agent 甜蜜点 | [Coding Agent Sweet Spot](https://baoyu.io/blog/2026-02-25/coding-agent-sweet-spot) |

### B. 竞品快速参考

| 仓库 | Stars | License | 我们的关系 |
|------|-------|---------|-----------|
| [obra/superpowers](https://github.com/obra/superpowers) | 160k | MIT | gallery 优化来源 + 竞品互补 |
| [affaan-m/everything-claude-code](https://github.com/affaan-m/everything-claude-code) | 166k | MIT | 不同赛道 (全栈 vs 方法论) |
| [anthropics/skills](https://github.com/anthropics/skills) | 120k | Apache-2.0 | gallery 优化来源 + 官方参考 |
| [forrestchang/andrej-karpathy-skills](https://github.com/forrestchang/andrej-karpathy-skills) | 62k | MIT | 思想来源之一 |
| [ComposioHQ/awesome-claude-skills](https://github.com/ComposioHQ/awesome-claude-skills) | 55k | MIT | 不同赛道 (列表 vs 方法论) |

### C. 版本历史

| 版本 | 日期 | 变更 |
|------|------|------|
| v0.1 | 2026-04-25 | 初始蓝图文档，包含完整规划 |
