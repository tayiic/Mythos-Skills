# Mythos-Skills

> 面向 AI Agent 的下一层能力：Skill Engineering。

语言：[English](README.md) | [简体中文](README.zh-CN.md) | [日本語](README.ja.md) | [한국어](README.ko.md) | [Español](README.es.md)

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Stars](https://img.shields.io/github/stars/tayiic/Mythos-Skills?style=social)](https://github.com/tayiic/Mythos-Skills/stargazers)
[![Forks](https://img.shields.io/github/forks/tayiic/Mythos-Skills?style=social)](https://github.com/tayiic/Mythos-Skills/forks)
[![Principles](https://img.shields.io/badge/Principles-8%20Iron%20Rules-blue.svg)](principles/SKILL_AUTHORING_PRINCIPLES.md)
[![Agent Skills](https://img.shields.io/badge/Agent%20Skills-Production%20Grade-black.svg)](skills)
[![Gallery](https://img.shields.io/badge/Gallery-Before%20to%20After-green.svg)](gallery)

我调研了上百个 AI agent skill 仓库，也看过大量已经注册或公开传播的 skills。一个很明显的问题是：生态正在爆发，但很多 skill 仍然只是长提示词、脆弱片段、个人笔记，离可复用的工程单元还有距离。

Mythos-Skills 的核心判断是：

**Skill 不是提示词文件，而是可复用的工程单元。**

这个仓库用 8 条铁律、原则驱动的 `skill-creator`、生产级示例和 before/after gallery，把 skill 编写从“凭感觉写提示词”提升到“可审查、可迁移、可复用的工程方法”。

它也覆盖了一组对 GitHub 搜索和用户认知都很重要的关键词：agent skills、Claude Code、Codex、Cursor、Gemini CLI、context engineering、prompt engineering、AI coding workflow。

## 先看证据

这个项目最重要的卖点不是口号，而是可验证优化。首批 gallery 会瞄准最有名、最容易被用户理解的 skills，把优化前后的数据直接摆出来。

| 著名 skill | 公开基线 | Mythos 目标 | 要证明的提升 |
|---|---:|---:|---|
| Anthropic `skill-creator` | 485 行 / 32.4 KB | <=55 行入口 | 激活上下文减少约 85-90% |
| Anthropic `claude-api` | 324 行 / 32.2 KB | <=55 行入口 | 激活上下文减少约 80-88% |
| Anthropic `xlsx` | 292 行 / 11.2 KB | <=55 行入口 | 激活上下文减少约 70-82% |
| Superpowers `systematic-debugging` | 长 workflow 文件 | <=55 行入口 | 更快触发，保留根因纪律 |
| Superpowers `test-driven-development` | 长 workflow 文件 | <=55 行入口 | 更快触发，保留 TDD 铁律 |

完整数据板见 [BENCHMARKS.md](BENCHMARKS.md)。每个案例都应该包含 `ORIGINAL.md`、优化后的 `SKILL.md`、`DIFF.md`、本地 `references/` 和 benchmark notes。gallery 是这个项目建立信任的地方。

## 更小不能更弱

减少 token 只是一个指标。用户同样会关心：优化后会不会更慢、能力会不会下降、AI 会不会理解偏。

在 Mythos 里，一个优化只有在下面几项都尽量保住或提升时，才算真的成功：

| 关注点 | 我们检查什么 |
|---|---|
| 速度 | 平均任务耗时、第一次做对动作的时间 |
| 能力 | Eval 通过率、任务完成质量 |
| 理解偏差 | 优化后的 trigger 是否仍然把 agent 路由到正确 workflow |
| 可靠性 | 隐藏依赖是否减少、gotchas 是否更清楚、验证门禁是否更好 |
| Token 成本 | 常驻上下文更小、总任务 token 尽可能更低 |

如果一个 skill 只是更小，但变慢、变弱，或者更容易误触发，那不算真正优化。每个案例都应该同时写清楚压缩收益和非降级检查。

## 为什么顶尖团队会采用

真正强的团队不会因为一个项目“听起来先进”就采用，它必须同时降低风险、统一质量标准、还能被验证。

Mythos-Skills 最有吸引力的点在这里：

| 采用理由 | 为什么重要 |
|---|---|
| Benchmark-first 优化 | 专家更看重证据，不看口号 |
| 非降级规则 | prompt 更小但能力掉了，没有意义 |
| 跨 Agent 可迁移 | Claude Code、Codex、Cursor、Gemini CLI 都能复用同一套路 |
| 极简入口和标准入口并存 | 可以先从一个文件开始，再扩展到完整结构 |
| 著名 skill 对比 | baseline 越知名，优化越容易建立信任 |
| 法律边界清楚 | 对 source-available 内容做 clean-room 处理，降低采用风险 |

如果要更打动专家，下一层应该补一个小型公开 eval harness 和平台兼容矩阵，明确每个 famous skill 在哪些平台做过验证。

## 为什么普通程序员和白领会收藏

大多数 star 不会来自平台专家，而会来自日常使用 AI 的开发者、产品、设计、分析、运营。

他们的痛点其实很一致：

- agent 对话几轮后就忘记规则
- 复制 skill 之后因为隐藏依赖直接坏掉
- prompt 太长，既贵又慢
- 错误 workflow 在错误时机被触发
- 没人说得清 AI workflow 到底是真的更好，还是只是更吵

对大众用户，最有力的宣传语应该非常直接：

**复制一个文件，或一个 skill 文件夹，就能得到一个更小、更清楚、更容易信任的工作流。**

## 太复杂？直接用极简版

你不需要一次理解整个仓库。

| 模式 | 拷贝什么 | 适合谁 |
|---|---|---|
| Lite | `engine/skill-creator-lite/SKILL.md` | 想要卡帕西式极简，一个文件先用起来 |
| Standard | `engine/skill-creator/` | 想完整使用 P1-P8 创建流程 |
| Gallery | `gallery/famous/<source>/<skill>/` | 想直接用优化后的著名 skill |

仓库可以很深，但入口必须很小。

## 为什么需要它

第一波 agent 工作靠 prompt。

第二波 agent 工作靠 tools。

下一波会靠 skills：把判断、流程、脚本、约束、示例和记忆打包成 agent 能在正确时机自动激活的能力单元。

但现在很多 skill 有共同问题：

| 问题 | 后果 |
|---|---|
| `SKILL.md` 膨胀 | 每次激活都污染上下文窗口 |
| 跨目录依赖 | 复制 skill 后引用断裂 |
| description 写“做什么” | agent 不知道何时触发 |
| 没有反模式 | agent 反复踩同样的坑 |
| 状态存在对话里 | 长任务中途丢失连续性 |
| 只写指令不给脚本 | agent 浪费 token 重造样板 |

Mythos-Skills 把这些失败模式变成一套设计系统。

## 8 条铁律

| # | 原则 | 规则 |
|---|---|---|
| P1 | 简洁即正义 | 上下文窗口是公共资源 |
| P2 | 渐进式披露 | 只在需要时加载细节 |
| P3 | 自包含独立 | 每个 skill 都应像原子单元一样可迁移 |
| P4 | 自由度匹配 | 脆弱操作低自由，创造任务高自由 |
| P5 | 触发优于描述 | 写何时使用，而不是只写它做什么 |
| P6 | 踩坑点即金矿 | 反复失败模式比理想路径更有价值 |
| P7 | 脚本优于指令 | 给 agent 脚本和结构化操作，而不是让它从文字重造 |
| P8 | 记忆外置 | 持久状态放文件，不放对话上下文 |

## 这个项目不一样在哪里

多数仓库回答：“我能复制哪些 skill？”

Mythos-Skills 回答：“什么样的 skill 值得复制？”

你会得到：

- 一套面向 skill engineering 的紧凑方法论。
- 一个用 P1-P8 校验新 skill 的 `skill-creator`。
- 三层结构的生产级示例。
- 可审查的 before/after 优化画廊。
- 面向真实命令执行的安全约束模型。

## 仓库结构

```text
Mythos-Skills/
|-- principles/        # P1-P8 方法论
|-- engine/            # 原则驱动的 skill-creator
|-- skills/            # 原创生产级示例
|-- gallery/           # 社区 skill 优化前后对比
|-- security/          # 命令安全和操作约束
|-- docs/              # 深入文档
|-- DISCLAIMER.md      # 非官方/非关联免责声明
|-- CONTRIBUTING.md    # 贡献指南
|-- SECURITY.md        # 安全策略
`-- LICENSE            # MIT
```

## 快速开始

克隆仓库：

```bash
git clone git@github.com:tayiic/Mythos-Skills.git
cd Mythos-Skills
```

把创建引擎安装到 agent skill 目录：

```bash
mkdir -p .codex/skills
cp -r engine/skill-creator .codex/skills/skill-creator
```

然后对你的 agent 说：

```text
Use skill-creator to design a production-grade skill for my workflow.
```

它会按 P1-P8 引导设计，而不是让 agent 自由发挥。

极简单文件模式：

```bash
mkdir -p .codex/skills/skill-creator-lite
cp engine/skill-creator-lite/SKILL.md .codex/skills/skill-creator-lite/SKILL.md
```

## Gallery: 优化前后对比

gallery 是这个项目的证明面。优先优化知名或被广泛复制的 skills，因为用户能更快理解对比价值。

每个优化案例包含：

- `ORIGINAL.md`：原始版本。
- `SKILL.md`：P1-P8 优化后的紧凑入口。
- `DIFF.md`：改了什么、为什么改、对应哪条原则。
- `BENCHMARK.md`：激活、速度、质量、理解偏差检查。
- `references/`：按需加载的本地细节。
- `operations.json`：必要时提供机器可读操作索引。

目标不是宣称神奇提升，而是展示更少激活上下文、更清晰触发、更少隐藏依赖、更好的失败模式覆盖，以及任务质量不发生明显降级。

优化后的著名 skill 放在 `gallery/famous/<source-slug>/<skill-slug>/`。首批 10-20 个候选见 [GALLERY_PLAN.md](GALLERY_PLAN.md)。

## 支持范围

Mythos-Skills 设计为适配任何支持 skill-like 行为的 agent 平台：

Claude Code、Codex、Cursor、OpenCode、Gemini CLI、GitHub Copilot、自定义 agent harness、团队内部 coding agent。

## 命名和免责声明

Mythos 在这里表示 foundational narrative、origin story、body of principles，也就是 skill engineering 的根基性叙事。

Mythos-Skills 不隶属于、不代表、也不受 Anthropic 或任何其他模型/agent 平台背书。详见 [DISCLAIMER.md](DISCLAIMER.md)。

## 路线图

- 发布完整 P1-P8 原则文档。
- 完整迁移并打磨 `skill-creator`。
- 添加三个原创生产级示例 skill。
- 添加首批 before/after gallery 案例。
- 添加行数、跨引用、三层结构验证脚本。

## 贡献

最好的贡献不是“再加一个 skill”，而是提交一个能教会生态如何写好 skill 的案例。

请先阅读 [CONTRIBUTING.md](CONTRIBUTING.md)，然后提交：

- 紧凑的 `SKILL.md`。
- 只依赖本地 references。
- 优化第三方 skill 时提供 `DIFF.md`。
- 为第三方来源保留许可证和署名。

## License

Mythos-Skills 原创内容使用 [MIT License](LICENSE)。第三方内容保留原始许可证和署名要求，详见 [THIRD_PARTY_LICENSES.md](THIRD_PARTY_LICENSES.md)。

## 快速链接

不想浏览完整仓库时，可以直接从这里开始：

| 需求 | 链接 |
|---|---|
| 下载全部 | [main.zip](https://github.com/tayiic/Mythos-Skills/archive/refs/heads/main.zip) |
| 下载 v002 分支 | [v002.zip](https://github.com/tayiic/Mythos-Skills/archive/refs/heads/v002.zip) |
| 单文件 creator | [skill-creator-lite/SKILL.md](engine/skill-creator-lite/SKILL.md) |
| 标准 creator 文件夹 | [engine/skill-creator](engine/skill-creator/) |
| 著名 skill 优化画廊 | [gallery/famous](gallery/famous/) |
| 性能/上下文 benchmark | [BENCHMARKS.md](BENCHMARKS.md) |
| 第一批 gallery 计划 | [GALLERY_PLAN.md](GALLERY_PLAN.md) |
| Anthropic skill-creator 优化版 | [gallery/famous/anthropic/skill-creator](gallery/famous/anthropic/skill-creator/) |
| Anthropic claude-api 优化版 | [gallery/famous/anthropic/claude-api](gallery/famous/anthropic/claude-api/) |
| Anthropic xlsx 优化版 | [gallery/famous/anthropic/xlsx](gallery/famous/anthropic/xlsx/) |
| Superpowers systematic-debugging 优化版 | [gallery/famous/superpowers/systematic-debugging](gallery/famous/superpowers/systematic-debugging/) |
| Superpowers TDD 优化版 | [gallery/famous/superpowers/test-driven-development](gallery/famous/superpowers/test-driven-development/) |

**如果你相信 skill 应该被工程化，而不是随手写成提示词，欢迎点亮 star。**
