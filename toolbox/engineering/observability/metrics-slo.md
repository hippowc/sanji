# 指标与 SLO

## 1. RED 方法（请求驱动服务）

| 信号 | 指标示例 |
|------|----------|
| Rate | `http_server_requests_total` QPS |
| Errors | 5xx 比例、业务失败码比例 |
| Duration | P50/P95/P99 延迟 |

## 2. USE 方法（资源）

| 信号 | 示例 |
|------|------|
| Utilization | CPU、内存、磁盘使用率 |
| Saturation | 队列深度、线程池排队 |
| Errors | 磁盘 IO 错误、TCP 重传升高 |

## 3. SLI / SLO 入门

1. 选择 **用户能感知** 的 SLI（如「成功下单占比」「首页加载 <2s 占比」）。  
2. 定义 **测量窗口**（滚动 30 天常见）。  
3. 设定 **SLO 目标**（如 99.9%）。  
4. 计算 **错误预算**：剩余预算多则允许更多发布/重构实验。

## 4. 告警原则

- **症状优先**：用户可见故障 > 底层噪声。  
- **分位数**： latency 用 **histogram + SLO 区间**，勿仅盯平均值。  
- **基数**：避免高 cardinality label（如每个 user_id 一条时间序列）。

## 5. 托管 vs 自建

- **托管监控**：低运维；厂商锁定与查询语言成本。  
- **Prometheus + Grafana**：云中立；需自行运维可用性与长期存储。

## 相关链接

- [术语表](../overview/glossary.md)
