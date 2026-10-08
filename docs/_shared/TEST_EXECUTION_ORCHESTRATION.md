---
schema_version: shared-doc.v1
category: test_execution_orchestration
applies_to: all-projects
sync_source: codex_standard/templates/shared-docs/TEST_EXECUTION_ORCHESTRATION.md
---

# 原子测试组合、证据账本与 Harness 可靠性（ELV-1）

> 本文是 AIStandard 下发到各项目的测试编排底线。项目可收紧时限和范围，不得放宽失败分账、去重和生产隔离。

## 0. 成熟路线与适用边界

- 采用项目既有唯一测试入口、白名单、隔离规则和证据格式；本文不授权直跑底层测试、修改冻结总控、改超时/重试/环境或跳过发布门禁。
- 先恢复已有验证账本，再决定是否需要执行。已绿且依赖未变的切片禁止因换任务、换代理、重新接管、单纯 commit hash 或无关文件变化而重跑。
- Owner 明确禁止重复测试时，不得自行增加“最终 Full 例外”。若唯一合法入口必然重复已绿切片，暂停该命令并提出精确的续跑能力/门禁决策；禁止临场拼命令、使用诊断 Skip 冒充验收或自动修改总控。
- 简单任务只需现有任务文档中的几行账本和最小检查；不强建新系统。需要委派时只拆可独立完成的有界任务，主控负责依赖和证据裁决，节约重复读取与输出。

## 1. 角色边界

- 主控：影响面、测试卡、风险、证据裁决和 SSOT。
- 实现代理：只修改代码与测试源码，不执行测试。
- 测试代理：只执行白名单命令、采集物证，不修改产品实现。

## 2. 稳定 T0

T0 必须由仓库内受版本控制的单一脚本生成结构化结果，覆盖安全门禁、权威环境、精确残留进程、挂载/源码指纹。禁止代理临场拼接 PowerShell/Python 采集器。

## 3. 失败分账

- `HARNESS_FAILED`：预检、采集、证据或 watchdog 自身失败；产品测试停止，不能记产品 FAIL。
- `PRODUCT_FAIL`：目标命令已执行并以非零退出或断言失败；保留首个失败，不自动重跑。
- `AGENT_INFRA_FAILED`：代理额度、审批链、失联或调度失败且无命令证据；不形成产品结论。

连续两次 pre-test Harness 失败必须熔断发卡，先修复并审阅 Harness。

## 4. 证据与撤换时限

- 接卡 10 秒内创建卡元数据或证据目录。
- 每 30 秒更新结构化进度。
- 60 秒无新证据且无状态回报，主控中断并撤换代理。
- 撤换前核对宿主和容器残留；同一容器/target 禁止重叠测试并发。

## 5. 指纹复用与命令去重

### 5.1 原子测试与一份验证账本

默认以一个测试文件为一个原子测试；同一文件不同参数/数据矩阵、headless/headed 或环境不能互相替代。`atom_id` 至少由项目内测试文件路径与必要运行变体构成；Full/Auth 等组合 Profile 的名称本身不产生新原子，只有实际命令、夹具或环境语义不同才区分变体。项目已有更细且隔离可靠的 case/module 可沿用；共享生命周期、顺序依赖或不可分割 E2E 必须整体作为一个原子，不能为剔除已绿项拆坏语义。静态检查、构建和运行验收也以项目批准的最小完整命令单元登记。

复用项目现有 SSOT/测试卡/证据索引，不复制原始日志。每个原子记录：ID、命令/Profile/变体、覆盖文件和共享依赖（测试、夹具、配置、数据库/外部状态）、源码/环境指纹、时间、证据位置/摘要哈希、退出码/统计，以及失效/重跑原因。不得保存密钥明文。新建/删除/重命名测试必须更新组合清单，不能依赖旧清单默默漏测。

| 状态 | 含义 | 下一步 |
|---|---|---|
| `PENDING` | 未取得执行证据 | 完成实现后按影响面验证 |
| `RUNNING` | 已启动且有运行证据 | 等待该运行，禁止重叠启动 |
| `LOCKED_GREEN` | 真实 PASS，覆盖依赖及有效性可证明 | 复用，不重跑 |
| `FAILED` | 真实产品断言/目标命令失败 | 保留证据，分析后成组修复 |
| `INVALIDATED` | 历史 PASS 的相关依赖或证据有效性已变化 | 记录原因，回归最小受影响切片 |
| `BLOCKED` | Harness/代理/权限/入口能力阻断 | 不计产品 PASS/FAIL；先解决明确阻断 |

`LOCKED_GREEN` 是可复用切片状态，不代表当前整库或生产 Gate 全绿。无法恢复依赖边界的旧 PASS 只能保留为历史证据，不得猜测为当前有效。

### 5.2 最小失效域

- `environment_fingerprint` 绑定容器/运行时、挂载、offline 配置、安全脚本和相关外部状态；可变数据库/服务观察按项目新鲜度规则复核，不能仅凭源码未改无限复用。
- `source_fingerprint` 绑定本切片覆盖文件及其共享依赖、测试合同、夹具；整树指纹和 commit 用于溯源，不是“一处变化全体失效”的替代品。
- 修改某切片测试夹具、公共认证合同、依赖版本或运行配置时，失效沿实际依赖扩散；仅改别处文档/改提交号不自动失效。无法判断的关联明确记为不确定，补只读依赖审查后再选必要范围。
- 环境未变且安全时效满足时复用可信 T0；Harness/代理切换不抹掉已证明执行的命令。保留旧结果，新增失效记录，不覆盖历史证据。

### 5.3 重跑门槛

发出命令前先查账本。重跑已绿切片必须记录具体理由：相关依赖/环境/测试合同变化、证据缺失/损坏/到期、Owner 明确要求复现，或项目强制最终 Gate。没有理由则不执行；“再保险”“换了代理”“准备提交”不是理由。

如已有冻结总控支持合法切片/续跑则直接使用；否则遵守 §0 的冲突处理，不能为追求速度伪造续跑或 PASS。

### 5.4 执行前恢复证据与计划

在原账本恢复显式历史来源，记录：`目标/停止条件 | 候选与失效依赖 | Profile/模式/正式计划 | 来源及RUN/REUSE | RUN理由/首失败/变化证据 | 正式结果及执行/复用/失败/缺失`。首次执行说明首次；明确复现附Owner要求，不另建一套账本。

有正式只计划能力的批准入口，先以相同Profile、模式和来源生成计划，再执行。历史PASS存在而计划未获得合法来源时先核对遗漏、损坏、真实失效或模式不符，不能因“无既往PASS”而机械重跑。计划结构缺口和总控校验失败须解决；只读投影或辅助审查不能豁免，也不证明当前依赖/环境/原日志有效。候选或相关环境变化后重新计划。没有此能力的项目保持现有合同并登记适配缺口，禁止借用其他项目的参数。

## 6. 最短回归

1. 先读取全部已产生的失败输出及同类迁移点，一次完成已知相关实现、断言、夹具和接口收尾；禁止“修一个可预见迁移点 → Full 从头跑 → 找下一个”。窄范围 TDD 不受此限制。
2. 尊重成熟路线的 fail-fast：没有执行到的阶段保持 `PENDING`；不得继续一个已停止的测试，只为收集更多失败。
3. 局部修复先用项目入口允许的最小静态证据排除已知缺陷，再验证原失败测试与受影响模块；静态已否定正确性时不启动昂贵后续工作。只有公共合同、依赖图或触发矩阵要求时扩大范围；不机械复跑旁路已绿项。此原则不授权调整冻结运行器顺序、增加静态原子或直跑底层工具。
4. 同一命令/输入没有实质变化却连续失败时停止重试；先定性并说明证据。稳定性/可重复性试验必须有独立批准的次数与目的，不能重试到绿。

## 7. 最终 Gate 与分批交付

- 将 `final_gate` 与切片状态分开记录：`NOT_REQUIRED | PENDING | RUNNING | PASSED | FAILED | BLOCKED`。
- 全量测试的定义是完整原子清单的组合，不是“每次重新执行全部文件”。`Full/Auth/Investor/...` 等 Profile 应映射为受版本控制的原子 ID 清单；共享原子在一次计划中去重，运行变体不得合并。
- 在候选代码与依赖清单冻结后生成组合计划：`required_atoms = run_atoms + reuse_atoms`（两者不重叠且并集完整）；`reuse_atoms` 只允许仍有效的 `LOCKED_GREEN`；`run_atoms` 为其余需要新证据的原子。`BLOCKED` 原子保持缺口，不能移出 required 清单凑绿。
- 实际调度只执行 `run_atoms`；每个原子独立退出码/证据，按项目隔离约束串行或并行。未执行到的原子仍 `PENDING`，不能因前一原子 PASS 或同文件别的模式 PASS 而转绿。
- 组合验收必须核对所有 required ID 恰好覆盖一次、依赖对当前候选有效、无缺失/失败/阻断，并输出组合清单：当前候选、计划版本/哈希、executed/reused/invalidated/failed/missing、逐原子原始 evidence/哈希及复用理由。原始运行 commit/指纹不改写；复用判定作为新记录链接它。
- 只有项目总控正式支持该组合与完整性核验，才能报告 `COMPOSED_PASS`（例如“全量覆盖 20 个原子，本轮执行 3、复用 17”）；不得说“本轮重新执行 20 个”。现有项目要求单次同指纹完整运行/特定模式时，先记录为待适配合同，不自动用新的通用规则宣告其 Gate 通过。
- 完成已知代码/测试/配置收尾并冻结候选后，才安排项目规定的最终组合及必要模式（如 headless → headed）；避免将最终 Gate 当迭代探针。
- 规则和文档实际被合同读取时一并冻结。最终裁决使用项目批准的证据位置；若收尾改动触及覆盖依赖，登记失效并只补必要原子。不得把所有文档视为无关，也不得在未审查实际读取闭包时缩窄指纹。
- “一次规划最终验证”不意味着失败后免验。失败后回到有依据的最小修复和失效判定；如项目仍要求新的完整 Gate，先说明原因，且不得违反 Owner 的禁止重复指令。
- 不得拼接不同指纹的历史 PASS 冒充当前 Full PASS。不同运行记录只有经上述逐原子依赖复核、合法总控组合后，才成为当前候选的有效组合证据。
- 已授权 Git 交付时，按依赖完整、验证可对应的批次显式暂存、提交、Push 并核对远端；不得只为拆小提交制造中间不可用版本。未授权则不自动 Push。测试 PASS、commit、远端到达、生产签收分别报告。

## 8. 最小回传

```yaml
task_id: ID
source_fingerprint: SHA256
environment_fingerprint: SHA256
command_ledger:
  - atom_id: tests/auth/test_session.py::headless-dev
    test_file: tests/auth/test_session.py
    variant: headless-dev
    command: project-approved entry and profile
    dependencies: [covered-files, shared-fixtures, relevant-config]
    state: LOCKED_GREEN
    evidence: existing-run-summary-path
    tested_source_fingerprint: SHA256
    tested_environment_fingerprint: SHA256
    exit_code: 0
    counts: {passed: 12, failed: 0}
    invalidation_or_rerun_reason: null
composition:
  plan_version: reviewed-profile-manifest-hash
  candidate: current-candidate-fingerprint
  required_atoms: [tests/auth/test_session.py::headless-dev]
  executed_atoms: []
  reused_atoms: [tests/auth/test_session.py::headless-dev]
  missing_atoms: []
  verdict: PENDING
final_gate: PENDING
verdict: PASS | PRODUCT_FAIL | HARNESS_FAILED | AGENT_INFRA_FAILED | BLOCKED
evidence: path
```

每次接续只需说明：代码是否写完、已绿/失效/待验清单、当前阻断、下一条允许命令。原始失败与账本必须可定位；禁止只重复“继续测试”而不增加证据。

## 9. 项目总控适配边界

推广本文仅安装规则，不等于改写各项目测试设施。总控适配须在项目允许的变更范围内单独落地：固定原子清单 → 逐原子执行证据 → 依赖失效计算 → 续跑选择 → 组合完整性 Gate；保留原有 Profile 对外入口、隔离、时限、失败停止、证据保密和生产写操作审批。适配前不能临时直跑 pytest/Vitest/Playwright 或偷改原始 summary；适配完成前报告“规则已推广，原子续跑尚未接入”。
