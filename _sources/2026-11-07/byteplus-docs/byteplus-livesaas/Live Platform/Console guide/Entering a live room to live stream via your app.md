---
title: "Entering a live room to live stream via your app"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-entering-a-live-room-to-live-stream-via-your-app"
---

After integrating the Live Streaming SDK, the next step is to obtain the necessary credentials to enter a live room. This guide explains how to get the required activity ID and secret key, either by making API calls or by retrieving them from the BytePlus Live console.

Get the activity ID and secret key for a live room using one of the following methods:


* Call [CreateActivityAPIV2](https://docs.byteplus.com/docs/byteplus-livesaas/docs-createactivityapiv2) or [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi) to get the activity ID, and call [GetTemporaryLoginTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-gettemporarylogintokenapi) to get the secret key.

* Log in to the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/), and then get the activity ID and secret key for a live room. See the screenshot below.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7c1be61c29194b9a91081bc73904d4dc~tplv-goo7wpa0wc-image.image) </span>


For more information about how to integrate the Live Streaming SDK, see [Integrating the Live Streaming SDK for iOS](https://docs.byteplus.com/docs/byteplus-livesaas/docs-integrating-the-live-streaming-sdk-for-ios) and [Integrating the Live Streaming SDK for Android](https://docs.byteplus.com/docs/byteplus-livesaas/docs-integrating-the-live-streaming-sdk-for-android).
