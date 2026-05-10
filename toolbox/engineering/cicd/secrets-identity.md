# 密钥与身份（OIDC）

## 1. 问题陈述

传统做法把云平台 **长期 Access Key** 存进 CI Secret，风险包括：

- Secret 泄露即 **长期有效**。  
- 多仓库共享同一密钥，无法细粒度追责。  
- 轮换痛苦导致「数年不换」。

## 2. 推荐模式：OIDC 联邦信任

**思路：** CI 平台生成短期 OIDC Token → 云平台验证签发者与 audience → 颁发 **临时云凭证**（STS AssumeRole 等价物）。

| 组件 | 说明 |
|------|------|
| **IdP** | GitHub/GitLab 等 |
| **Audience / Subject** | 限制为特定 org/repo/environment |
| **IAM Role** | 信任策略仅允许上述 subject |

**效果：** 仓库侧 **无需静态云密钥**；凭证自动过期。

## 3. 权限边界

- **CI 构建角色**：拉代码、推镜像、上传扫描报告；**不能** broad `AdministratorAccess`。  
- **CD 部署角色**：仅能操作约定命名空间或资源标签；生产部署可强制 **人工审批（manual gate）**。  
- **与运行时分离**：Pod/VM 使用 **工作负载身份**（IRSA、Workload Identity 等），勿复用 CI 角色。

## 4. 密钥托管的补充场景

- **第三方 API**：仍用 Secret Manager；CI 仅读取部署所需子集。  
- **签名**：移动端证书解密密钥短时注入 Job，结束后销毁内存副本。

## 5. 多云抽象

不同云厂商名词不同，思想一致：**联邦身份 + 短期凭证 + 最小权限策略**。落地时对照各云「OpenID Connect / Workload Identity Federation」文档。

## 相关链接

- [IAM 与密钥](../network-security/iam-secrets.md)
- [配置与密钥](../platform-contracts/config-and-secrets.md)
