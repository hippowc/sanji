# 场景与开源技术对照（工程交付）

下列列出各工程场景中 **业界常用、活跃维护的开源项目**，便于与云平台托管服务或商业产品对标选型。标注 **「本库 Star 索引」** 的条目已在 [`toolbox/repos/`](../repos/README.md) 中按主题收录（可随时同步你的 GitHub Star）。

若你希望 **「围绕一个核心（例如 PostgreSQL）叠一层层最佳实践组件」** 的端到端范式（类似 Supabase 的组合哲学），请优先阅读 **[场景化参考技术栈（stacks）](./stacks/README.md)**；本文件偏向 **按能力类目快速查零件**。

> 说明：开源 ≠ 免费运维；自托管需承担补丁、备份与高可用。最小生产可优先托管，再以开源组件填补缺口。

---

## 1. 开发与本地工具链

| 场景 | 常见开源 | 备注 |
|------|----------|------|
| 容器与本地编排 | [Docker](https://github.com/moby/moby)、[Compose](https://github.com/docker/compose) | 本地依赖一键起 |
| 开发容器规范 | [Dev Containers](https://github.com/devcontainers/spec) | IDE 统一工具链 |
| Java 构建 | [Maven](https://github.com/apache/maven)、[Gradle](https://github.com/gradle/gradle) | 见 [开发·Java](./development/java.md) |
| Java 质量 | [SpotBugs](https://github.com/spotbugs/spotbugs)、[Error Prone](https://github.com/google/error-prone) | 静态分析 |
| Java 测试 | [JUnit 5](https://github.com/junit-team/junit5)、[Testcontainers](https://github.com/testcontainers/testcontainers-java) | 集成测试 |
| Python 测试/格式 | [pytest](https://github.com/pytest-dev/pytest)、[Ruff](https://github.com/astral-sh/ruff) | |
| Go 工具链 | [golangci-lint](https://github.com/golangci/golangci-lint)、[govulncheck](https://go.googlesource.com/vuln/) | |
| 前端工具 | [Vite](https://github.com/vitejs/vite)、[ESLint](https://github.com/eslint/eslint)、[Prettier](https://github.com/prettier/prettier) | |
| API 契约测试 | [Pact](https://github.com/pact-foundation/pact-js)、[Spring Cloud Contract](https://github.com/spring-cloud/spring-cloud-contract) | 多端兼容 |

**本库 Star 索引：** [CLI / 包管理 / 终端](../repos/cli-tooling.md)（`fd`、`ripgrep`、`jq`、`age`、`asdf`、`nvm`、`Homebrew` 等）

---

## 2. CI/CD 与供应链安全

| 场景 | 常见开源 | 备注 |
|------|----------|------|
| 持续集成服务器 | [Jenkins](https://github.com/jenkinsci/jenkins)、[Tekton](https://github.com/tektoncd/pipeline) | 自建流水线内核 |
| GitOps 交付 | [Argo CD](https://github.com/argoproj/argo-cd)、[Flux](https://github.com/fluxcd/flux2) | K8s 声明式发布 |
| 容器镜像构建 | [BuildKit](https://github.com/moby/buildkit)、[Kaniko](https://github.com/GoogleContainerTools/kaniko) | CI 内构建 |
| 制品签名 | [Cosign](https://github.com/sigstore/cosign)（Sigstore） | 供应链可信 |
| 镜像/依赖漏洞扫描 | [Trivy](https://github.com/aquasecurity/trivy)、[Grype](https://github.com/anchore/grype) | 流水线门禁 |
| 静态应用安全测试 | [Semgrep](https://github.com/semgrep/semgrep)、[SpotBugs](https://github.com/spotbugs/spotbugs)（Java） | 按语言选 |

**托管 CI 提示：** GitHub Actions / GitLab CI 等与 OIDC 联邦信任云平台（见 [密钥与身份](./cicd/secrets-identity.md)），可与上表工具组合使用。

**本库索引：** [CI/CD 与 GitOps 开源列表](../repos/cicd-gitops.md)

---

## 3. 运行时、容器与 Kubernetes 生态

| 场景 | 常见开源 | 备注 |
|------|----------|------|
| 容器编排内核 | [Kubernetes](https://github.com/kubernetes/kubernetes) | 托管控制平面常见 |
| 轻量发行版 | [K3s](https://github.com/k3s-io/k3s) | 边缘/小规模 |
| 本地集群 | [minikube](https://github.com/kubernetes/minikube)、[kind](https://github.com/kubernetes-sigs/kind)、[lima-k8s](https://github.com/lima-vm/lima) | 开发/CI |
| 包管理与模板 | [Helm](https://github.com/helm/helm)、[Kustomize](https://github.com/kubernetes-sigs/kustomize) | |
| Ingress / API 网关（开源侧） | [ingress-nginx](https://github.com/kubernetes/ingress-nginx)、[Traefik](https://github.com/traefik/traefik)、[Envoy Gateway](https://github.com/envoyproxy/gateway) | 南北向流量 |
| 证书自动化 | [cert-manager](https://github.com/cert-manager/cert-manager) | TLS 与 Let's Encrypt |
| 密钥同步到集群 | [External Secrets Operator](https://github.com/external-secrets/external-secrets) | 对接云 KMS |

**本库 Star 索引：** [Kubernetes / 本地集群](../repos/kubernetes-infra.md)（含 `k3s`、`minikube`、`lima`、`Kubernetes Handbook`）

---

## 4. 数据、缓存与消息

| 场景 | 常见开源 | 备注 |
|------|----------|------|
| 关系型 OLTP | [PostgreSQL](https://github.com/postgres/postgres)、[MySQL](https://github.com/mysql/mysql-server)、[MariaDB](https://github.com/MariaDB/server) | 生产多用托管 RDS |
| 内存缓存 | [Redis](https://github.com/redis/redis)、[Valkey](https://github.com/valkey-io/valkey)（兼容分支） | 会话、限流、热点读 |
| 消息队列 / 流 | [Apache Kafka](https://github.com/apache/kafka)、[RabbitMQ](https://github.com/rabbitmq/rabbitmq-server)、[NATS](https://github.com/nats-io/nats-server)、[RocketMQ](https://github.com/apache/rocketmq) | 至少一次 + 幂等消费 |
| 对象存储（S3 兼容 API） | [MinIO](https://github.com/minio/minio) | 自建或边缘 |
| 分析型 / OLAP（进程内） | [DuckDB](https://github.com/duckdb/duckdb) | 分析栈补充 |

**本库 Star 索引：** [存储与同步](../repos/storage-backend.md)（`MinIO`、`Syncthing`、`PocketBase`）、[数据 / NLP](../repos/data-nlp.md)（含 `DuckDB`、`Scrapy`）

---

## 5. 网络、Ingress、服务网格（进阶）

| 场景 | 常见开源 | 备注 |
|------|----------|------|
| Web 服务器 / 自动 HTTPS | [Caddy](https://github.com/caddyserver/caddy) | 小型入口极佳 |
| 反向代理 / 负载均衡 | [HAProxy](https://github.com/haproxy/haproxy)、[Envoy](https://github.com/envoyproxy/envoy) | |
| 内网穿透（慎用合规） | [frp](https://github.com/fatedier/frp) | 开发/救援场景 |
| 服务网格（进阶） | [Istio](https://github.com/istio/istio)、[Linkerd](https://github.com/linkerd/linkerd2) | 多数最小生产可不启用 |
| 策略即代码（进阶） | [Open Policy Agent](https://github.com/open-policy-agent/opa) | |

**本库 Star 索引：** [网络 / 代理 / Web](../repos/networking-proxy.md)（含 `Caddy`、`frp`、`searxng`）

---

## 6. 身份、密钥与策略（自托管选项）

| 场景 | 常见开源 | 备注 |
|------|----------|------|
| 密钥与加密管理 | [Vault](https://github.com/hashicorp/vault)（BUSL 许可需注意）、[OpenBao](https://github.com/openbao/openbao)（社区分支） | 替代方案：云托管 Secrets Manager |
| 配置加密入库 | [SOPS](https://github.com/getsops/sops)、[Mozilla SOPS age](https://github.com/getsops/sops) | GitOps 密文 |
| OIDC / OAuth 授权服务器 | [Keycloak](https://github.com/keycloak/keycloak)、[ORY Hydra](https://github.com/ory/hydra) | 统一登录 |

---

## 7. 可观测性（指标 / 日志 / 链路）

| 场景 | 常见开源 | 备注 |
|------|----------|------|
| 指标与告警 | [Prometheus](https://github.com/prometheus/prometheus)、[VictoriaMetrics](https://github.com/VictoriaMetrics/VictoriaMetrics) | 长期存储可用 VM / Thanos / Mimir |
| 可视化 | [Grafana](https://github.com/grafana/grafana) | 仪表盘与告警 UI |
| 日志栈 | [Loki](https://github.com/grafana/loki)、[OpenSearch](https://github.com/opensearch-project/OpenSearch)、[Vector](https://github.com/vectordotdev/vector) | 采集与索引成本需治理 |
| 链路追踪 | [Jaeger](https://github.com/jaegertracing/jaeger)、[Tempo](https://github.com/grafana/tempo) | 配合 OTel |
| 统一采集与导出 | [OpenTelemetry Collector](https://github.com/open-telemetry/opentelemetry-collector) | 厂商中立 |

详见本卷 [可观测性](./observability/README.md)。

**本库索引：** [可观测性开源列表](../repos/observability.md)

---

## 8. 运维自动化与基础设施即代码

| 场景 | 常见开源 | 备注 |
|------|----------|------|
| 基础设施声明 | [Terraform](https://github.com/hashicorp/terraform)、[OpenTofu](https://github.com/opentofu/opentofu) | 多云模板 |
| 配置收敛 | [Ansible](https://github.com/ansible/ansible) | VM 场景常见 |

---

## 9. API、网关与 BFF（开源侧）

| 场景 | 常见开源 | 备注 |
|------|----------|------|
| API 网关 | [Kong](https://github.com/Kong/kong)、[Apache APISIX](https://github.com/apache/apisix) | 限流、认证、路由 |
| gRPC 桥 HTTP | [grpc-gateway](https://github.com/grpc-ecosystem/grpc-gateway) | |

详见 [API 形态与 BFF](./data/api-and-bff.md)。

---

## 10. 移动端与桌面（工具链 / 框架）

| 场景 | 常见开源 | 备注 |
|------|----------|------|
| 移动自动化构建 | [Fastlane](https://github.com/fastlane/fastlane) | iOS/Android 发布脚本 |
| 跨平台 UI | [Flutter](https://github.com/flutter/flutter)、[React Native](https://github.com/facebook/react-native) | 与团队栈匹配 |
| 桌面 Web 壳 | [Tauri](https://github.com/tauri-apps/tauri)、[Electron](https://github.com/electron/electron)（开源运行时） | |

**本库 Star 索引：** [前端 / 桌面 / Web](../repos/frontend-desktop-web.md)（含 `Wails`、`Godot`、`Ant Design`、`Hugo` 等）

---

## 维护方式

- **扩充 Star：** 在 [`repos/`](../repos/README.md) 对应主题 `.md` 增加条目后，可在本表「本库 Star 索引」列补齐链接。  
- **与正文同步：** 各卷 `README` 已链到本页；若正文章节调整，请同步检查上表分类。
