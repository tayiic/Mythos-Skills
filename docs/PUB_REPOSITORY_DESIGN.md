# Pub Repository Design

> 本文档是 `pub/` 对外开源仓库的设计方案。后续 README 策略、发布策略、增长策略、gallery 展示方案都优先同步到根目录 `docs/`，不再要求同步到 `pub/docs/`。

## 1. 仓库边界

`pub/` 是独立开源仓库，维护自己的 `.git/`，远程目标：

```text
git@github.com:tayiic/Mythos-Skills.git
```

根目录仓库只做本地保存，用于规划、调研、迁移、版本设计和内部文档沉淀。`pub/` 只承载对外发布内容。

## 2. 对外定位

Mythos-Skills 不是普通的 skill collection，而是 AI Agent Skill Engineering 的方法论仓库。

核心口号：

```text
Skills are not prompt files. They are reusable engineering units.
```

中文表达：

```text
Skill 不是提示词文件，而是可复用的工程单元。
```

项目要站在比普通 skill 仓库更高一层的位置：

- 普通仓库回答：有哪些 skill 可以复制？
- Mythos-Skills 回答：什么样的 skill 值得复制？
- 普通仓库展示：数量、列表、安装方式。
- Mythos-Skills 展示：原则、引擎、对比证据、优化收益。

## 3. 当前 pub 骨架

```text
pub/
|-- README.md                         # 英文主入口
|-- README.zh-CN.md                   # 中文入口
|-- LICENSE                           # MIT
|-- DISCLAIMER.md                     # 非官方/非关联免责声明
|-- THIRD_PARTY_LICENSES.md           # 第三方许可汇总
|-- CONTRIBUTING.md                   # 贡献指南
|-- SECURITY.md                       # 安全策略
|-- CODE_OF_CONDUCT.md                # 行为准则
|-- CHANGELOG.md                      # 变更记录
|-- ROADMAP.md                        # 路线图
|-- principles/
|   `-- SKILL_AUTHORING_PRINCIPLES.md # P1-P8 原则
|-- engine/
|   `-- skill-creator/                # 原则驱动的创建引擎
|-- skills/                           # 原创生产级示例
|-- gallery/                          # before/after 优化画廊
|-- security/                         # 命令安全体系
`-- .github/                          # Issue/PR 模板
```

## 4. README 首屏策略

作者不是名人时，不要把增长押在个人背书上，而要押在可验证冲击力上。

首屏必须同时完成四件事：

1. 说明这是一个新层级：从 prompt/tool 进入 skill engineering。
2. 说明痛点足够大：大量 skill 仓库存在膨胀、误触发、不可迁移、无反模式、无状态治理等问题。
3. 说明方法足够硬：P1-P8 + skill-creator + 三层架构。
4. 说明效果可验证：知名 skill 的 before/after 对比。

推荐首屏结构：

```text
# Mythos-Skills
> Skill engineering for AI agents.

I audited hundreds of AI agent skill repositories.
Most skills are still long prompts.
Mythos-Skills turns them into reusable engineering units.

[Before/After Gallery] [8 Principles] [Use skill-creator]
```

## 5. Star 增长策略

### 5.1 不靠名人，靠证据

非名人项目最需要降低信任成本。用户点 star 的理由通常不是“我完全读完了”，而是：

- 这个项目一句话就让我知道它解决什么问题。
- 它抓住了一个正在变大的趋势。
- 它有可复用的框架，而不是一堆零散内容。
- 它展示了真实案例，不只是宣称。
- 我以后可能会用到，先收藏。

所以 Mythos-Skills 的 README 不能只说“我调研了很多仓库”，还要立刻展示：

```text
Famous skill -> Mythos optimized skill -> measurable improvement
```

### 5.2 最值得大力宣传的优点

优先级从高到低：

1. **Before/After 证据**：最有名的 skill 经过 P1-P8 优化后，激活 token、触发准确性、可迁移性、反模式覆盖有什么提升。
2. **skill-creator 引擎**：不是只给原则，而是能让 Agent 按原则创建 skill。
3. **P1-P8 方法论**：把零散经验升维为清晰规则。
4. **三层结构**：`SKILL.md` + `references/` + `operations.json`，能解释为什么更稳定。
5. **跨 Agent**：Claude Code、Codex、Cursor、OpenCode、Gemini CLI 等都能理解。

### 5.3 Gallery 应该成为首页核心

建议把 gallery 从“后续补充”改为首屏后的第一核心卖点。尤其要挑最有名、最容易理解的 skill 做对比：

| 来源 | 候选 skill | 为什么适合首批优化 |
|---|---|---|
| Superpowers | TDD / systematic debugging / planning | 方法论强、认知度高、容易展示结构化收益 |
| Anthropic skills | 官方示例类 skill | 权威来源，适合展示兼容官方风格 |
| Awesome Agent Skills 中的热门技能 | 浏览器、文档、测试、部署类 | 用户容易理解收益 |

不要一开始铺 20 个。先做 3 个精品案例，每个案例要有图文对比。

### 5.4 图文比较格式

每个优化案例建议包含：

```text
Before
- SKILL.md: 180 lines
- Hidden dependency: yes
- Trigger: vague
- Gotchas: missing
- State: conversation only

After
- SKILL.md: 42 lines
- Hidden dependency: no
- Trigger: explicit
- Gotchas: documented
- State: file-backed
```

README 首页可放汇总表：

| Skill | Before | After | Improvement |
|---|---:|---:|---:|
| TDD workflow | 180-line activation | 42-line activation | 76% less activation context |
| Debugging workflow | Cross-skill references | Self-contained package | Portable |
| Planning workflow | Generic description | Trigger-first description | Better activation |

每个 gallery 子目录再放 `DIFF.md`，写清楚：

- 哪些内容被移到 `references/`。
- 哪些跨目录依赖被消除。
- 哪些 trigger 被重写。
- 哪些 gotchas 被补充。
- 哪些脚本或 operations 被结构化。

### 5.5 建议加一张视觉图

README 可以放一张 `docs/assets/mythos-before-after.png` 或 `gallery/assets/before-after.png`：

```text
Long Prompt Skill
      |
      v
P1-P8 + skill-creator
      |
      v
Production Skill Unit
```

图的目的不是装饰，而是让用户在 3 秒内理解项目层级。

## 6. 多语言策略

README 采用英文主入口，因为 GitHub 传播更广；同时必须提供中文入口：

```text
README.md
README.zh-CN.md
```

英文 README 顶部加语言切换：

```text
Languages: English | 简体中文
```

中文 README 不要逐字翻译，要强化中文用户更关心的点：

- 为什么 skill 会失控。
- P1-P8 如何约束 Agent。
- 这个仓库怎么帮你写自己的 skill。
- gallery 如何证明优化效果。

## 7. 发布顺序

建议下一阶段按这个顺序做：

1. 完整迁移 P1-P8 原则文档。
2. 完整迁移并打磨 `skill-creator`。
3. 做 1 个知名 skill 的真实 before/after 优化。
4. 给该案例补 `ORIGINAL.md`、`DIFF.md`、截图或 Mermaid 图。
5. 把 README 首屏改成“方法论 + 证据”。
6. 再做第 2、3 个优化案例。
7. 发帖推广时主标题围绕调研和证据，而不是项目名。

推荐首发标题：

```text
I audited hundreds of AI agent skills. Most fail for the same 8 reasons.
```

中文首发标题：

```text
我调研了上百个 AI Agent Skill 仓库，发现坏 skill 基本都死在这 8 个问题上
```

## 8. 风险控制

- 不要夸大未验证数字，例如 token 节省必须来自实际行数/估算方法。
- 不要宣称与任何官方模型或公司有关联。
- 第三方 skill 必须保留许可证和版权声明。
- 优化案例必须展示原始版本、改动说明和原则映射。

## 9. 当前结论

需要大力突出项目优点，但重点不是抽象宣传，而是把优势变成证据：

```text
P1-P8 says what good means.
skill-creator makes it repeatable.
gallery proves it works.
```

中文：

```text
P1-P8 定义好 skill。
skill-creator 让好 skill 可重复生产。
gallery 证明优化真的有效。
```
