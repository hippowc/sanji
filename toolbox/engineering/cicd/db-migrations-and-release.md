# 数据库迁移与发布协同

## 1. 核心矛盾

应用发布 **快**，数据库 schema 变更 **慢且往往不可逆**。需要 **兼容多版本代码并存** 一段时间。

## 2. 扩展-收缩（Expand-Contract）模式（概念）

典型三步：

1. **Expand**：新增列/表/索引；旧代码忽略；新代码 **双写或读新写旧**（按场景）。  
2. **Migrate**：数据回填；切换读路径到新结构。  
3. **Contract**：删除旧列/约束；仅当 **无旧版本实例** 时再执行。

移动端长周期下，**Contract** 往往滞后数个后端版本。

## 3. 迁移工具

| 生态 | 工具示例 |
|------|----------|
| JVM | Flyway、Liquibase |
| Python | Alembic（SQLAlchemy）、Django migrations |
| Go | golang-migrate、Atlas |
| Node | Knex、Prisma migrate |

**原则：** 迁移脚本 **版本有序**、可审计；禁止在手环境里手工改 prod schema 而不回补脚本。

## 4. 执行时机

| 方式 | 说明 |
|------|------|
| **Job 前置** | 部署前单独 Job；失败则阻断 rollout |
| **Init Container** | 首批 Pod 执行迁移（注意并发锁） |
| **独立流水线** | DBA 管控；与应用发布节奏分离（强合规团队） |

需 **分布式锁** 或迁移工具内置锁，防止双实例同时 migrate。

## 5. 回滚策略

- **应用回滚** 不一定能伴随 **schema 回滚**（删列危险）。  
- 预案：**向前修复（roll forward）** 新迁移修补；或 **保留兼容列** 直至窗口结束。  
- 重大变更前 **备份快照**（见 [备份恢复](../operations/backup-restore.md)）。

## 6. 与 API 兼容

新增必填字段前：旧客户端是否崩溃？默认值？服务端是否接受「缺省」？

## 相关链接

- [关系型与 OLTP](../data/oltp.md)
- [变更与回滚](../operations/change-rollback.md)
