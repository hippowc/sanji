# 移动客户端（Android / iOS）

> **状态：** 骨架提纲。

## 本文目标

移动端在最小生产中的 **构建、签名、分发、版本兼容与流水线** 要点；强调长客户端周期下的 **API 契约**。

## 建议撰写要点

- **工程选型维度**：原生 vs Flutter vs React Native 等（维护成本、生态、性能权衡）。
- **签名与证书**：调试 / 发布、密钥保管（不进库）。
- **分发**：应用商店与内测渠道（TestFlight、内部 APK 等概念层）。
- **版本策略**：强制升级、灰度发布（应用内）、与后端 API 兼容窗口。
- **流水线**：与 [移动端构建与发布](../cicd/mobile-build-release.md) 对齐。
- **可观测**：崩溃报告、性能采样与用户隐私合规概要。

## 相关链接

- [环境晋升与 API 兼容](../platform-contracts/environments-and-api-compat.md)
- [API 与 BFF](../data/api-and-bff.md)
