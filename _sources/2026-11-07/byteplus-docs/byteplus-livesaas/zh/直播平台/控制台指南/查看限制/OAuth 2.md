---
title: "OAuth 2"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-oauth-2-0-zh-CN"
---

为了限制对你的直播间的访问并实现单点登录体验，你可以将 OAuth 2.0 配置为观看限制。此方法要求观众在观看视频或发送评论前，先登录你的用户账号系统。本指南提供了设置 BytePlus Live 直播间 OAuth 2.0 集成的概念背景和分步操作说明。

<span id="prerequisites"></span>
## 前提条件


* 你必须拥有 BytePlus 账号或具备 Producer \> Edit 权限的 IAM 用户。有关如何添加 IAM 用户的更多信息，请参见 [管理用户、组织和角色](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles-zh-CN)。

* 请联系你的销售代表获取重定向 URI。如果你没有销售代表，请点击 [here](https://www.byteplus.com/en/contact) 填写表单，以便 BytePlus 销售团队稍后与你联系。

* 在你的用户账号系统中完成 BytePlus Live 的注册。注册过程中需要提供重定向 URI。注册完成后，将生成 client ID 和 client secret，用于识别 BytePlus Live。


<span id="context"></span>
## 背景

OAuth 2.0 是一种开放且标准化的授权协议，允许第三方应用通过令牌访问用户资源，无需用户名和密码。在本主题中，第三方应用指的是 BytePlus Live。

OAuth 2.0 定义了以下四种获取令牌的授权方式：授权码模式、隐式模式、密码模式和客户端凭证模式。BytePlus Live 使用授权码模式，该模式首先请求授权码，然后将其兑换为访问令牌。在所有授权方式中，该模式提供最高级别的安全性。有关该授权方式的更多信息，请参见 [OAuth 2](https://docs.byteplus.com/docs/byteplus-livesaas/docs-oauth-2-0-zh-CN)。

<span id="process"></span>
## 流程

通过授权码模式，BytePlus Live 可以从你的账号系统获取用户数据。详细流程如下。

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e67a4a4a707e43cfa8a71c364a22bca8~tplv-goo7wpa0wc-image.image) </span>


1. 用户通过链接或二维码访问 BytePlus Live 的观看页。

2. BytePlus Live 向你的授权服务器请求授权码，并向授权服务器提供 client ID 和 scope。用户被重定向至你的用户账号系统的登录页。

3. 用户登录你的用户账号系统后，授权服务器将授权码返回给 BytePlus Live。用户被重定向至销售代表提供的重定向 URI。

4. BytePlus Live 使用 client ID 和 client secret 进行身份验证，并利用授权码向你的授权服务器请求访问令牌。

5. 授权服务器验证 BytePlus Live 的身份和授权码。验证成功后，授权服务器向 BytePlus Live 发放访问令牌。

6. BytePlus Live 向你的资源服务器请求受保护的用户数据，并提供访问令牌进行身份验证。

7. 资源服务器验证访问令牌。验证成功后，资源服务器将用户数据提供给 BytePlus Live。

* 如果采用非标准 OAuth 2.0 登录模式，授权服务器在第 5 步发放访问令牌时，会将受保护的用户数据返回给 BytePlus Live。

* 如果用户的浏览器已存储你自有账号系统的登录状态，在 BytePlus Live 请求授权码后，资源所有者会直接将授权码返回给 BytePlus Live，无需用户再次登录。


<span id="procedure"></span>
## 操作流程


1. 登录 [BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)。

2. 在直播间列表中，点击打开一个直播间。

3. 在左侧导航栏，点击 **Producer** \> **观看限制**。

4. 将认证类型设置为 **OAuth2.0**，并完成以下配置。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/02cf75b685284b28982255c0eb737495~tplv-goo7wpa0wc-image.image) </span>

   
   |参数名称 |接口行为 |
   |---|---|
   |登录平台名称 |你自有账号系统的平台名称。建议填写英文名称。 |
   |Redirect URI |用于接收授权码的回调 URL。此 URL 必须与你用户账号系统中为 BytePlus Live 应用配置的 URL 保持一致。 |
   |Authorization 端点 |用于获取授权码的 URL。 |
   |Token 端点 |用于获取访问令牌的 URL。 |
   |UserInfo 端点 |选择 **URL** 或 **标识字段**。<br><br><br>* **URL**：输入用于获取用户信息的 URL。<br><br>* **标识字段**：输入用于解析用户信息的标识字段。如采用非标准 OAuth 2.0 登录模式，请选择此选项。当授权服务器向 BytePlus Live 下发访问令牌时，BytePlus Live 可获取受保护的用户数据。 |
   |用户名字段 |对应你用户账号系统中用户名的字段，用于提取用户名。<br><br>为防止个人信息泄露，请勿在自有账号系统中使用手机号等信息作为用户名。 |
   |用户 ID 字段 |对应你用户账号系统中用户 ID 的字段，用于提取用户 ID。<br><br>为防止个人信息泄露，请勿在自有账号系统中使用手机号等信息作为用户 ID。 |
   |Client id |用于标识 BytePlus Live 的客户端 ID，在 BytePlus Live 注册到你的自有账号系统后生成。 |
   |Client secret |用于标识 BytePlus Live 的客户端密钥，在 BytePlus Live 注册到你的自有账号系统后生成。 |
   |Scope |授权范围。BytePlus Live 只能访问指定范围内的资源。<br><br>如果你的自有账号系统中 `Scope` 没有默认值，则此参数为必填项。 |
   |试看 |启用此选项并选择时长。在试看时长内，观众无需登录直播间即可观看直播视频或回放。 |
