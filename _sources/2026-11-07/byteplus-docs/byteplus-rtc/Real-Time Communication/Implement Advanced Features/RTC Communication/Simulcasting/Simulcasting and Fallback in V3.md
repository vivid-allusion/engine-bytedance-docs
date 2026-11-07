---
title: "Simulcasting and Fallback in V3"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1359024"
---

The sender may need to encode and push multiple video streams with the same content yet different specifications to other users in the room simultaneously.

The stream encoded in the best resolution is called the high\-quality stream. And the other streams encoded in lower resolutions are called Simulcast streams.


* For the native SDK, you can set up to 3 Simulcast streams, including the base, low\-quality, and medium\-quality streams.

* For the Web SDK, you can set up to 2 Simulcast streams, including the medium\-quality and low\-quality streams.


<span id="applicable"></span>
## Applicable

You may need to lower the sent/ received video quality in the following scenarios:


* High\-resolution video streaming stutters under poor network connection;

* Sub\-optimal device performance leads to choppy decoding of high\-resolution video streams;

* Video profile should be set according to the window size of the receiver. For example, users should receive high\-resolution video streams when viewing in full screen and standard\-definition streams when the viewing window is smaller.


<span id="prerequisites"></span>
## Prerequisites


* You have integrated the RTC SDK and implemented basic real\-time functions.

   * Native SDK V3.60.2 or later versions.

   * Web SDK V4.63.0 or later versions.

* The Simulcast feature can only be used with video streams captured from a camera. It cannot be applied to screen\-sharing streams.


<span id="send-simulcast-streams"></span>
## Send Simulcast streams

 &nbsp;

When the sender enables simulcasting, the media stream can be automatically downgraded, and the receiver can select which simulcast stream to receive.


1. Call `setLocalSimulcastMode` before a user joins the room. The mode options include sending on demand and sending all simulcast streams. Arrange the stream list in ascending order.

   * `config[0]` is the base stream;

   * `config[1]` is the low\-quality stream;

   * `config[2]` is the medium\-quality stream.

> For the Web SDK, you can set up to 2 Simulcast streams, including the medium\-quality and low\-quality streams.


1. Call `setVideoEncoderConfig` to set the video encoding parameters for the high\-quality stream.

2. [Optional] You can call `setLocalSimulcastMode` again after the user joins a room to update the Simulcast stream encoding parameters.


<span id="media-stream-fallback"></span>
## Media stream fallback

When stream fallback is enabled, the SDK intelligently switches from the high\-quality to the lower\-quality streams based on network conditions. This dynamic adjustment ensures optimal viewing experience during video calling sessions, adapting in real\-time to varying network bandwidths and device capabilities.

Once the network and device performance improve, the streaming quality will revert to a higher level.

<span id="video-stream-fallback-on-the-sender-side"></span>
### Video stream fallback on the sender side


1. Enable the Simulcast feature through `setLocalSimulcastMode`. See [Send Simulcast streams](https://docs.byteplus.com/6uofwzl3/35212).

2. Allow automatic stream fallback on the sender side via `setPublishFallbackOption`.


In response to poor network conditions or insufficient device performance, the SDK then downgrades the published stream to the next lower\-quality stream, continuing until it reaches the lowest quality stream available.

<span id="media-stream-fallback-on-the-receiver-side"></span>
### Media stream fallback on the receiver side

Enable automatic fallback on the receiver side by calling `setSubscribeFallbackOption`. You can specify the fallback option by passing in enum values.


* The received stream is downgraded from the high\-quality stream to a lower\-quality one, continuing until it reaches the lowest quality stream in the published list. This mode applies when the sender has published simulcast streams.

* The stream falls back from video to audio\-only. This mode applies when the sender has not published any simulcast streams.


<span id="subscribe-to-a-simulcast-stream"></span>
## Subscribe to a Simulcast stream


1. Enable the Simulcast feature through `setLocalSimulcastMode`. See [Send Simulcast streams](https://docs.byteplus.com/6uofwzl3/35212).

2. Set your Simulcast stream subscription preferences using `setRemoteSimulcastStreamType`. You can specify your subscription preferences by passing in enum values.


When the specified simulcast stream cannot be found in the published list, the SDK automatically subscribes to the next lower\-quality stream.


* When the specified Simulcast stream is not published, the SDK will automatically subscribe to the next lower quality stream. For example,

   * If the sender only publishes the high\-quality stream and one Simulcast stream `config[0]`, and the receiver prefers the medium\-quality stream, they will actually subscribe to the only Simulcast stream `config[0]`.

   * If the sender publishes the high\-quality stream and two simulcast streams (`config[0]` and `config[1]`), and the receiver prefers the medium\-quality stream, they will actually subscribe to `config[1]`.

* When the sender and receiver use the Native and Web SDKs respectively:

   * The sender who uses the Native SDK sends the high\-quality stream and three Simulcast streams `config[0]`, `config[1]`, and `config[2]`. A receiver using the Web SDK can never subscribe to `config[0]`, which is the lowest\-quality stream.

   * The sender who uses the Web SDK sends the high\-quality stream and two Simulcast streams `config[0]` and `config[1]`. The receiver who uses the Native SDK prefers the base stream. They will actually subscribe to `config[0]`.


<span id="api-reference"></span>
## API reference


|Description |Android |iOS |macOS |Windows |Linux |Web |
|---|---|---|---|---|---|---|
|<br>---<br><br> |<br>---<br><br> |<br>---<br><br> |<br>---<br><br> |<br>---<br><br> |<br>---<br><br> |<br>---<br><br> |
|Enables the Simulcast feature. |`setLocalSimulcastMode(VideoSimulcastMode mode)` |`setLocalSimulcastMode:` |`setLocalSimulcastMode:` |`setLocalSimulcastMode(VideoSimulcastMode mode)` |`setLocalSimulcastMode(VideoSimulcastMode mode)` |[setLocalSimulcastMode](https://docs.byteplus.com/en/docs/12/docs-104478#setlocalsimulcastmode) |
|Sets the high\-quality stream. |`setVideoEncoderConfig` |`setVideoEncoderConfig:` |`setVideoEncoderConfig:` |`setVideoEncoderConfig` |`setVideoEncoderConfig` |[setVideoEncoderConfig](https://docs.byteplus.com/en/docs/12/docs-104478#setvideoencoderconfig) |
|Sets the Simulcast streams. |`setLocalSimulcastMode(VideoSimulcastMode mode, VideoEncoderConfig[] streamConfig)` |`setLocalSimulcastMode:config:` |`setLocalSimulcastMode:config:` |`setLocalSimulcastMode(VideoSimulcastMode mode, VideoEncoderConfig[] streamConfig)` |`setLocalSimulcastMode(VideoSimulcastMode mode, VideoEncoderConfig[] streamConfig)` |[setLocalSimulcastMode](https://docs.byteplus.com/en/docs/12/docs-104478#setlocalsimulcastmode) |
|Sets the preferred simulcast stream type to subscribe to. |`setRemoteSimulcastStreamType` |`setRemoteSimulcastStreamType:streamType:` |`setRemoteSimulcastStreamType:streamType:` |`setRemoteSimulcastStreamType` |`setRemoteSimulcastStreamType` |[setRemoteSimulcastStreamType](https://docs.byteplus.com/en/docs/12/docs-104478#setremotesimulcaststreamtype) |
|Sets the fallback options on the sender side. |[setPublishFallbackOption](https://docs.byteplus.com/en/docs/12/docs-70080#setpublishfallbackoption) |[setPublishFallbackOption:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-setpublishfallbackoption) |[setPublishFallbackOption:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCEngine-setpublishfallbackoption) |[setPublishFallbackOption](https://docs.byteplus.com/en/docs/12/docs-70095#setpublishfallbackoption) |[setPublishFallbackOption](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-setpublishfallbackoption) |*  |
|Sets the fallback options on the receiver side. |[setSubscribeFallbackOption](https://docs.byteplus.com/en/docs/12/docs-70080#setsubscribefallbackoption) |[setSubscribeFallbackOption:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-setsubscribefallbackoption) |[setSubscribeFallbackOption:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCEngine-setsubscribefallbackoption) |[setSubscribeFallbackOption](https://docs.byteplus.com/en/docs/12/docs-70095#setsubscribefallbackoption) |[setSubscribeFallbackOption](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-setsubscribefallbackoption) |[setSubscribeFallbackOption](https://docs.byteplus.com/en/docs/12/docs-104478#setsubscribefallbackoption) |


<span id="changelog"></span>
## Changelog

In Native SDK V3.60.2 and Web SDK V4.63.0, we improved the Simulcast feature. For information of the legacy interface, see [Pushing Simulcast Video Streams](https://docs.byteplus.com/en/docs/12/docs-70139) and [Audio and Video Stream Fallback](https://docs.byteplus.com/en/docs/12/docs-70137).


* The sender and receiver interfaces have changed. For more information, see [Upgrade Guide](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-changelogs).

* The video streaming will now fallback to each provided encoding parameters in descending order, rather than falling back to the predefined resolution streams set by the SDK. For example, if the sender has set up 1080P (high), 360P (medium), and 180P (low).

   * In the previous versions, the degrading path was 1080P (high) \-\> 720P (high) \-\> 630P (high) \-\> 540P (high) \-\> 450P (high) \-\> 360P (medium) \-\> 270P (medium) \-\> 180P (low) \-\> 144P (low).

   * In the current version, the degrading path is 1080P (high) \-\> 360P (medium) \-\> 180P (low).
