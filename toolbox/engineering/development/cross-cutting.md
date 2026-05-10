# 横切：仓库、测试与本地开发

> **状态：** 骨架提纲。

## 本文目标

描述与语言无关的 **仓库治理、分支策略、测试分层与本地开发环境**，作为四语言与四端的共同前置。

## 建议撰写要点

- **分支与评审**：主干开发 / GitFlow 变体选型；合并门禁最小集。
- **测试金字塔**：单测、契约测试、少量 E2E；何时引入负载测试（指向运维卷）。
- **本地开发**：Docker Compose / devcontainer；本地数据库与缓存；种子数据与隐私。
- **文档**：README、CHANGELOG、架构决策记录（ADR）与 [`articles/scenes/engineering`](../../../articles/scenes/engineering/README.md) 的配合方式。

## 相关链接

- [平台契约](../platform-contracts/README.md)
- [CI/CD 流水线](../cicd/pipeline-and-artifacts.md)
