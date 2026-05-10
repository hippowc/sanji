# 密钥与身份（OIDC）

> **状态：** 骨架提纲。

## 本文目标

说明 CI/CD 与云平台对接时 **避免长期 Access Key** 的推荐模式（OIDC / Workload Identity Federation 等概念层）。

## 建议撰写要点

- **反模式**：把云平台永久密钥存在仓库 Secrets 并多人共享。
- **推荐模式**：OIDC 联邦信任 CI 提供商；短期令牌；最小权限策略绑定到仓库/环境。
- **与运行时区分**：构建身份 ≠ 运行时 Workload 身份；权限边界分开描述。
- **多云**：抽象为「信任 CI → 交换短期云凭证」的共同模式。

## 相关链接

- [IAM 与密钥](../network-security/iam-secrets.md)
- [配置与密钥](../platform-contracts/config-and-secrets.md)
