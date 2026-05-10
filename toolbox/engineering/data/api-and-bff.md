# API 形态与 BFF

> **状态：** 骨架提纲。

## 本文目标

对比 **REST、GraphQL、gRPC** 等的适用边界，并说明 **BFF（面向客户端的后端）** 在移动端/Web 并存时的典型用法。

## 建议撰写要点

- **REST**：缓存友好、简单 CRUD；过度聚合时的痛点。
- **GraphQL**：聚合与按需字段；N+1 与治理成本。
- **gRPC**：内部服务高效通信；浏览器侧限制（网关）。
- **BFF**：减少往返、协议转换、鉴权聚合；避免业务逻辑泄露到 UI。
- **契约测试**：与 [环境晋升](../platform-contracts/environments-and-api-compat.md) 互链。

## 相关链接

- [移动客户端](../development/mobile.md)
