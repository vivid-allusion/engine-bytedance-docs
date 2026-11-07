---
title: "Playing videos with temporary playback tokens"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-playing-videos-with-temporary-playback-tokens"
---

To enhance security when playing audio and video files from the BytePlus VOD service, you can use the BytePlus VOD Player SDK to obtain playback addresses with temporary tokens. These tokens are specific to each video, have a limited duration, and are not interchangeable. This guide explains the playback process using tokens and how your app server can generate them for your client.

<span id="be757fdb"></span>
## **Playback process**

The process of playback using a temporary playback token is shown in the following diagram:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/94091b1c969a4a5d90ab29dbc09212ed~tplv-goo7wpa0wc-image.image) </span>

The process is explained as follows:


1. The app client requests a temporary playback token from the app server.

2. The app server generates a temporary playback token locally.

3. The app server returns the temporary playback token to the app client.

4. The app client passes the temporary playback token to the Player SDK.

5. The Player SDK requests playback information from the BytePlus VOD service using the temporary playback token.

6. The BytePlus VOD service returns the playback information to the Player SDK.

7. The Player SDK starts playing.


<span id="f0277407"></span>
## **Generating temporary playback tokens**

For ease of use, the Video On Demand server SDK encapsulates the issuance of temporary playback tokens. It is recommended to integrate the Video On Demand server SDK on the app server to generate temporary playback tokens and directly provide them to the client.

When using a temporary playback token, please note the following:


* The temporary playback token is a playback credential, not an actual playback address. The Video On Demand SDK automatically retrieves the playback address based on the temporary playback token.

* The temporary playback token contains audio and video information such as Vid and Format, and can only be used to obtain the playback address of the specified audio and video. Different Vid and Format require different temporary playback tokens.

* The default validity period of a temporary playback token is 900 seconds. When generating a temporary playback token using the Video On Demand server SDK, you can specify the validity period. After the temporary playback token expires, you need to obtain a new one. Note that the validity period of the token is not the same as the validity period of the obtained playback address. The validity period of the playback address still depends on the playback address validity period set in the Video On Demand console. For more details, please refer to the documentation.

* Issuing temporary playback tokens on the server\-side is a local operation, and you don't need to be concerned about the API latency.


To simplify the process, the BytePlus VOD Server SDK provides an API to generate temporary playback tokens. It is recommended to integrate the BytePlus VOD Server SDK into your application server to generate these tokens and provide them directly to the client.

When using a temporary playback token, keep the following in mind:


* The temporary playback token is a credential for playback, not an actual playback address. The BytePlus VOD Player SDK will automatically retrieve the playback address based on the temporary token.

* The temporary playback token contains audio and video information, such as `Vid` and `Format`, and can only be used to obtain the playback address for the specified audio and video. Different `Vid` and `Format` combinations require different temporary playback tokens.

* By default, the temporary playback token is valid for 900 seconds. When generating a temporary playback token using the BytePlus VOD Server SDK, you can specify the validity period. Once the token expires, you will need to obtain a new one. It's important to note that the token's validity period is different from the validity period of the obtained playback address, which is determined by the settings in the BytePlus VOD console. For more information, see [Anti-hotlinking with timestamp](https://docs.byteplus.com/docs/byteplus-vod/docs-timestamp-).

* The issuance of temporary playback tokens on the server\-side is a local process, so you don't need to be concerned about API latency.


For instructions on how to pass a temporary playback token when using the Player SDK, refer to the following documentation:


* [Android Player SDK: Quickstart](https://docs.byteplus.com/docs/byteplus-vod/docs-getting-started-with-the-android-player-sdk)

* [iOS Player SDK: Quickstart](https://docs.byteplus.com/docs/byteplus-vod/docs-getting-started-with-the-ios-player-sdk)

* [Web Player SDK: Quickstart](https://docs.byteplus.com/docs/byteplus-vod/docs-getting-started-with-the-web-player-sdk)
