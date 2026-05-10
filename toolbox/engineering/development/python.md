# Python

> **状态：** 骨架提纲。

## 本文目标

Python 在 **服务端与自动化** 场景下的最小生产工程化清单与选型维度。

## 建议撰写要点

- **解释器版本策略**、虚拟环境与依赖锁定（pip-tools、Poetry、uv 等择要对照）。
- **Web**：WSGI/ASGI、典型框架快速对比维度（并发模型、生态）。
- **类型检查与格式化**：mypy、ruff/black 等在三件套中的位置。
- **测试**：pytest、覆盖率门禁。
- **打包与部署**：容器入口、多阶段构建、gunicorn/uvicorn 与进程模型。
- **性能剖析**：cProfile、线上采样概要。

## 相关链接

- [服务端](./server-side.md)
- [CI/CD](../cicd/README.md)
