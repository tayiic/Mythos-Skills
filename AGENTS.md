# Project Rules (auto-synced from codex_standard)

> 红线 G19；完整手册：`docs/_shared/CODEX_PERMISSION_APPROVAL_RUNBOOK.md` §10。
当内嵌补丁在读取首个目标前以 `helper_unknown_error: setup refresh had errors` 失败时：
1. MUST 读取 `.codex/.sandbox/setup_error.json` 与当日 sandbox 日志并分类；不得把 helper 初始化失败归因于仓库或补丁。
2. 若日志含 `write ACE grant failed` / `SetNamedSecurityInfoW failed: 5`，MUST 先使用专用 patch-only 模式完成当前精确变更：`codex.ps1 --codex-run-as-apply-patch <complete-utf8-patch>`。
3. MUST 在每个补丁后执行目标 diff 与 diff check。
4. MUST NOT 使用任意 shell 写文件、关闭 sandbox、扩大 writable root，或把退出、重启、重开任务作为默认恢复方案。
5. 持久 ACL 修改 MUST 获得用户对精确根目录的显式批准；SID 必须从当前已知良好 writable root 动态识别，禁止硬编码。
6. patch-only 成功只代表当前落盘恢复；只有 Desktop 内嵌补丁复验成功，才可宣称 helper 永久恢复。
# Project Rules (auto-synced from codex_standard)

## verification

# Fixed Test Execution Protocol
> Universal protocol for turning "we tested it" into a repeatable, reviewable method.
---
## Iron Law
**Do not invent the test method mid-task. Map the change to a fixed path, then execute that path.**
## Required Order
Every non-trivial verification MUST follow this order:
1. **MAP**
   - Identify the affected module, contract, and user path.
   - Map them to the concrete test files or validation commands.
   - If no mapping exists, create or update the project test-scenario index first.
2. **STATIC**
   - Run the smallest static proof first.
   - Examples: import check, lint, source assertion, route/config assertion, schema/contract check.
   - If static evidence already disproves correctness, stop and fix before broader tests.
3. **LAYERED**
   - Run only the smallest sufficient tests in this order:
     1. Unit / logic
     2. Integration / API / orchestration
     3. E2E / page / browser
   - Expand scope only when the previous layer passes but does not yet cover the risk.
4. **RUNTIME**
   - Collect runtime evidence tied to the real failure mode.
   - Health checks, page entry checks, or smoke endpoints are supporting evidence only, not final proof by themselves.
## Acceptance Record
A verification is valid only if it records all four:
1. **Change path** — what changed
2. **Test path** — which test file or command covers it
3. **Risk alignment** — what failure mode it proves or disproves
4. **Result** — pass/fail with key output summary
If any of the four are missing, the verification is incomplete.
## Forbidden Moves
1. Treating `HTTP 200` as full verification
2. Running broad suites before mapping the affected path
3. Mixing unrelated full-suite results into a focused conclusion
4. Using a single giant command when a smaller layered proof exists
5. Verifying frontend-only changes with backend-only evidence, or the reverse
## Frontend Rule
For frontend-affecting work, prefer:
1. lint / type / route assertion
2. targeted browser test file or grep subset
3. concrete page entry proof
4. backend contract proof only if the UI depends on it
## Backend Rule
For backend logic or orchestration work, prefer:
1. import / source assertion
2. targeted unit subset
3. targeted integration or API subset
4. health/debug/runtime proof
5. browser proof only if user-visible behavior changed
## Project Index
Each project SHOULD keep a `TEST_SCENARIOS.md` (or equivalent) that maps:
- test file -> business path
- command -> scope
- when to run -> failure mode
Without this index, test selection becomes improvisation.
## §6 Test Agent Isolation
> 红线 G17 (见 RED_LINES_CATALOG.md)
> Full rules: see .codex/protocols/ directory
## Grand Orchestrator Self-Check

- Sync Source: X:\workspace\AIStandard\codex_standard
- Check Command: `pwsh X:\workspace\AIStandard\codex_standard\generators\sync-engine.ps1 -ProjectPath . -Status`
- Sync Command: `pwsh X:\workspace\AIStandard\codex_standard\generators\sync-engine.ps1 -ProjectPath . -Write -AutoApply`
- Rule: Before starting any task, run -Status to check if sync is needed. If out-of-date, suggest user run sync.

<!-- AI-ROUTING-V1 -->
## AI 模型路由治理（workspace 统一 v1）

> 激活标志：本项目 `.ai/PROJECT_ROUTING.yaml`；权威规范：`X:\workspace\AIStandard\codex_standard\universal\ai_model_routing.md`（数据：同目录 `routing\*.yaml`）。本节为执行要点，完整矩阵/评分/降级链见权威规范。

**每次任务第一个动作：输出 ROUTE 行，并追加一条 JSON 到 `.codex/runs/routing/<YYYYMMDD>.ndjson`（目录不存在则先创建）：**

```text
ROUTE: model=<别名> reasoning=<low|medium|high> risk=R<n> complexity=C<n> context=X<n> parallel=P<n> agents=<k> gate=<-|rev|MMPI>
```

角色别名（物理模型见 model-aliases.yaml，换代只改数据不改规则）：`MODEL_EXPLORER`（luna/low，搜索提取时间线）/ `MODEL_ANALYST`（terra/low，多文件阅读小改）/ `MODEL_ENGINEER`（sol/medium，开发重构）/ `MODEL_REVIEWER`（sol/high，审查与 R3 独立 gate）/ `MODEL_ARCHITECT`（astra，架构与 R4 最终 gate）。

执行铁律：
1. **Risk Floor 优先于 Complexity**；R4（本项目高危项见 overlay）最终结论/动作必须 `MODEL_ARCHITECT`（Astra）或人工，缺位挂起不降级。
2. **ROUTE_MISMATCH 拦截**：当前会话模型低于矩阵要求 → 只许取证（读码/搜索/整理），禁止宣布最终结论或执行最终动作，必须提示切换模型或人工裁决。
3. R3/R4 触发 MMPI（暂停 AI 生成 → 跨模型独立审查 → 人工解锁）；R2+ 结论必须附可回放证据（`path:line` / `cmd#hash`），证据不足不得宣布完成。
4. 升级纪律：同级 2 次无新证据 → 升一级并把 prompt 重构为 Task Packet；连续 2 次升级无进展 → 熔断停止转人工，禁止烧额度原样重试。
5. 大上下文先压缩（定位 → 精确 read → diff → packet）再给强模型；禁止全量日志/全量测试输出进上下文。
6. 用户 override 服从，但第 1/2/3 条安全规则不可被成本偏好覆盖。

<!-- /AI-ROUTING-V1 -->
