# 软件工程与云平台交付 — 知识体系

面向在 **公有云** 上落地 **最小生产（Minimal Production）** 的体系化参考：覆盖平台契约、开发、CI/CD、运行时、数据、网络与安全、可观测与运维。叙述语言为 **中文**；产品名、CLI、RFC 与代码标识保留常用英文。

**维护说明：** 技术栈与托管服务名称会随云厂商迭代而变化；正文强调 **能力与选型维度**，具体控制台路径请以当前官方文档为准。

## 适用读者与边界

- **读者**：能为团队搭建或评审端到端交付链路的工程师、Tech Lead、具备基础云平台操作能力的一线开发者。
- **公有云假设**：优先使用 **托管 VPC、负载均衡、托管数据库、托管密钥与监控**；多云之间用「能力类型」对标（如「托管 Kubernetes」「托管关系型数据库」），不绑定单一厂商控制台截图。
- **非目标**：大数据数仓与实时计算平台建设、完整 FinOps 体系、特定语言的从零语法教程、通过某项厂商认证的全考点覆盖。

## 阅读路线

1. [总纲与最小生产](./overview/README.md) — 底线定义与术语
2. [平台契约](./platform-contracts/README.md) — 配置、密钥、环境、API 兼容
3. [网络与安全基线](./network-security/README.md) — VPC、IAM、TLS、边界防护
4. [运行时](./runtime/README.md) + [数据](./data/README.md) — 计算形态与状态存储
5. [CI/CD](./cicd/README.md) — 从提交到发布的工程化闭环
6. [可观测性](./observability/README.md) + [运维与成本](./operations/README.md)
7. [开发](./development/README.md) — Java / Python / Go / TypeScript 与多端实践（篇幅最长，可按需选读）

个人落地、拓扑与 ADR 建议写在 [`articles/scenes/engineering`](../../articles/scenes/engineering/README.md)，本目录保持 **可复用的通用参考**。

## 各卷索引

| 卷 | 路径 |
|----|------|
| 总纲 | [overview/](overview/README.md) |
| 平台契约 | [platform-contracts/](platform-contracts/README.md) |
| 开发 | [development/](development/README.md) |
| CI/CD | [cicd/](cicd/README.md) |
| 运行时 | [runtime/](runtime/README.md) |
| 数据 | [data/](data/README.md) |
| 网络与安全 | [network-security/](network-security/README.md) |
| 可观测性 | [observability/](observability/README.md) |
| 运维与成本 | [operations/](operations/README.md) |

## 与工具箱其它目录的关系

- 开源仓库索引：[repos/](../repos/README.md)
- 语言与库的补充条目：[languages/](../languages/README.md)、[libraries/](../libraries/README.md)、[services/](../services/README.md)
