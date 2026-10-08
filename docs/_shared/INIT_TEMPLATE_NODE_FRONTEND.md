---
schema_version: shared-doc.v1
category: init_template
applies_to: node-frontend-projects
sync_source: codex_standard/templates/shared-docs/INIT_TEMPLATE_NODE_FRONTEND.md
---

# Node / 前端项目初始化模板

适用: Vue、React、Vite、Ant Design Vue、Playwright/Vitest 前端、Node 工具项目。

## 必检文件

| 文件 | 必检内容 |
|------|----------|
| `package.json` | 包管理器、scripts、测试/构建命令 |
| `pnpm-lock.yaml` / `package-lock.json` | 锁文件必须存在且与包管理器一致 |
| `vite.config.*` / `tsconfig*.json` | dev server、alias、strict、build 输出 |
| `playwright.config.*` | baseURL、webServer、浏览器项目、trace/screenshot 策略 |
| `.env.example` / `.env.*` | Vite 变量、API base URL、mock 开关 |
| `frontend/Dockerfile` | build/runtime 分层、静态产物位置 |

## 初始化步骤

1. 确认包管理器: 有 `pnpm-lock.yaml` 时默认 `pnpm`，有 `package-lock.json` 时默认 `npm`。
2. 确认 Node 版本: 从 `.nvmrc`、Dockerfile、CI、README 或 `engines` 字段记录。
3. 确认 dev 命令: 例如 `pnpm -C frontend dev`、`pnpm dev`、`npm run dev`。
4. 确认构建命令: 例如 `pnpm build`、`npm run build`，并记录产物目录。
5. 确认测试集合: unit、typecheck、lint、E2E、视觉/浏览器错误检查。

## E2E 与认证边界

- 页面 E2E 默认走真实 UI 登录或项目提供的 `auth.setup` / login fixture。
- 禁止手写 token、localStorage、sessionStorage、store、cookie、动态路由来伪造页面认证态。
- 如果项目使用 mock 登录，必须标明 dev-only 边界和生产禁用条件。

## 配置记录模板

| 配置项 | 来源 | 是否可提交 | 说明 |
|--------|------|------------|------|
| `VITE_API_BASE_URL` | `.env.development` / runtime | 示例可提交 | 不写生产密钥 |
| mock 开关 | `.env.*` / dev server | 可提交 | 必须 dev-only |
| 端口 | `vite.config.*` / `project-preset.json` | 可提交 | 同机唯一 |
| 浏览器测试 baseURL | `playwright.config.*` | 可提交 | 与 dev server 一致 |

## 常见证据

- `pnpm -C frontend install --frozen-lockfile`
- `pnpm -C frontend typecheck`
- `pnpm -C frontend test`
- `pnpm -C frontend build`
- `npx playwright test --workers=1 --max-failures=1`
