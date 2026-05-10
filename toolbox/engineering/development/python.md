# Python

## 1. 解释器与版本策略

- 生产明确 **minor 版本**（如 3.11、3.12）；CI 与生产一致。  
- 避免隐式依赖系统 Python；容器内使用 **固定基础镜像**。

## 2. 依赖与环境隔离

| 方案 | 说明 |
|------|------|
| **venv + pip-tools** | `requirements.in` → 编译出锁定 `requirements.txt` |
| **Poetry / PDM / uv** | 一体化依赖与打包；注意 lockfile 提交 |

**原则：** lockfile **提交 Git**；构建使用 `--no-deps` 或等价防止漂移。

## 3. Web 与并发模型

| 模型 | 典型栈 | 适用 |
|------|--------|------|
| **WSGI** | Gunicorn + Django/Flask sync | CPU 密集少、模型简单 |
| **ASGI** | Uvicorn/Hypercorn + FastAPI/Starlette | IO 密集、WebSocket |

注意：**异步路由中禁止阻塞调用**（同步 DB 客户端），否则吞没事件循环。

## 4. 代码质量

- **格式化**：Ruff（含 import 排序）或 Black。  
- **类型**：mypy 或 pyright；CI 门禁级别按团队设定（可先 warn 后 error）。  
- **测试**：pytest；覆盖率阈值可按模块递增。

## 5. 与数据层

- **ORM**：SQLAlchemy 2.x、Django ORM 等；避免 N+1（`selectinload` 等）。  
- **连接池**：与实例规格匹配；容器并发数 × workers 估算总连接数。

## 6. 打包与容器

- **多阶段构建**：builder 安装依赖 → runtime 仅拷贝 venv/site-packages。  
- **进程模型**：每容器 **单进程单应用** + 外层 replicas；或 Gunicorn workers 明确数量。

## 7. 观测

- **结构化日志**：`structlog` 或标准 logging JSON formatter。  
- **指标**：Prometheus client；OpenTelemetry Python SDK 统一 traces。

## 相关链接

- [服务端](./server-side.md)
- [CI/CD](../cicd/README.md)
