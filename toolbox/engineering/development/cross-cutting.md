# 横切：仓库、测试与本地开发

## 1. 仓库与分支

常见策略（择一并与团队规模匹配）：

| 模式 | 特点 | 适用 |
|------|------|------|
| **主干开发（Trunk-Based）** | 短生命周期分支，频繁合并主干 | 流水线成熟、特性开关完善 |
| **Git Flow 变体** | `develop` / `release` / `hotfix` | 发布节奏较慢、需并行多版本 |

**合并门禁建议：** 至少 1 人 Code Review；主干保护禁止 force push；必须通过 CI。

## 2. 文档与决策记录

- **README**：如何本地启动、环境变量说明、常用命令。  
- **CHANGELOG**：面向使用方与运维的版本说明（可与语义化版本配合）。  
- **ADR（Architecture Decision Record）**：记录重大选型背景、备选方案与权衡；适合放在 [`articles/scenes/engineering`](../../../articles/scenes/engineering/README.md)。

## 3. 测试分层（金字塔）

```
        /\
       /E2E\        ← 少量、关键路径、慢、脆弱
      /------\
     / 集成   \      ← API、数据库、消息：Testcontainers 等
    /----------\
   /   单元测试  \   ← 快、多、确定性高
  /--------------\
```

| 层级 | 目标 | CI 中的位置 |
|------|------|-------------|
| 单元 | 函数/类正确性 | 每次提交 |
| 集成 | 组件协作、真实依赖替身或容器 | 合并请求 |
| E2E | 用户旅程 | nightly 或发布前 |

**契约测试**：服务端与移动端/Web 之间维护 API 契约，防止破坏性变更 silently 上线（见 [环境晋升与 API 兼容](../platform-contracts/environments-and-api-compat.md)）。

## 4. 本地开发环境

### 4.1 推荐组合

- **Docker Compose**：编排本地 Postgres、Redis、消息队列等；与生产拓扑 **形似** 即可。  
- **Dev Container**：统一编辑器内工具链版本（JDK、Node、Python），降低「在我机器能跑」。  
- **种子数据**：`fixtures` 或迁移脚本；生产数据 **禁止** 直接导入开发机（脱敏例外流程）。

### 4.2 本地与云的责任边界

| 内容 | 本地 | 云上 staging/prod |
|------|------|-------------------|
| 配置 | `.env` + `.env.example` | 托管配置与 Secret |
| 数据库 | 容器内实例或云开发实例 | 托管 RDS + 备份 |
| 身份 | 测试用户、Mock OIDC | 真实 IAM 与工作负载身份 |

## 5. 供应链安全（入门）

- 依赖 **锁文件** 提交仓库；PR 中展示依赖差异。  
- CI 运行 **漏洞扫描**（语言生态工具或第三方）；高危项阻断或限时豁免流程。  
- 私有依赖使用 **制品仓库代理**，避免构建时直连不稳定外部源。

## 相关链接

- [CI/CD：流水线](../cicd/pipeline-and-artifacts.md)
- [Java](./java.md) · [Python](./python.md) · [Go](./go.md) · [TypeScript](./typescript.md)
