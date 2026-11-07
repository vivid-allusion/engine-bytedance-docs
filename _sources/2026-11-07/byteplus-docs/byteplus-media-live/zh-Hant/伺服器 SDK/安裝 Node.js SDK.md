---
title: "安裝 Node.js SDK"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-node-js-sdk-zh-TW"
---

本主題介紹如何安裝 Node.js SDK，並提供範例程式碼以協助加速您的開發流程。

<span id="75e5f6a0"></span>
## 先決條件


* Access Key：請參考 [Server SDK 概述](https://docs.byteplus.com/docs/byteplus-media-live/docs-server-sdk-zh-TW)。

* 環境需求：需安裝 Node.js 16 或更高版本。


<span id="1aa97479"></span>
## 安裝 SDK

使用 npm 安裝 SDK：

```JavaScript
npm install -S @byteplus/vcloud-sdk-nodejs@latest
```


<span id="a0f1289c"></span>
## 初始化 SDK 並配置憑證

Node.js SDK 提供三種設定存取憑證（AK 與 SK）的方法。建議的方法是在程式碼中配置憑證，這可讓開發環境進行動態配置。


<Tabs>
<Tab zoneid="z2DiNgezwQ" title="在程式碼中配置 AK/SK（推薦）">
<TabTitle>在程式碼中配置 AK/SK（推薦）</TabTitle>

此方法適用於需在應用程式啟動時動態設定憑證的場景。

```JavaScript
import { liveOpenapi } from '@byteplus/vcloud-sdk-nodejs';
// Use the default service instance.
const liveService = liveOpenapi.defaultService;

// Set AK and SK.
liveService.setAccessKeyId(AccessKeyId);
liveService.setSecretKey(SecretKey);
// If you use STS for requests, you also need to set the `SessionToken` after the AK and SK are set.
liveService.setSessionToken(SessionToken);
```



</Tab>
<Tab zoneid="hQJaWlBFVu" title="透過環境變數配置 AK/SK">
<TabTitle>透過環境變數配置 AK/SK</TabTitle>

此方法適用於本地或已部署環境，憑證可直接透過環境變數設定。

```JavaScript
BYTEPLUS_ACCESSKEY="your ak" BYTEPLUS_SECRETKEY="your sk"
```



</Tab>
<Tab zoneid="I7l8wXnmlj" title="透過設定檔配置 AK/SK">
<TabTitle>透過設定檔配置 AK/SK</TabTitle>

此方法適用於固定的開發環境。設定檔路徑為 `~/.byteplus/config`，內容需為 JSON 格式：

```JavaScript
{"BYTEPLUS_ACCESSKEY":"your ak","BYTEPLUS_SECRETKEY":"your sk"}
```



</Tab>
</Tabs>


<span id="927d549b"></span>
## 呼叫 API

SDK 初始化後，即可呼叫 API。以下為從 MediaLive 服務呼叫 [DescribeLiveBandwidthData](https://docs.byteplus.com/en/docs/byteplus-media-live/eescribelivebandwidthdata) API 的範例：

```JavaScript
import { liveOpenapi } from "@byteplus/vcloud-sdk-nodejs";

async function main(AccessKeyId, SecretKey) {
  // Use the default service instance.
  const liveService = liveOpenapi.defaultService;

  // Set AK and SK.
  liveService.setAccessKeyId(AccessKeyId);
  liveService.setSecretKey(SecretKey);

  // Call the API.
  const usersResponse = await liveService.DescribeLiveBandwidthData({
    Aggregation: 300,
    EndTime: "2025-04-16T23:59:59+08:00",
    StartTime: "2025-04-16T00:00:00+08:00",
    TimeZone: "Asia/Shanghai",
  });
}
```
