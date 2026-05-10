# Web 前端

## 1. 渲染形态选型

| 形态 | 优点 | 代价 |
|------|------|------|
| **CSR（SPA）** | 交互丰富；CDN 静态托管简单 | 首屏与 SEO；需额外 SSR 若要强 SEO |
| **SSR** | 首屏快、SEO 友好 | 服务端复杂度、TTFB 与缓存策略 |
| **边缘渲染 / ISR** | 全球延迟优化 | 厂商绑定度、失效策略 |

**最小生产：** CSR + 托管静态站点 + API 分离 是最常见起步；内容型站点再评估 SSR。

## 2. 构建与产物

- **指纹静态资源**：长期缓存 `immutable`。  
- **Source Map**：生产可上传至监控平台 **不对外暴露**。  
- **Bundle 分析**：定期 `rollup-plugin-visualizer` / webpack analyzer，控制 vendor 体积。

## 3. 环境变量与安全

- **浏览器可见的任何配置均不可信**：视为公开。  
- **密钥**：仅在服务端（BFF/SSR）使用；客户端调用的 API 使用 **短期令牌** 或 **OAuth PKCE** 等模式。

## 4. 前端可观测

- **Real User Monitoring（RUM）**：Core Web Vitals、JS 错误聚合。  
- **API 错误**：与 `request_id` 关联，便于对照服务端日志。

## 5. 安全基线

- **CSP（Content-Security-Policy）**：渐进收紧；先 report-only。  
- **依赖漏洞**：与 CI 扫描联动；高危 transitive dependency 升级路径评估。  
- **第三方脚本**：最小化；供应链攻击面。

## 6. CDN 与缓存

- HTML **短缓存** 或不缓存；静态资源 **长缓存**。  
- **API** 缓存谨慎：鉴权与用户相关内容默认 **私有**。

## 相关链接

- [TypeScript](./typescript.md)
- [TLS 与 WAF](../network-security/tls-waf-ddos.md)
