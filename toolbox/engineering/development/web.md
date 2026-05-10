# Web 前端

> **状态：** 骨架提纲。

## 本文目标

Web 端在公有云最小生产中的 **构建、部署形态（静态托管 vs SSR）与环境变量** 要点。

## 建议撰写要点

- **CSR / SSR / 边缘渲染** 选型维度与成本。
- **环境变量**：构建期注入 vs 运行时注入；避免密钥进浏览器。
- **前端可观测**：Real User Monitoring 与错误上报接入点（与可观测卷互链）。
- **缓存与 CDN**：静态资源指纹、失效策略概要。
- **安全**：CSP、依赖漏洞与供应链。

## 相关链接

- [TypeScript](./typescript.md)
- [网络：TLS 与 WAF](../network-security/tls-waf-ddos.md)
