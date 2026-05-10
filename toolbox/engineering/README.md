# 软件工程与云平台交付 — 知识体系（参考）

面向 **公有云上搭一套最小生产（Minimal Production）** 的体系化参考：覆盖交付、运行时、数据、网络与安全、可观测与运维。正文 **中文**；产品名、CLI、API 保留常用英文。

> **状态：** 骨架与提纲已就位；各文件内「建议撰写要点」供后续逐章充实。

## 阅读路线（推荐）

1. [总纲](./overview/README.md) → [最小生产定义](./overview/minimal-production.md)
2. [平台契约](./platform-contracts/README.md)（配置、环境、API 兼容）
3. [网络与安全基线](./network-security/README.md)
4. [运行时](./runtime/README.md) + [数据](./data/README.md)
5. [CI/CD](./cicd/README.md)
6. [可观测性](./observability/README.md) + [运维与成本](./operations/README.md)
7. [开发](./development/README.md)（语言与多端篇幅最大，可在骨架搭好后展开）

## 各卷索引

| 卷 | 路径 | 说明 |
|----|------|------|
| 总纲 | [overview/](overview/README.md) | 边界、假设、术语、最小生产底线 |
| 平台契约 | [platform-contracts/](platform-contracts/README.md) | 配置/密钥、环境晋升、日志与追踪约定、API 版本 |
| 开发 | [development/](development/README.md) | Java/Python/Go/TS；服务端/Web/桌面/移动 |
| CI/CD | [cicd/](cicd/README.md) | 流水线、制品、身份与密钥、迁移与发布、移动端 |
| 运行时 | [runtime/](runtime/README.md) | 从小到大演进、托管 K8s 何时值得 |
| 数据 | [data/](data/README.md) | OLTP、缓存、消息、对象存储、API 形态与 BFF |
| 网络与安全 | [network-security/](network-security/README.md) | VPC、暴露面、IAM、TLS、WAF/限流 |
| 可观测性 | [observability/](observability/README.md) | 日志、指标与 SLO、链路、告警与 Runbook |
| 运维与成本 | [operations/](operations/README.md) | 备份恢复、变更回滚、容量与账单 |

## 与个人笔记的配合

- **本目录**：偏客观参考、选型维度与检查清单。  
- **个人落地与 ADR**：写在 [`articles/scenes/engineering/`](../../articles/scenes/engineering/README.md)，此处用链接互指。

## 与现有 toolbox 的关系

- 具体 **开源仓库** 索引见 [`../repos/`](../repos/README.md)；本体系正文可在表格中引用对应主题文件。
