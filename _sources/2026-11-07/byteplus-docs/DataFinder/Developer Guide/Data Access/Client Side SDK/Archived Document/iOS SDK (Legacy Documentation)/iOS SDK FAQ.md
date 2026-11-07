---
title: "iOS SDK FAQ"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/iOS_SDK_FAQ"
---

<span id="f77c0ce5"></span>
### 1.   iOS data reporting strategy

The SDK is not initialized and will not be cached locally. When to report:


* Report immediately when switching between the front and back of the app

* Profile request immediately

* After the SDK is started, it will be reported every 60s (up to 2,000 pieces each time. If more than 2,000 pieces are generated in one minute, you need to wait for the next 60s to report again)


<span id="2b8f0b2b"></span>
### 2. iOS client side can't receive the callback notification of ABTestSuccess after calling the pullABTestConfigs interface

Check whether the object listening for the notification is released when the notification is called back. If it is released, the notification will not be received.

<span id="ios本地缓存储存在哪里？sdk侧是否有限制？"></span>
### 3. Where iOS local cache stored? Is there any restriction on the SDK side?

The local cache is stored in SQLite, and the SDK has no restrictions, following the memory size limit of the mobile phone.

<span id="ios-sdk是否支持iwatch的watch-os系统"></span>
### 4. iOS SDK supports iWatch watch OS

Not supported yet. If you need to use event tracking, you can consider using the HTTP API, refer to the documentation:[HTTP API](https://docs.byteplus.com/docs/DataFinder/HTTP_API).
