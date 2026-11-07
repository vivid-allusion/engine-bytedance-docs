---
title: "Setting Configurations for Scenarios"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70135"
---

If you want to configure audio & video calls for specific scenarios, or cloud media processing tasks (such as recording, retweeting LIVE, etc.), you can use the cloud configuration feature.

<span id="introduction"></span>
## Introduction

To apply special configurations like higher resolution or different recording quality to specific scenarios within the same AppId, you can use the `BusinessId` feature. This allows you to differentiate between various business needs, such as providing enhanced audio for a music chat room or setting unique recording parameters for certain cloud media tasks, all while using a single AppId. This guide explains how to define a `BusinessId` and use it to enable scenario\-based configurations for your RTC calls and cloud processing tasks.

<span id="procedure"></span>
## Procedure

Before requesting a special configuration, make sure you have enabled the RTC service, created the application, and obtained the corresponding AppId. For information on how to create an application, see [Before Using RTC Service](https://docs.byteplus.com/en/docs/12/docs-69865).

When using the Segment Configuration delivery feature, you must follow these steps:


1. Go to the `Console > BusinessID` page, and add the BusinessId you need under AppId. As shown in the figure below, in the application of `AppId = defaultAppName`, there is `BusinessId = chatroom`.

   <span>![图片](https://p16-arcosite-sg.ibyteimg.com/tos-alisg-i-k9wyc2ijk0-sg/186b5f2d96fc45f9b4c7e9ffae3821b9~tplv-k9wyc2ijk0-image.image) </span>

   You can add a new BusinessId such as livePK shown below:

   <span>![图片](https://p16-arcosite-sg.ibyteimg.com/tos-alisg-i-k9wyc2ijk0-sg/a37eb51085be4b4b83da7ea57f055b9b~tplv-k9wyc2ijk0-image.image) </span>

2. Contact technical support, specify `AppId > BusinessId` that requires special configuration, and describe your use case. Technical support will add the special configuration in the background.

3. To apply the special configuration, you must provide the corresponding `AppId` and `BusinessId` when starting a call or task.


When starting an audio & video call, you can use the following interfaces to set the `businessId`:


* Android: [setBusinessId](https://docs.byteplus.com/en/docs/12/docs-70080#setbusinessid)

* iOS: [setBusinessId](https://docs.byteplus.com/en/docs/12/docs-70086#setbusinessid)

* macOS: [setBusinessId](https://docs.byteplus.com/en/docs/12/docs-70092#setbusinessid)

* Windows: [SetBusinessId](https://docs.byteplus.com/en/docs/12/docs-70095#setbusinessid)

* Web: [setBusinessId](https://docs.byteplus.com/en/docs/12/docs-104478#setbusinessid)


When performing cloud media processing tasks, the `businessId` field is usually included in the passed parameters.
