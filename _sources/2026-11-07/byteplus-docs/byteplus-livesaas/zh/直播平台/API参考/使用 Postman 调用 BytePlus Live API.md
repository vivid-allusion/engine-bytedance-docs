---
title: "使用 Postman 调用 BytePlus Live API"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-using-postman-to-call-byteplus-live-apis-zh-CN"
---

要测试和调试 BytePlus Live API，你可以使用流行的 API 客户端 Postman。本指南提供了逐步操作说明，帮助你分叉官方集合、配置认证头，并发送你的首个请求。

<span id="prerequisites"></span>
## 前提条件


* 一个 Postman 账号。

* 一个 BytePlus 账号。更多信息，请参见[注册 BytePlus 账号](https://docs.byteplus.com/en/byteplus-platform/docs/signing-up-your-account)。

* AccessKey ID（AK）和 Secret Access Key（SK）。要获取这些信息，请前往[BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/) \> **用户信息** \> **IAM** \> **密钥管理**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/36d6e087508a4a61914ea025d4158706~tplv-goo7wpa0wc-image.image) </span>


<span id="context"></span>
## 背景

Postman 提供了用户友好的界面用于发送 API 请求，并允许你轻松检查和分析返回调用结果。它支持多种请求方式，包括 GET、POST、PUT 和 DELETE，并允许你为请求添加头部、参数及其他数据。凭借其强大的功能和直观的界面，Postman 已成为 API 开发和测试的重要工具。

<span id="procedure"></span>
## 操作流程


1. 可使用 Postman 的在线或离线版本。

   * Postman 在线版本：登录[Postman 在线平台](https://www.postman.com/livesaas/workspace/byteplus-live/overview)。点击左侧的**BytePlus Live Open API**，然后点击**Fork**，将 BytePlus Live 集合分叉到你的工作区。你必须分叉该集合，因为目前无法从公共工作区发送请求。关于如何创建分叉的更多信息，请参见[Creating a fork](https://docs.byteplus.com/docs/byteplus-livesaas/docs-using-postman-to-call-byteplus-live-apis-zh-CN#creating-a-fork)。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6ae8dcfea7534baf9fbb01edfc310152~tplv-goo7wpa0wc-image.image) </span>

   * Postman 离线版本：点击**Import**，并选择以下文件。

      [openapi-call-example.postman_collection.json](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eed499b8cade40f6ad95d12aa5b36727~tplv-goo7wpa0wc-image.image)

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4d93480913664f6c9e15b3d1aa00ef44~tplv-goo7wpa0wc-image.image) </span>

2. 点击**查看更多操作**图标并选择**Duplicate**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a8c95d7e5c2c4d24a49e9054805f730a~tplv-goo7wpa0wc-image.image) </span>

3. 根据需要更改 API 名称、请求方式、请求 URI、查询参数和请求体参数。更多信息，请参见你要调用的 API 的相关文档。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f521e8d41bab40858db6b4da32fd6674~tplv-goo7wpa0wc-image.image) </span>

4. 在**Headers**标签页，将`AccessKey`和`SecretKey`的值替换为你在[Prerequisites](https://docs.byteplus.com/docs/byteplus-livesaas/docs-using-postman-to-call-byteplus-live-apis-zh-CN#152c47a4)部分获得的密钥。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7b6869ae77ac4b169f829fe5806c1692~tplv-goo7wpa0wc-image.image) </span>

5. 点击**Send**发送请求。

6. 在页面底部查看返回调用结果。


<span id="troubleshooting"></span>
## 故障排查

如果返回调用结果出现错误，请参见[通用错误及状态码](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-error-and-status-codes)获取更多信息。

为避免常见错误，请确保满足以下要求：


* AK 和 SK 与[Prerequisites](https://docs.byteplus.com/docs/byteplus-livesaas/docs-using-postman-to-call-byteplus-live-apis-zh-CN#152c47a4)部分获得的密钥一致。

* 已添加所有必需参数。

* 添加的参数及其对应值均正确。

* 请求方式和请求 URI 均正确。


如果问题仍然存在，请联系你的销售代表寻求帮助。如果你没有销售代表，请点击[此处](https://www.byteplus.com/en/contact)填写联系表单，BytePlus 销售团队成员将与你跟进。
