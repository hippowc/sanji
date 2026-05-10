# 移动客户端（Android / iOS）

## 1. 技术路线对比

| 路线 | 优点 | 代价 |
|------|------|------|
| **原生（Kotlin/Swift）** | 性能与平台 API 最全 | 双端人力 |
| **Flutter** | 一致 UI、高性能渲染 | Dart 栈；复杂平台通道 |
| **React Native** | JS/TS 生态、热更新潜力 | 原生桥接调试成本 |

**选型：** 团队技能 > 动画与图形需求 > 第三方 SDK 依赖程度。

## 2. 版本与兼容

- **语义化版本**：`MAJOR.MINOR.PATCH`；`build number` 单调递增（商店要求）。  
- **API 契约**：假设 **多版本 App 并存**；后端 [兼容策略](../platform-contracts/environments-and-api-compat.md) 必须同步产品节奏。  
- **强制升级**：仅用于安全或协议断裂；需商店审核与应用内提示预案。

## 3. 构建与签名

| 平台 | 要点 |
|------|------|
| **Android** | Keystore / Play App Signing；AAB 上架 |
| **iOS** | 证书 + Provisioning Profile；自动化需 Apple API Key |

**密钥：** 构建机密不进仓库；CI 使用加密 Secret 或 KMS 解密短时可用。

## 4. 分发与流水线

- **内测**：Firebase App Distribution、TestFlight、企业签名（合规前提下）。  
- **商店**：Google Play / App Store **API 提交自动化** 各厂商差异大；预留人工兜底窗口。  
详见 [移动端构建与发布](../cicd/mobile-build-release.md)。

## 5. 网络与安全

- **证书绑定（Certificate Pinning）**：防中间人；注意轮换与故障降级策略。  
- **本地存储**：敏感数据 Keychain / Keystore；避免明文 SharedPreferences。

## 6. 可观测与合规

- **崩溃与性能**：Firebase Crashlytics、Sentry、自建 OTel（注意采样）。  
- **隐私**：个人信息保护法、GDPR、应用商店隐私问卷；第三方 SDK 清单审计。

## 相关链接

- [API 形态与 BFF](../data/api-and-bff.md)
- [环境晋升与 API 兼容](../platform-contracts/environments-and-api-compat.md)
