# Mythos-Skills

> 面向 AI Agent 的下一层能力：Skill Engineering。

语言：[English](README.md) | [简体中文](README.zh-CN.md)

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

## 先看证据

这个项目最重要的卖点不是口号，而是可验证优化。

首批 gallery 会优先选择知名或高频复制的 skills，用 Mythos-Skills 的 P1-P8 原则重构，然后展示明确差异：

| 案例 | 优化前 | 优化后 | 证明方式 |
|---|---|---|---|
| TDD workflow | 激活文件过长，流程和细节混在一起 | 入口层压缩，细节进入 references | 行数和 token 估算 |
| Debugging workflow | 存在隐含跨 skill 依赖 | 自包含 skill 包 | 可迁移检查清单 |
| Planning workflow | 描述偏“做什么” | 改成触发优先的 description | 触发质量 rubric |

每个案例都应该包含 `ORIGINAL.md`、优化后的 `SKILL.md`、`DIFF.md`、本地 `references/` 和提升表。gallery 是这个项目建立信任的地方。

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

## Gallery: 优化前后对比

gallery 是这个项目的证明面。优先优化知名或被广泛复制的 skills，因为用户能更快理解对比价值。

每个优化案例包含：

- `ORIGINAL.md`：原始版本。
- `SKILL.md`：P1-P8 优化后的紧凑入口。
- `DIFF.md`：改了什么、为什么改、对应哪条原则。
- `references/`：按需加载的本地细节。
- `operations.json`：必要时提供机器可读操作索引。

目标不是宣称神奇提升，而是展示更少激活上下文、更清晰触发、更少隐藏依赖、更好的失败模式覆盖。

## 支持范围

Mythos-Skills 设计为适配任何支持 skill-like 行为的 agent 平台：

Claude Code、Codex、Cursor、OpenCode、Gemini CLI、自定义 agent harness、团队内部 coding agent。

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

**如果你相信 skill 应该被工程化，而不是随手写成提示词，欢迎点亮 star。**
