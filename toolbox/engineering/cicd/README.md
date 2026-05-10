# CI/CD：构建、测试与发布

持续集成（CI）回答「合并是否安全」；持续交付（CD）回答「变更如何 **可控地** 抵达生产」。本卷按 **流水线阶段、制品、身份、迁移与多端** 组织，默认托管 CI（GitHub Actions、GitLab CI、云厂商流水线等概念等价）。

## 文档索引

| 文档 | 内容 |
|------|------|
| [流水线与制品](./pipeline-and-artifacts.md) | 阶段模型、缓存、晋级 |
| [密钥与身份（OIDC）](./secrets-identity.md) | 无长期云密钥 |
| [数据库迁移与发布协同](./db-migrations-and-release.md) | 迁移顺序与回滚 |
| [移动端构建与发布](./mobile-build-release.md) | Android/iOS 特有条目 |

## 原则

1. **同一流水线产物晋级** dev → staging → prod，避免「每个环境各自构建」。  
2. **自动化优先**：重复手工步骤是故障源。  
3. **权限最小**：CI 仅能部署到指定环境资源。

## 开源生态参考

- **场景对照表：** [场景与开源技术对照 §2](../oss-landscape.md)（Jenkins、Tekton、Argo CD、Trivy、Cosign 等）  
- **本库索引：** [CI/CD / GitOps 开源列表](../../repos/cicd-gitops.md)；亦可搭配 [Kubernetes](../../repos/kubernetes-infra.md)、[网络 / 入口](../../repos/networking-proxy.md)

## 相关链接

- [开发横切](../development/cross-cutting.md)
- [变更与回滚](../operations/change-rollback.md)
