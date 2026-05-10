# repos — 仓库索引

来自 GitHub Star 的整理（账号：`hippowc`），按主题拆分；条目格式：**仓库链接 + 简要说明**。

**与工程知识体系对照：** 若希望按「场景」浏览业界常用开源栈并与本索引联动，见 [`../engineering/oss-landscape.md`](../engineering/oss-landscape.md)。

**同步说明：** 初次写入于 2026-05；日后可在本地用 GitHub API 对照更新。

## 主题索引

| 文件 | 内容 |
|------|------|
| [ai-agents-llm.md](ai-agents-llm.md) | AI / Agent / LLM 框架与终端编程助手 |
| [media-generation.md](media-generation.md) | 图像与视频生成、扩散模型工具链 |
| [cli-tooling.md](cli-tooling.md) | 终端工具、包管理与版本管理 |
| [networking-proxy.md](networking-proxy.md) | 网络、代理、Web 服务、元搜索 |
| [storage-backend.md](storage-backend.md) | 同步、对象存储、轻量后端 |
| [kubernetes-infra.md](kubernetes-infra.md) | Kubernetes、本地集群、虚拟机 |
| [cicd-gitops.md](cicd-gitops.md) | CI/CD、GitOps、镜像构建与供应链安全（开源索引） |
| [observability.md](observability.md) | 指标、日志、链路、OpenTelemetry（开源索引） |
| [frontend-desktop-web.md](frontend-desktop-web.md) | 前端 UI、桌面/Web 框架、静态站、游戏与可视化 |
| [data-nlp.md](data-nlp.md) | 数据、爬虫、中文 NLP、分析型数据库 |
| [jvm-java-kotlin.md](jvm-java-kotlin.md) | JVM、Java 诊断、网络框架、Kotlin |
| [media-streaming-bench.md](media-streaming-bench.md) | 音视频、串流、压测、兼容层 |
| [learning-resources.md](learning-resources.md) | 教程与综合学习资源 |

## 更新 Star 列表（参考）

```bash
curl -sS "https://api.github.com/users/hippowc/starred?per_page=100" \
  | jq -r '.[] | "\(.full_name)\t\(.description // "")"'
```
