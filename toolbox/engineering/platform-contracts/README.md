# 平台契约与工程约定

「契约」指团队 **默认遵守** 的一组约束：配置如何分级、密钥如何托管、环境如何晋升、日志如何关联、API 如何保证多端兼容。契约写得清楚，可减少 CI、运行时与客户端之间的隐性耦合。

## 文档索引

| 文档 | 内容 |
|------|------|
| [配置、密钥与十二因子实践](./config-and-secrets.md) | 环境变量、密钥管理、反模式 |
| [环境晋升与 API 兼容](./environments-and-api-compat.md) | dev/stage/prod、移动端兼容 |

## 与其它卷的交叉点

- CI 侧密钥：[密钥与身份（OIDC）](../cicd/secrets-identity.md)
- 运行时注入配置：[运行时](../runtime/README.md)
- 观测字段：`trace_id` / `request_id` 约定见 [日志](../observability/logs.md)
