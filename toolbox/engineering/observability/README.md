# 可观测性与应急响应

可观测性（Observability）通过 **日志、指标、链路** 三类信号帮助推断系统内部状态；再配合 **告警与 Runbook** 形成闭环。最小生产不要求一上来全套顶配，但 **日志 + 核心指标 + 症状告警** 属于底线（参见 [最小生产](../overview/minimal-production.md)）。

## 文档索引

| 文档 | 内容 |
|------|------|
| [日志](./logs.md) | 结构化、采集、保留 |
| [指标与 SLO](./metrics-slo.md) | RED、SLI/SLO |
| [链路追踪](./tracing.md) | 采样与关联 |
| [告警与 Runbook](./alerting-runbooks.md) | 降噪与演练 |

## 相关链接

- [平台契约：日志字段](../platform-contracts/config-and-secrets.md)
- [变更与回滚](../operations/change-rollback.md)
