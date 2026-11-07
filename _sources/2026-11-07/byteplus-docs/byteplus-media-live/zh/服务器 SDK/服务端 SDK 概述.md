---
title: "服务端 SDK 概述"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-server-sdk-zh-CN"
---

BytePlus MediaLive 提供多种编程语言的服务端 SDK。每个服务端 SDK 都封装了以下能力，帮助你快速调用 BytePlus MediaLive OpenAPI：


* 签名生成，免去你繁琐的计算过程。

* 常用 OpenAPI 操作，包括发送请求和处理返回调用结果。每个 SDK 都提供了相应的代码示例。


<span id="17e2c1c8"></span>
## 获取 Access Key

要使用服务端 SDK，你需先获取 Access Key，该密钥由**Access Key ID**和**Secret Access Key**组成。

泄露主账号的 Access Key 可能带来严重的安全风险。因此，建议你使用子账号的 Access Key。


* 如需使用管理员账号，你需要[获取管理员账号的 Access Key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-an-accesskey#create-an-access-key-through-the-key-management-screen)；

* 如需使用子账号，你需要[获取子账号的 Access Key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-an-accesskey#create-an-access-key-through-the-user-details-screen)。


<span id="SDKs"></span>
## 安装与使用


|**SDK** |**指南** |**源码** |**示例** |
|---|---|---|---|
|Java SDK |[安装 Java SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-java-sdk-zh-CN) |[Java SDK 源码](https://github.com/byteplus-sdk/byteplus-sdk-java) |[Java 示例](https://github.com/byteplus-sdk/byteplus-sdk-java/tree/master/example/src/main/java/com/byteplus/example/live) |
|Go SDK |[安装 Go SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-golang-sdk-zh-CN) |[Go SDK 源码](https://github.com/byteplus-sdk/byteplus-sdk-golang) |[Go 示例](https://github.com/byteplus-sdk/byteplus-sdk-golang/tree/master/example/demo_live) |
|Python SDK |[安装 Python SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-python-sdk-zh-CN) |[Python SDK 源码](https://github.com/byteplus-sdk/byteplus-sdk-python) |[Python 示例](https://github.com/byteplus-sdk/byteplus-sdk-python/tree/master/byteplus_sdk/example/live) |
|PHP SDK |[安装 PHP SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-php-sdk-zh-CN) |[PHP SDK 源码](https://github.com/byteplus-sdk/byteplus-sdk-php) |[PHP 示例](https://github.com/byteplus-sdk/byteplus-sdk-php/tree/master/examples/Live) |
|Node.js SDK |[安装 Node.js SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-node-js-sdk-zh-CN) |无 |无 |
