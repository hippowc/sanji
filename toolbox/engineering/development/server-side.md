# 服务端

> **状态：** 骨架提纲。

## 本文目标

归纳服务端在最小生产中的 **横切能力**：API 设计入口、错误模型、幂等、限流、健康检查与后台任务。

## 建议撰写要点

- **同步 HTTP API** 与 **异步任务**（队列）分工；何时拆服务（指向运行时与数据卷）。
- **幂等键**、重试风暴防护、超时与熔断概念层。
- **健康检查**：liveness / readiness 与负载均衡的关系。
- **BFF**：与 [API 与 BFF](../data/api-and-bff.md) 互链。
- **与四语言文档**：Java/Python/Go/TS 各自展开实现细节。

## 相关链接

- [数据：API 与 BFF](../data/api-and-bff.md)
- [可观测：指标](../observability/metrics-slo.md)
