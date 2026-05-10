# 数据与中间件

本卷覆盖最小生产中常见的 **事务存储、缓存、消息、对象存储** 以及 **API 形态与 BFF**。默认 **托管优先**；自建仅在合规或成本奇点出现时讨论。

## 文档索引

| 文档 | 内容 |
|------|------|
| [关系型与 OLTP](./oltp.md) | RDS 类服务、连接池、备份 |
| [缓存（Redis）](./cache.md) | 场景、一致性、故障模式 |
| [消息与异步](./messaging.md) | 队列与流、幂等 |
| [对象存储](./object-storage.md) | 静态资源、生命周期 |
| [API 形态与 BFF](./api-and-bff.md) | REST/GraphQL/gRPC、BFF |

## 相关链接

- [数据库迁移](../cicd/db-migrations-and-release.md)
- [备份恢复](../operations/backup-restore.md)
