---
title: "安装 Node.js SDK"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-node-js-sdk-zh-CN"
---

本主题介绍如何安装 Node.js SDK，并提供示例代码以帮助加快您的开发流程。

<span id="75e5f6a0"></span>
## 前提条件


* 访问密钥：请参阅 [服务端 SDK 概述](https://docs.byteplus.com/docs/byteplus-media-live/docs-server-sdk-zh-CN)。

* 环境要求：需要 Node.js 16 或更高版本。


<span id="1aa97479"></span>
## 安装 SDK

使用 npm 安装 SDK：

```JavaScript
npm install -S @byteplus/vcloud-sdk-nodejs@latest
```


<span id="a0f1289c"></span>
## 初始化 SDK 并配置凭证

Node.js SDK 提供三种设置访问凭证（AK 和 SK）的方法。推荐的方法是在代码中配置凭证，这样可以在开发环境中实现动态配置。


<Tabs>
<Tab zoneid="bWihGvRsUS" title="在代码中配置 AK/SK（推荐）">
<TabTitle>在代码中配置 AK/SK（推荐）</TabTitle>

此方法适用于需要在应用程序启动时动态设置凭证的场景。

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
<Tab zoneid="zxWaLAwF01" title="通过环境变量配置 AK/SK">
<TabTitle>通过环境变量配置 AK/SK</TabTitle>

此方法适用于本地或已部署环境，在这些环境中可以直接通过环境变量设置凭证。

```JavaScript
BYTEPLUS_ACCESSKEY="your ak" BYTEPLUS_SECRETKEY="your sk"
```



</Tab>
<Tab zoneid="QBRzsV3nhC" title="通过配置文件配置 AK/SK">
<TabTitle>通过配置文件配置 AK/SK</TabTitle>

此方法适用于固定的开发环境。配置文件路径为 `~/.byteplus/config`，内容需为 JSON 格式：

```JavaScript
{"BYTEPLUS_ACCESSKEY":"your ak","BYTEPLUS_SECRETKEY":"your sk"}
```



</Tab>
</Tabs>


<span id="927d549b"></span>
## 调用 API

SDK 初始化后，您可以调用 API。以下是调用 MediaLive 服务中的 [DescribeLiveBandwidthData](https://docs.byteplus.com/en/docs/byteplus-media-live/eescribelivebandwidthdata) API 的示例：

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
