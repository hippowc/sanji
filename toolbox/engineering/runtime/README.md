# 运行时：部署形态与演进

运行时回答：**工作负载放在何种计算抽象上**、如何伸缩、如何接入流量与配置。本卷按 **从小到大** 描述公有云常见路径，并单独讨论 **托管 Kubernetes** 的引入时机。

## 文档索引

| 文档 | 内容 |
|------|------|
| [从小到大演进路径](./evolution-path.md) | PaaS、Serverless 容器、VM、K8s |
| [托管 Kubernetes 何时值得](./kubernetes.md) | 触发条件与最低认知集合 |

## 原则

- **匹配团队运维半径**：抽象层级越高，自定义空间越小，运维负担越低。  
- **与服务网格解耦**：多数最小生产不需要网格；需要时再引入。

## 开源生态参考

- **场景对照表：** [场景与开源技术对照 §3](../oss-landscape.md)（Kubernetes、Helm、ingress-nginx、cert-manager 等）  
- **本库 Star：** [Kubernetes / 本地集群](../../repos/kubernetes-infra.md)

## 相关链接

- [网络拓扑](../network-security/network-exposure.md)
- [可观测性](../observability/README.md)
