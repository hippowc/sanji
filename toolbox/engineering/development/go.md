# Go

## 1. 工具链

- 统一 **Go 版本**（如 1.22+）；`go.mod` 声明 `go` 行版本。  
- 私有模块：`GOPRIVATE`、公司内部模块代理（Athens 等）。

## 2. 模块与构建

- `go mod tidy` 纳入 CI；检查 **伪版本** 与 replace 指令滥用。  
- 构建：`go build -trimpath -ldflags "-s -w"` 减小体积（按是否需要调试符号权衡）。  
- **CVE**：`govulncheck` 扫描标准库与模块已知漏洞。

## 3. 静态分析与风格

- **标配**：`go vet`、`staticcheck`。  
- **格式化**：`gofmt`/`goimports`；CI 校验格式化差异为 0。  
- **Race**：集成测试阶段 `go test -race`（性能开销大，可抽样）。

## 4. HTTP 服务

- **标准库 `net/http`** 足以构建生产服务；框架如 Gin、Echo、Chi 提供路由与中间件糖衣。  
- **优雅退出**：监听 `SIGTERM`，`Shutdown` context 超时；拒绝新请求并完成在途。  
- **超时**：Server、`http.Client`、数据库上下文 **层层设置 deadline**。

## 5. 并发

- Goroutine **泄漏** 与 channel 误用是常见故障源；使用 `context` 传递取消。  
- **worker pool** 限制并发，保护下游。

## 6. 观测

- **`expvar` / pprof**：禁止无条件暴露公网；由认证反向代理或仅 admin 网络访问。  
- **OpenTelemetry**： traces + metrics 统一导出。

## 7. 容器镜像

- **distroless / scratch + CA 证书**：减小攻击面；注意时区与 TLS 根证书捆绑。  
- **非 root 用户** 运行（`USER nonroot`）。

## 相关链接

- [服务端](./server-side.md)
- [CLI 工具索引](../../repos/cli-tooling.md)
