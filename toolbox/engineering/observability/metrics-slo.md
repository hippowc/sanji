# 指标与 SLO

> **状态：** 骨架提纲。

## 本文目标

介绍 **RED/USE**、**SLI/SLO** 与最小告警集合，并与公有云托管监控对齐思路。

## 建议撰写要点

- **RED**：Rate、Errors、Duration 适用于请求驱动服务。
- **USE**：Utilization、Saturation、Errors 适用于资源层。
- **SLI 选型**：可用性、延迟、错误率；错误预算概念。
- **告警**：对用户有影响的症状告警优于底层噪声。
- **仪表盘**：最小集合：流量、错误率、延迟分位数、饱和度。

## 相关链接

- [术语表](../overview/glossary.md)
