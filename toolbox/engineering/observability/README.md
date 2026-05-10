# 可观测性与应急响应

> **状态：** 骨架提纲。

## 本文目标

覆盖 **日志、指标、链路追踪与告警 Runbook**，支撑最小生产中的故障发现与定位。

## 文档索引

| 文档 | 说明 |
|------|------|
| [日志](./logs.md) | 结构化、采集、保留与成本 |
| [指标与 SLO](./metrics-slo.md) | RED/USE、SLI/SLO、告警入门 |
| [链路追踪](./tracing.md) | 何时引入、与日志关联 |
| [告警与 Runbook](./alerting-runbooks.md) | 降噪、值班、演练 |

## 建议撰写要点（总）

- 与 [平台契约](../platform-contracts/config-and-secrets.md) 中的 `trace_id` 约定一致。
- **托管 vs 自建**：Prometheus/Grafana 系与云托管监控的对照维度。

## 相关链接

- [运维：变更与回滚](../operations/change-rollback.md)
