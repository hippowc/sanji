# CI/CD：构建、测试与发布

> **状态：** 骨架提纲。

## 本文目标

覆盖从提交到上线的 **流水线阶段、制品、测试门禁、密钥身份、数据库迁移与发布协同**，以及 **移动端** 的特殊环节。

## 文档索引

| 文档 | 说明 |
|------|------|
| [流水线与制品](./pipeline-and-artifacts.md) | 阶段模型、缓存、不可变制品 |
| [密钥与身份（OIDC）](./secrets-identity.md) | 无长期云密钥、Workload Identity |
| [数据库迁移与发布协同](./db-migrations-and-release.md) | 迁移顺序、向后兼容 |
| [移动端构建与发布](./mobile-build-release.md) | 构建号、签名、商店自动化概要 |

## 建议撰写要点（总）

- **托管 CI** vs **自建 Runner** 的选型维度（成本、隔离、合规）。
- **安全门禁**：SAST、依赖漏洞、许可证（按需）在流水线中的位置。
- 与 [平台契约](../platform-contracts/README.md)、[运行时](../runtime/README.md) 互链。

## 相关链接

- [开发横切](../development/cross-cutting.md)
- [网络：IAM](../network-security/iam-secrets.md)
