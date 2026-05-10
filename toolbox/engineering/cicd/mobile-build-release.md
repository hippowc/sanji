# 移动端构建与发布

## 1. 版本号策略

| 概念 | Android | iOS |
|------|---------|-----|
| 用户可见版本 | `versionName`（如 2.3.1） | `CFBundleShortVersionString` |
| 单调递增构建号 | `versionCode` | `CFBundleVersion` |

**规则：** 上架提交 **构建号必须递增**；与后端 API **协商废弃窗口** 时在 Release Note 同步。

## 2. 流水线阶段（典型）

```
检出 → 依赖安装 → 静态检查/单测 → 构建 Debug/Release → 签名 → 归档产物 → （可选）上传分发/商店 API
```

- **缓存**：Gradle / CocoaPods / SPM 缓存加速。  
- **矩阵**：多 flavor（渠道包）注意 **合规**（权限声明一致）。

## 3. 签名与机密

- **Android**：Upload key → Play App Signing；CI 保存加密 keystore 或使用托管签名。  
- **iOS**：Fastlane match 或 Xcode Cloud；API Key（Issuer ID + Key ID + p8）权限最小化。

**禁止：** 私钥明文进仓库；旋转周期写入 Runbook。

## 4. 分发渠道

| 渠道 | 用途 |
|------|------|
| 内测 | Firebase App Distribution、TestFlight、蒲公英类 |
| 正式 | Play Store、App Store |

商店 API **自动化提交** 能力随政策变化；保留人工上传兜底。

## 5. 合规与元数据

- **隐私清单**：第三方 SDK 披露（鸿蒙/Android/iOS 各自要求）。  
- **权限**：最小权限原则；敏感权限需运行时说明文案。

## 相关链接

- [移动客户端](../development/mobile.md)
