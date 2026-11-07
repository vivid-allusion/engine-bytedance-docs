---
title: "Installing Node.js SDK"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-node-js-sdk"
---

This guide describes how to use the BytePlus MediaLive Node.js SDK, including installation, credential configuration, calling OpenAPI endpoints.

<span id="17bf8b9b"></span>
## Prerequisites

Before you begin, ensure that you have the following prerequisites:


* **Access Key**: Refer to the [Server SDK overview](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-server-sdk#get-access-key) for details on how to obtain your Access Key and Secret Key.

* **Node.js**: Ensure that you have Node.js 16 or later installed.


<span id="install-the-sdk"></span>
## Install the SDK

To get started, install the SDK using npm:

```JavaScript
npm install -S @byteplus/vcloud-sdk-nodejs@latest
```


<span id="91b4a4b5"></span>
## Initialize the SDK and Configure Credentials

BytePlus MediaLive SDK provides three methods for setting access credentials (AK/SK). The recommended method is to configure the credentials in code, which allows for dynamic configuration in a development environment.


<Tabs>
<Tab zoneid="ebkAMhMTy0" title="Configure AK/SK in Code (Recommended)">
<TabTitle>Configure AK/SK in Code (Recommended)</TabTitle>

This approach is suitable for scenarios where credentials need to be dynamically set at the start of your application.

```JavaScript
import { liveOpenapi } from '@byteplus/vcloud-sdk-nodejs';
// Use the default service instance.
const liveService = liveOpenapi.defaultService;

// set aksk
liveService.setAccessKeyId(AccessKeyId);
liveService.setSecretKey(SecretKey);
// If you use sts to request, you need to set up `SessionToken` after aksk is set
liveService.setSessionToken(SessionToken);
```



</Tab>
<Tab zoneid="daeuTLxAd8" title="Configure AK/SK via Environment Variables">
<TabTitle>Configure AK/SK via Environment Variables</TabTitle>

This method is appropriate for local or deployed environments where credentials are directly set via environment variables.

```JavaScript
BYTEPLUS_ACCESSKEY="your ak" BYTEPLUS_SECRETKEY="your sk"
```



</Tab>
<Tab zoneid="kIwKOSjjJp" title="Configure AK/SK via Configuration File">
<TabTitle>Configure AK/SK via Configuration File</TabTitle>

This method is suitable for fixed development environments. The configuration file path is ~/.byteplus/config, and the content should be in JSON format:

```JavaScript
{"BYTEPLUS_ACCESSKEY":"your ak","BYTEPLUS_SECRETKEY":"your sk"}
```



</Tab>
</Tabs>


<span id="9fa683c6"></span>
## Call OpenAPI Interfaces

Once the SDK is initialized, you can call OpenAPI endpoints. Below is an example of calling the `DescribeLiveBandwidthData` API from the MediaLive service:

```JavaScript
import { liveOpenapi } from "@byteplus/vcloud-sdk-nodejs";

async function main(AccessKeyId, SecretKey) {
  // Use the default service instance.
  const liveService = liveOpenapi.defaultService;

  // set aksk
  liveService.setAccessKeyId(AccessKeyId);
  liveService.setSecretKey(SecretKey);

  // Request OpenAPI
  const usersResponse = await liveService.DescribeLiveBandwidthData({
    Aggregation: 300,
    EndTime: "2025-04-16T23:59:59+08:00",
    StartTime: "2025-04-16T00:00:00+08:00",
    TimeZone: "Asia/Shanghai",
  });
}
```
