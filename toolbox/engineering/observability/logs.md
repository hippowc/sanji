# 日志

## 1. 结构化

推荐使用 **JSON** 一行一条，字段示例：

| 字段 | 说明 |
|------|------|
| `timestamp` | ISO8601 |
| `level` | ERROR/WARN/INFO/DEBUG |
| `message` | 人类可读摘要 |
| `logger` | 分类 |
| `trace_id` | 与链路追踪对齐 |
| `request_id` | 网关或边缘生成 |
| `service` | 服务名 |
| `user_id` | 业务 ID（注意脱敏与合规） |

## 2. 采集路径

- **容器**：stdout/stderr → 节点 Agent → 托管日志服务。  
- **VM**：Filebeat / Fluent Bit 等价物。  
- **敏感**：密码、token、完整信用卡号 **禁止** 落日志；必要时掩码。

## 3. 保留与成本

- **生产**：满足合规最短保留期；错误日志可更长。  
- **采样**：极高 QPS 路径可对 DEBUG 采样；ERROR 不全采样丢弃。  
- **索引**：按服务与时间分区；冷门检索走冷存储。

## 4. 查询习惯

- **关联**：从告警中的 `trace_id`/`request_id` 一键跳转。  
- **仪表盘**：Top N 错误消息聚合（注意 cardinality 爆炸）。

## 相关链接

- [链路追踪](./tracing.md)
