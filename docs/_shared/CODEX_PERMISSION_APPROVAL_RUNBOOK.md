---
schema_version: shared-doc.v1
category: baseline_operational
applies_to: all-projects
sync_source: codex_standard/templates/shared-docs/CODEX_PERMISSION_APPROVAL_RUNBOOK.md
---

# Codex 权限、沙箱与审批控制面运行手册

> 目标：让工作区内非高危命令自动执行，同时保留对破坏性操作、生产写入、敏感数据和广泛越界的拦截。

## 1. 四层故障分类

看到“授权失败”或“Git 未执行”时，必须先判断失败层级：

| 层级 | 典型证据 | 正确结论 |
|---|---|---|
| 审批控制面 | `autoApprovalReview`、`stream disconnected`、命令未启动 | Auto-review 子会话失败 |
| Sandbox 启动 | `CreateProcessAsUserW failed`、`spawn EPERM` | 本地执行边界或进程启动失败 |
| 命令执行 | 已有 PID/退出码/标准错误 | 命令自身失败 |
| Git 专属 | transport、凭据、remote、真实 index lock | Git 路线失败 |

不得把命令启动前的审批断线记为 Git、Docker、测试或产品失败。

## 2. 权限合同

推荐保持：

```text
Permission profile: workspace
Approval policy: on-request
Approvals reviewer: auto_review
```

Auto-review 只是审批审查者，不会扩大 sandbox、writable roots、网络或项目规则。

### 自动执行

- 工作区内读、搜索、编辑和生成。
- 普通构建、静态检查及项目锁定的成熟测试入口。
- Git 只读命令。
- 已验证的精确 prefix rule。
- Auto-review 判定为低风险的必要越界。

### 继续拦截

- 工作区外写入。
- 广泛删除、覆盖和递归移动。
- 生产写操作。
- 凭据读取或外传。
- `git reset --hard`、强推、remote 改写。
- 关闭沙箱或长期 Full Access。

禁止通过 `["pwsh"]`、`["python"]`、`["git"]`、`["docker"]` 等宽泛解释器规则消除提示。

## 3. Windows PowerShell 启动排查

Windows 下必须区分：

```text
C:\Users\<user>\AppData\Local\Microsoft\WindowsApps\pwsh.exe
C:\Program Files\PowerShell\7\pwsh.exe
```

若 Store alias 在 sandbox 内出现访问拒绝，而其他进程可启动，应优先验证：

1. 当前 Windows sandbox 实现。
2. `pwsh` 实际解析路径。
3. 标准 MSI PowerShell 是否存在。
4. Codex 更新前后的 START/SUCCESS 日志差异。

不要通过改用未经项目允许的 Shell、WSL、容器 Git 或临时 transport 绕过。

## 4. 审批 WebSocket 网络合同

Codex 审批和模型流需要稳定的 ChatGPT 控制面连接：

- 允许 `wss://chatgpt.com/` 经 TCP 443 建立 WebSocket。
- 允许标准 WebSocket `Upgrade`。
- 代理、防火墙、安全网关和 TLS/SSL 检查不得阻断、改写或提前关闭长连接。
- 检查 idle timeout、最大 frame size 和最大 message size。
- 禁止任何小于 60 秒的强制会话上限。

若当前网络失败，应使用可信直连或不经过相同代理/安全网关的网络做 A/B 验证。不能仅凭一次断线判定为服务端或本机根因。

### 4.1 全局配置、任务快照与重启

- 用户级 `config.toml` 决定新进程可读取的全局默认；项目文档、AGENTS 和 AIStandard 共享手册本身不授予运行权限。
- 每个任务仍有独立的 Permission Profile、approval policy、reviewer、writable roots 和网络边界。
- 全局 sandbox 修改后必须完全退出并重启 Codex；旧任务应重新打开，关键验证优先在新任务执行。
- 一个任务中的文字授权不自动成为其他任务的永久白名单。
- 不得为了跨项目少授权而把整个工作区父目录加入所有任务的 writable roots；每个任务只写自身项目和明确附加根目录。
- 只有重启后的 60 秒门禁通过，才能宣称全局修改已经生效并减少普通授权。

## 5. 60 秒稳定性门禁

修复后必须满足：

1. 连续 10 个受控、低风险的 Auto-review 样本全部完成。
2. 每个稳定性样本持续满 60 秒。
3. 审批开始事件均有完成事件。
4. `stream disconnected`、reviewer timeout、command-before-start failure 均为 0。
5. 至少一次项目成熟 Git 路线中的必要审批完成，并确认 Git 子进程真实启动。
6. 再观察两个真实任务或等价的 30 条安全命令。

## 6. 断线后的处理

1. 停止解释业务结果，先确认命令是否启动。
2. 对有副作用操作只做一次只读状态确认。
3. 若未启动，记录为审批控制面阻断；不要改写成命令失败。
4. 不换工具、不改 Shell、不放宽 sandbox 绕过同一拒绝。
5. 恢复审批连接后沿原成熟路线继续。

## 7. 配置变更原子性

任何用户级 Codex 配置变更必须：

1. 备份原文件。
2. 记录字节数、修改时间和 SHA-256。
3. 断言旧值只出现一次。
4. 执行单点替换。
5. 断言新值存在。
6. 再次记录 SHA-256。
7. 重启 Codex并在新任务快照验证。

不得手工修改 Desktop 内部状态文件来模拟 UI 权限变更。

## 8. 支持证据包

跨网络仍可复现时，收集：

- Codex Desktop 版本、安装路径和二进制哈希。
- 发生时间及明确时区。
- 任务 ID、turn ID、tool call ID。
- `autoApprovalReview/started` 至断开的最小日志窗口。
- session JSONL 最小脱敏片段。
- 网络 A/B、代理/VPN/TLS 检查和 WebSocket 超时策略。
- 当时 OpenAI 状态页结果。

不得包含令牌、Cookie、Authorization header、证书私钥或业务敏感数据。

## 9. 官方参考

- <https://help.openai.com/en/articles/9247338-network-recommendations-for-chatgpt-errors-on-web-and-apps>
- <https://learn.chatgpt.com/docs/sandboxing/auto-review>
- <https://status.openai.com/>

## 10. Windows Sandbox 写入前失败：诊断与恢复

### 10.1 适用故障签名

以下条件同时成立时，归类为 **Sandbox helper 初始化失败**，不是仓库文件损坏，也不是补丁内容冲突：

1. `apply_patch` 在读取第一个已存在目标文件前失败。
2. 对多个不同文件重复出现同一错误。
3. 只读命令仍能正常读取目标文件。
4. `.codex/.sandbox/setup_error.json` 或当日日志出现：

```text
helper_unknown_error: setup refresh had errors
```

若日志进一步出现：

```text
write ACE grant failed on <workspace>
SetNamedSecurityInfoW failed: 5
```

则根因已收敛为：Sandbox helper 在刷新工作区写权限 ACE 时被 Windows 拒绝。不得把它表述为“仓库不可写”“需要重开任务”或“业务代码失败”。

### 10.2 强制处置顺序

1. 记录原始错误、时间、任务 ID 和首个目标路径。
2. 只读确认目标存在、卷类型、owner、继承与当前 ACL；不得先改权限。
3. 读取 `.codex/.sandbox/setup_error.json` 和当日 `sandbox.YYYY-MM-DD.log`，定位第一条 `write ACE` 失败。
4. 判断是否满足 10.1 的全部条件；不满足则回到四层故障分类，不得套用本节降级。
5. 满足条件后，可使用 10.3 的专用 patch-only 恢复完成当前精确补丁。
6. 每个补丁后立即执行 `git diff -- <targets>` 与 diff check；失败即停止，不得继续扩大写入面。
7. 当前任务完成后再评估 10.4 的永久 ACL 治理；它不是应急落盘的前置条件。

**不得把退出、重启或重开任务作为此故障的默认解法。** 这些动作可能更换任务快照，但不能修复已经由日志确认的 Windows ACL 拒绝。

### 10.3 唯一允许的应急落盘通道

仅在 10.1 已证实时，允许调用已安装 Codex CLI 的专用补丁模式：

```powershell
C:\Users\<user>\AppData\Roaming\npm\codex.ps1 --codex-run-as-apply-patch <complete-utf8-patch>
```

约束：

- 输入必须是完整、可审计的 UTF-8 patch。
- 只允许修改用户已授权范围内的精确文件。
- 禁止改用 `Set-Content`、Python、重定向或任意 shell 写入模拟补丁。
- 禁止关闭 sandbox、扩大 writable root 或申请宽泛解释器白名单。
- 禁止使用受保护的 WindowsApps shim 代替已验证的 npm wrapper。
- patch 成功只证明“当前变更已落盘”，不证明 Desktop 内嵌 helper 已永久修复。

### 10.4 永久 ACL 治理审批边界

持久修改目录 ACL 属于系统权限变更，必须获得用户对**精确目标根目录**的显式批准后才能执行。批准后仍须满足：

1. 先保存目标根目录的 owner、继承状态、完整 SDDL 和 ACL 备份。
2. 从当前任务的已知良好 writable root 动态识别正在使用的 `CodexSandboxUsers` 与 sandbox capability；禁止硬编码 SID，SID 可能随安装或版本变化。
3. 仅以 additive 方式授予目标根目录及子项所需的 `Modify`；禁止改 owner、关闭继承、删除既有 ACE 或授予 `FullControl`。
4. 对网络盘、非 NTFS、非当前用户所有或受组织策略保护的目录，停止自动修复并升级人工管理员处理。
5. 修复后用 Desktop 内嵌 `apply_patch` 做一个可恢复的小文件验证；成功后回滚验证文件并保留日志。
6. 若验证失败，移除本次新增的精确 ACE 并恢复原 SDDL，不得继续叠加权限。

### 10.4.1 已获批准但 DACL 仍被拒绝

若已获得精确根目录授权，且使用 `Set-Acl` 与 Windows 原生 `icacls /grant` 仍均返回 `Access is denied` 或 `Attempted to perform an unauthorized operation`：

1. 结论是**当前执行令牌不具备该目录 DACL 管理权**，或目录受组织策略/上级 ACL 约束；不能再归因于 Codex patch 内容。
2. MUST 只读确认新增 ACE 未落地、owner/继承状态未变化，并保留两个失败命令的退出码与最小错误文本。
3. MUST 停止重复 ACL 写入；不得尝试 takeown、关闭继承、改 owner、提升为 FullControl 或扩大到工作区父目录。
4. 需要永久修复时，移交有该目录 ACL 管理权的 Windows 管理员；其操作仍必须遵守 10.4 的 SDDL 备份、动态 SID、additive Modify 和内嵌 helper 复验要求。
5. 在管理员完成并复验前，继续使用 10.3 的受限 patch-only 通道；不得宣称 Desktop helper 已永久恢复。

`setup_error.json` 当前为空只代表该时刻没有留下 setup 错误；它不是 ACL 修复成功或 helper 稳定性的证据。至少要有连续的内嵌 `apply_patch` 创建与删除验证都成功，才能改变该结论。

### 10.5 必需证据

- `setup_error.json` 的错误码与消息。
- 当日日志首条 `write ACE grant failed` 和 Windows 错误码。
- 目标根目录与已知良好 writable root 的 ACL 对照（脱敏）。
- patch-only 命令退出码、目标 diff、diff check。
- 若做永久修复：用户批准、ACL 备份、添加的精确 ACE、内嵌 helper 复验与回滚结果。

## 11. 2026-08-12 已确认案例

GlobalMonitoring 工作区曾同时满足 10.1 的四项条件。根因证据为 `SetNamedSecurityInfoW failed: 5`；同任务使用 npm wrapper 的 `--codex-run-as-apply-patch` 成功完成精确补丁和后续验证，无需重开任务。历史证据与裁决见 AIStandard：

`docs/Codex_Windows_Sandbox_落盘失败事故复盘_20260812.md`
