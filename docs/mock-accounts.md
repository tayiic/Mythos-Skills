---
schema_version: shared-doc.v1
category: baseline_operational
applies_to: all-projects
sync_source: codex_standard/templates/shared-docs/BASELINE_MOCK_ACCOUNTS.md
target_path: docs/mock-accounts.md
---

# mythos-skills Mock 账号

> 最后更新: 2026-08-30
> 用途: 开发环境测试用，严禁在生产环境使用

## 一、Mock 认证

### 1.1 开发环境绕过认证

设置环境变量 `ENV=TAYII_NOTEBOOK` 后，后端自动启用 mock 认证模式。

### 1.2 Mock 用户

| 角色 | 用户名 | 密码 | 说明 |
|------|--------|------|------|
| 管理员 | admin | admin123 | 全部权限 |
| 普通用户 | user | user123 | 基本权限 |
| 合格投资者 | investor | investor123 | 可查看基金详情 |

### 1.3 Mock Token

```json
{
  "access_token": "mock-token-mythos-skills-dev",
  "token_type": "bearer",
  "expires_in": 86400
}
```

直接设置 HTTP Header: `Authorization: Bearer mock-token-mythos-skills-dev`

---

## 二、Mock 外部接口

### 2.1 合格投资者认证

| 接口 | Mock 响应 |
|------|----------|
| `POST /api/v1/investor/qualification` | `{"status": "passed", "level": "qualified"}` |

### 2.2 统一认证（SSO）

| 接口 | Mock 响应 |
|------|----------|
| `POST /api/v1/auth/login` | 返回 mock token |
| `POST /api/v1/auth/logout` | `{"status": "ok"}` |
| `GET /api/v1/auth/me` | 返回当前 mock 用户信息 |

---

## 三、Mock 数据

### 3.1 基金数据

| 基金代码 | 基金名称 | 净值 |
|---------|---------|------|
| FUND001 | 测试基金一号 | 1.2350 |
| FUND002 | 测试基金二号 | 0.9870 |

### 3.2 披露报告

开发环境自动生成 mock 季度报告和年度报告，数据来源为 `backend/app/seed/mock_disclosure.py`。

---

## 四、切换认证模式

```powershell
# 开发模式（Mock）
$env:ENV = "TAYII_NOTEBOOK"

# 生产模式（真实 SSO）
$env:ENV = "THS_PRODUCT"
```