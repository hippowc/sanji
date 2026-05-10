# 托管 Kubernetes 何时值得

## 1. 价值主张

托管 Kubernetes 在一个平台上统一：

- **多服务** 的交付单元（Deployment）。  
- **配置与密钥**（ConfigMap / Secret + 外部 Secret Operator）。  
- **流量入口**（Ingress / Gateway API）。  
- **弹性**（HPA、cluster autoscaler）。  
- **可观测** hook（DaemonSet 采集、Sidecar）。

若你现在只有 **单个 API + 单个数据库**，多数云的 **托管容器服务（无需自建控制平面认知）** 可能更划算。

## 2. 何时「值得」

| 信号 | 说明 |
|------|------|
| 服务数量 | 多个独立发布单元，脚本编排乏力 |
| 团队 | 有人能消化 kube-api、RBAC、网络策略 |
| 频率 | 每日多次发布，需要标准化滚动/金丝雀 |
| 弹性 | CPU/内存水位-driven 扩缩成为常态 |
| 生态 | 需要 Operator（Kafka、Es 等）统一管理 |

## 3. 何时「不急」

- 单体应用 + 垂直扩容仍充足。  
- 团队无任何 Kubernetes 经验且无平台支持。  
- 可被 **函数计算 / Serverless 容器** 覆盖的突发任务型负载。

## 4. 最低认知集合（入职培训大纲）

| 概念 | 用途 |
|------|------|
| Pod | 调度原子 |
| Deployment | 无状态副本集与滚动更新 |
| Service | 集群内负载均衡与 DNS |
| Ingress / Gateway | 南北向 HTTP(S) 路由 |
| ConfigMap / Secret | 配置注入 |
| Resource requests/limits | 调度与 QoS |
| Liveness / Readiness | 探针 |
| HPA | 水平伸缩 |
| Namespace | 软隔离与 RBAC 边界 |

## 5. 默认不建议的早期组件

- **服务网格全链 mTLS**：运维与排障成本高；多数业务先用 **应用层 TLS + 网络策略** 足够。  
- **过于复杂的 GitOps 多层封装**：先跑通一条清晰路径再分层。

## 相关链接

- [网络暴露](../network-security/network-exposure.md)
- [工具箱：Kubernetes 索引](../../repos/kubernetes-infra.md)
