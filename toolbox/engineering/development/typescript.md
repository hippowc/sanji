# TypeScript

## 1. 使用场景划分

| 场景 | 运行时 | 关注点 |
|------|--------|--------|
| **Web 前端** | 浏览器 | bundle 体积、CSR/SSR、浏览器兼容 |
| **Node 服务端** | Node.js / Deno（少数） | IO、进程模型、与前端共享类型 |

 monorepo（pnpm workspace、Nx、Turborepo）可在前后端 **共享类型与校验逻辑**，注意 **边界**：服务端密钥永不进入前端 bundle。

## 2. 包管理与 lockfile

- **npm / pnpm / Yarn**：团队统一；**lockfile 提交**。  
- **workspace**：共享 internal packages（`@corp/types`）减少重复 DTO 定义。

## 3. 类型检查与 Lint

- **`tsc --noEmit`** 作为 CI 门禁；避免仅靠 IDE。  
- **ESLint** + TypeScript 插件；规则集可用 `@typescript-eslint/recommended`。  
- **Prettier** 统一格式；与 ESLint 集成避免冲突。

## 4. 前端构建

| 工具 | 特点 |
|------|------|
| **Vite** | 开发体验快；默认适用 SPA 与现代浏览器 |
| **Webpack** | 生态老、配置灵活 |
| **esbuild / SWC** | 极快转译；常作为底层 |

**环境变量：** Vite 下仅 `VITE_*` 注入客户端；**禁止** `VITE_` 前缀存放密钥。服务端渲染框架（Next.js 等）遵循各框架的 `NEXT_PUBLIC_*` 类似规则。

## 5. Node 服务端

- **框架**：Express、Fastify、NestJS（结构化 DI）；选型看团队背景。  
- **进程**：生产用 **多实例 + 反向代理** 或 platform 托管；PM2 适用于 VM 场景。  
- **原生模块**：注意与 Alpine musl 兼容性。

## 6. 测试

- **Vitest / Jest**：单元与组件测试。  
- **Playwright / Cypress**：E2E；与 staging 环境联动。

## 7. 供应链

- **`npm audit`** 或 Snyk 等；lockfile 变动 PR 审查依赖diff。  
- **Dependabot / Renovate**：自动化_minor/patch 升级（策略可控）。

## 相关链接

- [Web](./web.md)
- [服务端](./server-side.md)
