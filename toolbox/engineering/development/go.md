# Go

> **状态：** 骨架提纲。

## 本文目标

Go 在 **服务端与 CLI** 场景下的最小生产工程化清单与选型维度。

## 建议撰写要点

- **Go 版本策略**、模块与私有仓库代理。
- **格式化与静态分析**：gofmt、vet、staticcheck、govulncheck。
- **测试**：表驱动测试、race detector 在 CI 中的使用条件。
- **HTTP 服务**：标准库与框架择要；优雅关停（graceful shutdown）。
- **构建**：交叉编译、`-trimpath`、符号与可观测（pprof）。
- **容器**：scratch / distroless 镜像取舍。

## 相关链接

- [服务端](./server-side.md)
- [工具箱 CLI 索引](../../repos/cli-tooling.md)
