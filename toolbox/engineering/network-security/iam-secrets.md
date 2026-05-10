# IAM 与密钥

## 1. 身份类型

| 主体 | 用途 |
|------|------|
| 人类用户 | 控制台与 CLI；应 MFA |
| CI 工作流 | OIDC 联邦角色（见 [CI 文档](../cicd/secrets-identity.md)） |
| 工作负载 | Pod/VM 附加的角色（IRSA、Workload Identity） |
| 运行时服务账号 | 应用访问云 API（如读写 Secret Manager） |

## 2. 最小权限

- **策略**：按资源 ARN、Tag、前缀限定；禁止 `Action:* Resource:*` 出现在应用角色。  
- **分离**：部署角色 ≠ 运行角色 ≠ DBA 人类角色。  
- **Break-glass**：紧急管理员账号禁用日常使用；启用需审批与告警。

## 3. 密钥生命周期

- **轮换**：数据库口令、签名证书、API Key；自动化优先。  
- **存储**：KMS 加密 Secret；读取审计。  
- **泄漏响应**：立即作废、复盘、扫描 Git 历史（git-secrets、trufflehog）。

## 4. 审计

- **云平台审计日志**：开启保留与告警（如 `Delete*`、`PutBucketPolicy`）。  
- **应用层审计**：敏感操作写 append-only 日志。

## 相关链接

- [配置与密钥](../platform-contracts/config-and-secrets.md)
