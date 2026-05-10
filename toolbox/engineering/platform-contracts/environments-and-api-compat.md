# 环境晋升与 API 兼容

> **状态：** 骨架提纲。

## 本文目标

定义 **dev → staging → prod** 晋升规则，以及 **API 向后兼容** 对移动端（长版本周期）的特殊约束。

## 建议撰写要点

- **环境对齐**：staging 尽量逼近 prod（网络拓扑可简化，数据脱敏）。
- **数据库迁移顺序**：与 [数据库迁移与发布](../cicd/db-migrations-and-release.md) 互链。
- **API 版本**：路径版本 / Header / 契约测试；废弃策略与时间窗。
- **移动端**：强制升级 vs 兼容多版本后端；契约测试在流水线中的位置。

## 相关链接

- [移动端构建与发布](../cicd/mobile-build-release.md)
- [API 形态与 BFF](../data/api-and-bff.md)
