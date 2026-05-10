# Java

> **状态：** 骨架提纲。

## 本文目标

Java 在 **服务端** 场景下的最小生产工程化清单与典型技术栈 **选型维度**。

## 建议撰写要点

- **JDK 发行版与 LTS**、构建工具（Maven / Gradle）。
- **依赖与漏洞扫描**在 CI 中的位置。
- **格式化与静态分析**（Checkstyle、SpotBugs、Nullness 等择要）。
- **测试**：JUnit、Testcontainers 用于集成测试的边界。
- **打包**：容器镜像与 JVM 参数基线（内存、GC 日志开关与可观测对接）。
- **框架**：Spring Boot 等为代表时的默认起步项与健康检查端点。

## 相关链接

- [服务端](./server-side.md)
- [JVM 相关仓库索引](../../repos/jvm-java-kotlin.md)
