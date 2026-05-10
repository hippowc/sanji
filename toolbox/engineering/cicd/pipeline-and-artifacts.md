# 流水线与制品

## 1. 推荐阶段模型

```
lint/format → 单元测试 → 构建 → 集成测试 → 安全扫描 → 制品推送 → 部署触发（按环境）
```

| 阶段 | 失败策略 | 说明 |
|------|----------|------|
| 静态检查 | **阻断合并** | 格式、类型、依赖漏洞（阈值可议） |
| 单元测试 | 阻断 | 快速反馈 |
| 构建 | 阻断 | 产出容器镜像或未容器化制品 |
| 集成测试 | 阻断或 nightly | Testcontainers、staging 冒烟 |
| 制品推送 | 阻断 | tag 不可变 |
| 部署 | 人工审批或自动（按风险） | 与环境晋升策略绑定 |

## 2. 缓存与可重现构建

- **依赖缓存**：npm/pnpm、maven、gradle、go module proxy；注意缓存 **失效键** 包含 lockfile hash。  
- **Docker layer cache**：利用构建 Kit；多阶段构建减少最终层。  
- **可重现性**：固定基础镜像 digest（`image@sha256:...`）在安全性要求高场景。

## 3. 制品策略

| 制品类型 | 版本标识 | 存放 |
|----------|----------|------|
| 容器镜像 | `repo:git-sha` + 可选 semver tag | 托管镜像仓库 |
| Helm Chart / Kustomize | Chart version + values | OCI 或 Git |
| 移动端 | `versionName` + `versionCode/build` | 归档存储 + 商店 |

**不可变：** 已标记 `prod` 的 digest **不复用覆盖**；新问题通过新构建修复。

## 4. 部署触发模式

- **GitOps**：合并即声明式变更；控制器调和集群（Argo CD、Flux）。  
- **流水线推送**：CI 调用云平台 API / kubectl apply（需强身份治理）。  
- **Release Train**：固定窗口上车，降低变更叠加。

## 5. 与环境的关系

staging 部署应使用 **生产等价配置维度**（较小规格即可），详见 [环境晋升](../platform-contracts/environments-and-api-compat.md)。

## 相关链接

- [密钥与身份](./secrets-identity.md)
- [运行时演进](../runtime/evolution-path.md)
