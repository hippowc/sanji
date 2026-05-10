# 开发：语言、多端与工程化

本卷面向 **Java、Python、Go、TypeScript** 四类语言，以及 **服务端、Web、桌面、移动** 四类交付形态，给出 **工程化清单与选型维度**。正文不是语法教程，而是帮助你在公有云最小生产语境下 **选对默认值与门禁**。

## 阅读顺序建议

1. [横切：仓库、测试与本地开发](./cross-cutting.md)  
2. 语言篇（按需）：[Java](./java.md) · [Python](./python.md) · [Go](./go.md) · [TypeScript](./typescript.md)  
3. 端篇：[服务端](./server-side.md) · [Web](./web.md) · [桌面](./desktop.md) · [移动](./mobile.md)

## 与平台契约的关系

配置外部化、API 兼容、日志字段等统一见 [平台契约](../platform-contracts/README.md)。

## 文档索引

### 横切与语言

| 文档 | 说明 |
|------|------|
| [cross-cutting.md](./cross-cutting.md) | 分支、评审、测试金字塔、本地环境 |
| [java.md](./java.md) | JVM 生态与 Spring 系常见默认 |
| [python.md](./python.md) | 解释器、依赖锁、ASGI/WSGI |
| [go.md](./go.md) | 模块、静态分析、并发模型 |
| [typescript.md](./typescript.md) | 前后端 TS、构建与类型门禁 |

### 端

| 文档 | 说明 |
|------|------|
| [server-side.md](./server-side.md) | API、幂等、任务队列 |
| [web.md](./web.md) | CSR/SSR、CDN、前端安全 |
| [desktop.md](./desktop.md) | Electron/Tauri、更新 |
| [mobile.md](./mobile.md) | 原生/跨端、签名与兼容 |
