---
title: "BytePlus Live API 入门"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getting-started-with-byteplus-live-api-zh-CN"
---

BytePlus Live API 是基于 HTTP 的 RESTful API，采用签名算法进行身份验证。API 请求和返回调用结果的主体均采用 JSON 格式。本主题将引导你完成调用 BytePlus Live API 的流程。


1. 了解限制与配额

2. 注册账号

3. 完成身份验证

4. 首次调用 API


<span id="understanding-limits-and-quotas"></span>
## 了解限制与配额

每个 API 对每个账号 ID 的调用频率限制为每分钟 120 次（除非另有说明）。

<span id="signing-up-for-an-account"></span>
## 注册账号

在调用 BytePlus Live API 之前，请按照 [注册 BytePlus 账号](https://docs.byteplus.com/en/byteplus-platform/docs/signing-up-your-account) 的说明注册账号。

你可以使用 BytePlus 账号或具有特定权限的 IAM 用户调用 API。例如，若要使用 IAM 用户调用 [UpdateHostAccount](https://docs.byteplus.com/en/docs/byteplus-livesaas/updatehostaccount) 以添加或更新主播账号，该 IAM 用户必须具备 **营销工具包** \> **编辑** 权限。关于如何添加 IAM 用户，详见 [管理用户、组织和角色](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles-zh-CN)。

<span id="completing-authentication"></span>
## 完成身份验证

BytePlus Live API 的身份验证会对 API 请求进行签名，以验证你的身份并防止请求在传输过程中被恶意拦截。更多信息，请参见 [API 认证](https://docs.byteplus.com/docs/byteplus-livesaas/docs-API-authentication-zh-CN)。

进行 API 身份验证时，请使用发起调用账号（即 BytePlus 账号或 IAM 用户）的 Access Key ID 和 Secret Access Key。

<span id="making-your-first-call"></span>
## 首次调用 API

BytePlus Live API 对请求结构有特定要求。更多信息，请参见 [API HTTP请求](https://docs.byteplus.com/docs/byteplus-livesaas/docs-api-http-request-zh-CN)。
