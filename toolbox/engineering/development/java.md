# Java

## 1. 运行时与发行版

- 优先选择 **LTS** 版本线（如 17、21）；团队统一 minor 升级节奏。  
- **发行版**：Eclipse Temurin、Amazon Corretto、Azul Zulu 等；生产与 CI 使用同一 lineage，避免行为差异。  
- **容器镜像**：使用官方或加固的基础镜像；注意 **CVE 扫描** 与定期重建。

## 2. 构建与依赖

| 工具 | 说明 |
|------|------|
| **Maven** | 约定优于配置；多模块常见 |
| **Gradle** | 灵活；Kotlin DSL 流行 |

- 使用 **依赖锁**（Maven `dependencyManagement` + 版本钉扎；Gradle 版本目录）。  
- CI 中启用 **`mvn verify` / `gradle check`**，包含测试与静态检查。

## 3. 代码质量与静态分析

建议组合（可按团队裁剪）：

- **格式化**：Spotless、Google Java Format 等。  
- **Bug 模式**：SpotBugs / Error Prone。  
- **风格**：Checkstyle。  
- **空安全/合约**：Optional、Bean Validation（`jakarta.validation`）。

## 4. 测试

- **JUnit 5** + AssertJ（或 Hamcrest）。  
- **集成测试**：Testcontainers 启动真实 Postgres/Redis/Kafka 等，贴近生产。  
- **契约测试**：Spring Cloud Contract 或 Pact（与移动端/Web 对接时）。

## 5. Web 与服务框架（常见）

| 场景 | 常见选择 | 备注 |
|------|----------|------|
| 同步 REST | Spring Boot + Spring MVC | 生态成熟；注意启动时间与原生镜像 |
| 响应式 | Spring WebFlux | 背压与事件循环模型不同，团队需统一认知 |
| 微服务配套 | Spring Cloud 系列 | 配置中心、客户端负载均衡等按需取用 |

**健康检查：** 提供 `/live` 与 `/ready`（或平台约定路径），区分进程存活与依赖就绪。

## 6. 性能与观测

- **JVM 参数**：堆大小、GC 选择（G1/ZGC 等）在 staging 压测后定型；生产避免调试型 GC 日志洪流。  
- **指标**：Micrometer + Prometheus 端点或 OTel。  
- **剖析**：Async Profiler、JFR（需谨慎开启采样频率）。

## 7. 打包与部署

- **Fat JAR** 或 **分层镜像**（Spring Boot layered jar）加速镜像构建。  
- **优雅关停**：处理 SIGTERM，完成在途请求再退出（配合 K8s `terminationGracePeriodSeconds`）。

## 相关链接

- [服务端](./server-side.md)
- [JVM 仓库索引](../../repos/jvm-java-kotlin.md)
