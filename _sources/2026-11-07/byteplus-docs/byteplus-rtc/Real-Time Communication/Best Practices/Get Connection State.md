---
title: "Get Connection State"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-95376"
---

To optimize the users' experience, you are encouraged to prompt the user as the network state changes. This document shows you how to get network states.

<span id="show-network-quality"></span>
## Show network quality

A weak Wi\-Fi or cellular signal can result in a poor call experience. Inform users of the network quality so they can anticipate potential issues or take preventive measures.

Get the network quality of the local client and remote clients via `onNetworkQuality`. Refer to [Show Call Statistics](https://docs.byteplus.com/docs/byteplus-rtc/docs-106866).

<span id="get-informed-of-local-connection-state"></span>
## Get the Local Connection State

Both of the disconnections below make an RTC call no longer available.


1. The client lost connection to the Internet.

2. The client cannot reach the RTC server or the server is down.


<span id="_1-no-internet-connection"></span>
### 1. No Internet connection

Get notifications of the disconnection via the following:


* `onNetworkTypeChanged` notifies you when the device loses its connection to a Wi\-Fi or cellular network.

   * For the Native SDK, listen to `onNetworkTypeChanged` to detect a local network disconnection.

   * For the Web SDK, a `DOWN` state in the [onNetworkQuality](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onnetworkquality) callback indicates a local network disconnection.

> Due to the limitations of the platform, you may not be notified of the disconnection event promptly for a Windows device or certain Android models.


* Perform a "ping" test against a URL or IP address that is expected to respond.


<span id="_2-server-connection-lost"></span>
### 2. Server connection lost

Get notifications of disconnection from the server via `onConnectionStateChanged`.

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/%E9%AB%98%E7%BA%A7%E5%8A%9F%E8%83%BD/%E8%BF%9E%E6%8E%A5%E7%8A%B6%E6%80%81%E6%8F%90%E7%A4%BA/connection_state.png) </span>


* `CONNECTION_STATE_DISCONNECTED`: This state indicates that the SDK has not received a response from the server for 12 seconds.

* `CONNECTION_STATE_LOST`: This state indicates that a 10\-second reconnection attempt has failed after the SDK was disconnected.


<span id="learn-about-a-remote-user-is-disconnected"></span>
## Learn when a remote user is disconnected

After 15 seconds without a response, the server attempts to reconnect for another 15 seconds. If that fails, the server marks the user as offline, and the RTC server broadcasts the `onUserLeave` event to inform other users in the room.

If the disconnected user was also publishing media streams, the RTC server also broadcasts `onUserPublishStreamAudio` or `onUserPublishStreamVideo` notifications.

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/%E9%AB%98%E7%BA%A7%E5%8A%9F%E8%83%BD/%E8%BF%9E%E6%8E%A5%E7%8A%B6%E6%80%81%E6%8F%90%E7%A4%BA/remote_user_connection_state.png) </span>

<span id="api-reference"></span>
## API reference


* Android

   * [onConnectionStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#onconnectionstatechanged)

   * [onNetworkTypeChanged](https://docs.byteplus.com/en/docs/12/docs-70081#onnetworktypechanged)

* iOS

   * [rtcEngine:onConnectionStateChanged:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onconnectionstatechanged)

   * [rtcEngine:onNetworkTypeChanged:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onnetworktypechanged)

* macOS

   * [rtcEngine:onConnectionStateChanged:](https://docs.byteplus.com/en/docs/12/docs-70093#ByteRTCEngineDelegate-rtcengine-onconnectionstatechanged)

   * [rtcEngine:onNetworkTypeChanged:](https://docs.byteplus.com/en/docs/12/docs-70093#ByteRTCEngineDelegate-rtcengine-onnetworktypechanged)

* Windows

   * [onConnectionStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#onconnectionstatechanged)

   * [onNetworkTypeChanged](https://docs.byteplus.com/en/docs/12/docs-70096#onnetworktypechanged)

* Web

   * [onConnectionStateChanged](https://docs.byteplus.com/en/docs/12/docs-104479#onconnectionstatechanged)

> `CONNECTION_STATE_LOST` indicates a disconnection between the client and the server. This state is available in version 4.45 and later.


   * [onNetworkQuality](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onnetworkquality)

> `DOWN` indicates that the local network has disconnected. This status is available in version 4.55 and later.
