---
schema_version: shared-doc.v1
category: sensitive_info_policy
applies_to: all-projects
sync_source: codex_standard/templates/shared-docs/SENSITIVE_INFO_POLICY.md
---

# 敏感信息策略

> 本文件由 sync-engine 自动同步，禁止项目手动修改。

## 分级

| 级别 | 处理方式 | 标注 |
|---|---|---|
| 允许暴露 | 经用户同意后明文出现 | `<!-- EXPOSABLE: user-confirmed -->` |
| 环境变量 | 通过 .env 注入，代码引用变量名 | `$env:VARIABLE_NAME` / `os.environ["VAR"]` |
| 严格禁止 | 绝对不可出现 | N/A |

## 标注示例

```python
# <!-- EXPOSABLE: user-confirmed -->
DB_HOST = "localhost"  # 允许暴露，已用户确认

# 环境变量引用
DB_PASSWORD = os.environ["DB_PASSWORD"]  # 从 .env 注入
```

## Secret Scan 规则

sync-engine 内置 12 种前缀模式 + 3 种长值模式：
- 前缀：sk-proj-, sk-ant-, sk-live-, sk-test-, ghp_, gho_, AKIA, xoxb-, xoxp-, glpat-, eyJhbG, -----BEGIN
- 长值：api_key/secret_key/access_token >= 20 chars

## 关联

- 全局红线 G7/G8 → [RED_LINES_CATALOG.md](./RED_LINES_CATALOG.md)
