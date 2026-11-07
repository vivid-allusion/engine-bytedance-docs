---
title: "Server SDK 概述"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-server-sdk-zh-TW"
---

BytePlus MediaLive 提供多種程式語言的 Server SDK。每個 Server SDK 都封裝了以下功能，讓您能夠快速調用 BytePlus MediaLive OpenAPI：


* 簽名生成，可省去繁瑣的計算流程。

* 常見的 OpenAPI 操作，包括發送請求與處理回應。每個 SDK 都提供相應的程式碼範例。


<span id="17e2c1c8"></span>
## 取得 Access Key

要使用 Server SDK，您需先取得 Access Key，其由 **Access Key ID** 和 **Secret Access Key** 組成。

主帳戶的 Access Key 洩漏可能會造成嚴重的安全風險。因此，建議您使用子帳戶的 Access Key。


* 若要使用管理員帳戶，您需要 [取得管理員帳戶的 Access Key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-an-accesskey#create-an-access-key-through-the-key-management-screen)；

* 若要使用子帳戶，您需要 [取得子帳戶的 Access Key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-an-accesskey#create-an-access-key-through-the-user-details-screen)。


<span id="SDKs"></span>
## 安裝與使用


|**SDK** |**指南** |**原始碼** |**範例** |
|---|---|---|---|
|Java SDK |[安裝 Java SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-java-sdk-zh-TW) |[Java SDK 原始碼](https://github.com/byteplus-sdk/byteplus-sdk-java) |[Java 範例](https://github.com/byteplus-sdk/byteplus-sdk-java/tree/master/example/src/main/java/com/byteplus/example/live) |
|Go SDK |[安裝 Go SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-golang-sdk-zh-TW) |[Go SDK 原始碼](https://github.com/byteplus-sdk/byteplus-sdk-golang) |[Go 範例](https://github.com/byteplus-sdk/byteplus-sdk-golang/tree/master/example/demo_live) |
|Python SDK |[安裝 Python SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-python-sdk-zh-TW) |[Python SDK 原始碼](https://github.com/byteplus-sdk/byteplus-sdk-python) |[Python 範例](https://github.com/byteplus-sdk/byteplus-sdk-python/tree/master/byteplus_sdk/example/live) |
|PHP SDK |[安裝 PHP SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-php-sdk-zh-TW) |[PHP SDK 原始碼](https://github.com/byteplus-sdk/byteplus-sdk-php) |[PHP 範例](https://github.com/byteplus-sdk/byteplus-sdk-php/tree/master/examples/Live) |
|Node.js SDK |[安裝 Node.js SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-node-js-sdk-zh-TW) |無 |無 |
