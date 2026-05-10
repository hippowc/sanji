# 托管 Kubernetes 何时值得

> **状态：** 骨架提纲。

## 本文目标

说明 **托管 K8s（如 ACK/EKS/GKE）** 的收益与成本，避免过早采用。

## 建议撰写要点

- **值得上的信号**：服务数量、环境复杂度、统一发布需求、团队具备平台运维能力。
- **不值得上的信号**：单服务、低频发布、可被 PaaS 覆盖的全托管路径。
- **最小组件认知**：Deployment、Service、Ingress、ConfigMap/Secret、HPA（概念层）。
- **入口**：托管 Ingress Controller / 网关与 TLS。
- **与服务网格**：默认「可不采用」，列出例外场景。

## 相关链接

- [工具箱 K8s 索引](../../repos/kubernetes-infra.md)
- [网络暴露](../network-security/network-exposure.md)
