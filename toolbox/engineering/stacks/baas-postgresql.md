# 参考栈：以 PostgreSQL 为核心的 BaaS（后端即服务）

本文描述一类常见范式：**以 PostgreSQL 为唯一权威数据源（System of Record）**，在其上叠加「自动 API、身份、网关、实时、对象存储、边缘函数」等能力，快速交付移动 / Web 应用的后端。  

[Supabase](https://github.com/supabase/supabase) 是该范式的著名 **开源一体化发行版**：把多个成熟开源项目 **按职责缝合**，并提供控制台与客户端 SDK。下文先抽象 **能力分层与选型**，再对照 Supabase 的整合方式，最后给出 **自建组合** 路径。

---

## 1. 场景定义

### 1.1 适合解决的问题

- 产品早期需要 **鉴权用户 + CRUD + 少量服务端逻辑**，团队不想从零搭全套后端。  
- 希望 **关系模型 + SQL + 事务** 仍是真相来源（相对某些文档型 BaaS）。  
- 需要 **实时推送**（列表订阅、协同草稿等）与 **对象存储**（头像、附件）在同一套账户体系下。

### 1.2 非目标

- 极复杂领域规则、长事务工作流（更适合独立领域服务 + 事件驱动）。  
- 全球多活强一致（需单独做单元化 / CRDT 等架构）。  
- 替代数据仓库与离线分析（应另建 OLAP 管道）。

---

## 2. 为什么核心是 PostgreSQL

| 理由 | 说明 |
|------|------|
| 模型表达力 | 关系 + JSONB + 全文检索扩展，覆盖多数业务建模 |
| 生态 | 扩展（PostGIS、pgvector…）、逻辑复制、逻辑解码（实时）、成熟运维工具 |
| 许可与托管 | OSS + 各云托管 RDS；Exit 路径清晰 |
| 「API 自动生成」基础 | 约束、视图、Row Level Security（RLS）可与 **行级权限** 模型结合 |

**要点：** BaaS 不是「只要一个 API」，而是 **在数据库层落实权限与数据边界**（RLS + policy），网关与 JWT 声明协同——Supabase 的推广路径即建立在此思想上。

---

## 3. 能力分层：从内核到边缘

下列为一类 **逻辑分层**；实际部署可合并进程或使用网关统一入口。

```
                    ┌───────────── 客户端 SDK / BFF ─────────────┐
                    ▼                                          │
              ┌──────────┐    ┌─────────────┐    ┌────────────┐ │
              │ API 网关  │───▶│ 自动 REST   │───▶│ PostgreSQL │ │
              │ (路由/限流)│    │ / GraphQL   │    │  + RLS     │ │
              └──────────┘    └─────────────┘    └────────────┘ │
                    │                │                  ▲         │
                    │         ┌────┴────┐             │ 逻辑解码 │
                    │         │ 身份 IdP │─────────────┘         │
                    │         │ JWT/OIDC │                       │
                    │         └─────────┘                       │
                    │                │                           │
                    ▼                ▼                           │
              ┌──────────┐    ┌─────────────┐                    │
              │ 实时通道  │    │ 对象存储 API │                    │
              │ (订阅/WAL)│    │ (S3 兼容)   │                    │
              └──────────┘    └─────────────┘                    │
                    │                │                           │
                    └────────┬───────┘                           │
                             ▼                                   │
                    ┌─────────────────┐                          │
                    │ 边缘函数 / 业务钩子 │◀─────────────────────┘
                    │（慎用：保持薄逻辑）│
                    └─────────────────┘
```

---

## 4. 各层：开源选型与职责

### 4.1 数据访问层：从数据库「长」出 API

| 方案 | 特点 | 典型项目 |
|------|------|----------|
| **REST 自动生成** | 强依赖 PG schema / 视图 / RLS；适合表格型 CRUD | [PostgREST](https://github.com/PostgREST/postgrest) |
| **GraphQL 引擎** | 模型映射 + 订阅；运维与查询复杂度更高 | [Hasura](https://github.com/hasura/graphql-engine) |
| **手写 ORM API** | 灵活；失去「纯声明式」速度 | Spring / Django / Prisma 等服务 |

**实践：** 若走 PostgREST 路线，把 **权限写进数据库策略（RLS）** 比在每个 Handler 里散落判断更一致。

### 4.2 身份与访问（IdP）

| 方案 | 特点 |
|------|------|
| **专用 Auth 服务** | 邮箱/第三方 OAuth、JWT 签发、用户表与 PG 同步 | Supabase **GoTrue**、[Ory](https://github.com/ory) 栈、[Keycloak](https://github.com/keycloak/keycloak) |
| **外包 IdP** | Auth0、Clerk、云厂商 Cognito 等 | 快；注意供应商锁定与数据驻留 |

JWT 中的 `role`、`user_id` 声明需与 **PostgREST / RLS** 使用的角色映射一致。

### 4.3 API 网关

| 方案 | 特点 |
|------|------|
| **Kong** | 插件生态（鉴权、限流、日志）；Supabase 历史组件之一 |
| **Traefik / Envoy Gateway** | 云原生Ingress常见 |
| **云托管 API 网关** | 与 WAF、IAM 集成省事 |

职责：**TLS 终结、路由、限流、把匿名流量挡在业务逻辑之前**。

### 4.4 实时（Realtime）

常见实现思路：

- **逻辑复制 / WAL** → 专用实时服务推 WebSocket（Supabase Realtime 一类）。  
- **GraphQL Subscriptions**（Hasura）。  
- **轻量场景**：`LISTEN/NOTIFY`（吞吐有限）。

选型看：**延迟、扇出规模、是否需要过滤与权限**。

### 4.5 对象存储

- **S3 API 兼容**：MinIO、Garage、Ceph RGW；或直接用云厂商 OSS。  
- 与 **用户身份** 绑定：预签名 URL、Bucket 策略、或经 BaaS Storage API 统一授权。

**本库索引：** [存储与同步](../../repos/storage-backend.md)（含 `MinIO` 等你已 Star 的仓库）。

### 4.6 边缘函数 / Serverless 钩子

用于 **薄逻辑**（Webhook、转换、权限二次校验），避免把 BaaS 写成「大泥球单体」。

| 方向 | 示例 |
|------|------|
| WASM / Isolate | Deno、WasmEdge 等运行时 |
| Knative / OpenFaaS | K8s 上函数服务 |

**原则：** 复杂规则下沉到 **独立服务** 或 **数据库侧约束**，函数层保持可测试、可限制资源。

### 4.7 开发者体验（控制台 / Studio）

一体化发行版的价值往往在 **Schema 管理、RLS 可视化、日志、密钥轮换**——自建可用：

- 管理 UI：自建 Admin、或复用开源 Dashboard（按栈搭配）。

---

## 5. Supabase：一体化映射（理解「组合」）

Supabase 的思路可概括为：**用 Postgres 作核心，把各层最好的开源之一接进来**（具体组件随版本演进，以官方仓库为准）：

| 能力 | 常见对应开源 / 角色 |
|------|---------------------|
| 数据库 | PostgreSQL |
| 自动 REST | PostgREST |
| 身份 | GoTrue（Auth） |
| 网关 / 路由 | Kong 等（历史架构常见） |
| 实时 | Realtime 服务（订阅 WAL / replication） |
| 存储 | S3 兼容存储抽象 + API |
| 边缘函数 | Deno 类隔离运行时 |
| 客户端 SDK | 多语言，封装 Auth + DB + Realtime |

**定位：** 你若认同「Postgres 为中心 + 分层开源」，Supabase 是 **少决策成本的默认答案**；若要 **深度定制或多云合规**，则按第 4 节 **拆模块自建**。

---

## 6. 其他一体化 / 半一体化路径（对照）

| 项目 | 核心 / 特点 | 备注 |
|------|-------------|------|
| [Appwrite](https://github.com/appwrite/appwrite) | 自带数据库抽象与多运行时 | 非「PG 唯一核心」范式，但同属 BaaS |
| [Hasura](https://github.com/hasura/graphql-engine) | GraphQL + PG | 强实时与权限模型需学习曲线 |
| [PocketBase](https://github.com/pocketbase/pocketbase) | 单文件、SQLite、内置 Admin | 极简与小团队；与「PG 核心」路径不同但场景重叠 |

**本库 Star：** [存储 / 后端](../../repos/storage-backend.md) 含 `PocketBase`、`MinIO`。

---

## 7. 自建「PG 核心 BaaS」的最小积木（示例配方）

> 仅供架构讨论；生产需补全监控、备份、多实例与高可用。

| 层级 | 选型示例 |
|------|----------|
| DB | 托管 RDS PostgreSQL + 启用 RLS |
| REST | PostgREST |
| Auth | Keycloak 或 Ory（或外包 IdP） |
| 网关 | Kong 或云 ALB + API Gateway |
| 实时 | 自研订阅服务读逻辑解码，或先用 Hasura 取代 REST+订阅 |
| 存储 | MinIO + 预签名 |
| 函数 | Knative Serving（已在 K8s） |

---

## 8. 最小生产与本栈特有风险

- **RLS 策略错误** 可导致跨租户数据暴露 —— 必须有 **自动化策略测试** 与 staging 数据脱敏验证。  
- **PostgREST 暴露面**：禁止默认超级用户角色直连；使用受限 DB 角色。  
- **实时通道**：注意订阅风暴与授权校验（每条订阅是否绑定 JWT）。  
- **对象存储**：Bucket 公开读列表、错误 ACL 是高频事故。

更多通用底线见 [最小生产定义](../overview/minimal-production.md) 与 [数据卷：API 与 BFF](../data/api-and-bff.md)。

---

## 9. 延伸阅读（本知识库内）

- [关系型与 OLTP](../data/oltp.md)  
- [对象存储](../data/object-storage.md)  
- [API 形态与 BFF](../data/api-and-bff.md)  
- [IAM 与密钥](../network-security/iam-secrets.md)  
- [场景开源总表：数据类](../oss-landscape.md)  

---

## 10. 后续可追加的栈（占位）

若你认可这一写法，可按相同模板继续添加例如：

- 「事件驱动 + Kafka 核心」的微服务平台  
- 「ClickHouse / DuckDB 核心」的分析型产品后台  
- 「Timescale / PG」的时序与监控数据栈  

需要时可直接复制 [stacks/README.md](./README.md) 中的模板起稿。
