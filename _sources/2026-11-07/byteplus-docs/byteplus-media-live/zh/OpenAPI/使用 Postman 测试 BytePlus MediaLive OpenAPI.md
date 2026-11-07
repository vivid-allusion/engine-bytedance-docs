---
title: "使用 Postman 测试 BytePlus MediaLive OpenAPI"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-using-postman-to-test-the-byteplus-medialive-openapi-zh-CN"
---

要快速测试 BytePlus MediaLive OpenAPI，可以使用官方的 Postman 集合。本主题提供了逐步操作说明，指导你如何将该集合分叉到你的工作区，配置认证凭证（AK/SK），并发送示例 API 请求。

<span id="ee247ee9"></span>
## 前提条件


* 一个 Postman 账号。

* 一个 BytePlus 账号。更多信息，请参见[注册 BytePlus 账号](https://docs.byteplus.com/en/byteplus-platform/docs/signing-up-your-account)。

* [开通 BytePlus MediaLive 服务](https://docs.byteplus.com/en/byteplus-media-live/docs/getting-started#da5a6a63)。

* 服务已开启后，登录[BytePlus 控制台](https://console.byteplus.com/)，点击页面右上角的账号名称，然后选择**IAM** \> **密钥管理**，获取账号的 Access Key ID（AK）和 Secret Access Key（SK），用于 API 请求认证。


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7f6dc1b6f2bc466785242136a7995c07~tplv-goo7wpa0wc-image.image) </span>

<span id="f11782de"></span>
## 操作步骤


1. 登录[Postman 在线平台](https://www.postman.com/byteplus-medialive-docs/workspace/byteplus-medialive)。

2. 在左侧点击**BytePlus MediaLive OpenAPI**，再点击**Fork**，将整个集合分叉到你自己的工作区。


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4c6064319e6e44f982725c3f053fcbff~tplv-goo7wpa0wc-image.image) </span>


3. 在你的工作区中，选择 DescribeDomain API，然后点击**Headers**标签页。

4. 将**Headers**标签页中的 AK 和 SK 替换为你在[前提条件](https://docs.byteplus.com/docs/byteplus-media-live/docs-using-postman-to-test-the-byteplus-medialive-openapi#Prerequisites)中获取的 AK 和 SK。

5. 点击**Body**标签页，在`DomainList`中将域名替换为你自己的域名。

6. 点击**Send**发送请求。


你可以在页面底部查看返回调用结果。
