---
title: "Stream Fallback in V3"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70137"
---

You may need to lower the sent/received video quality in the following scenarios:


* High\-resolution video streaming stutters under poor network connection;

* Sub\-optimal device performance leads to choppy high\-resolution video stream codec;

* Video profile should be set according to the window size of the receiver. For example, receive high\-resolution video streams in fullscreen; Receive standard definition video streams when the window is smaller.


In these scenarios, the publisher/subscriber can enable the stream fallback. After it is set up,


* On the publisher: High\-quality streams are degraded based on the resolution level.

* On the subscriber side, the subscribed stream is downgraded to the publisher's next\-lowest resolution level.

> Note: Currently, the Web SDK only supports subscribers setting up stream fallback for weak network conditions, not for insufficient decoding performance.

> See [Simulcasting](https://docs.byteplus.com/en/docs/12/docs-70139) for resolution levels.


<span id="prerequisite"></span>
## Prerequisite

To set up video stream fallback, ensure that you have enabled simulcasting on the publisher. For more information, see [Simulcasting](https://docs.byteplus.com/en/docs/12/docs-70139).

<span id="using-the-client-sdk"></span>
## Using the client SDK

You need to configure video stream fallback on both the publisher and the subscriber.

<span id="set-the-stream-fallback-policy-for-the-publisher"></span>
### Set the stream\-fallback policy for the publisher

After the publisher has enabled simulcasting and set the expected parameter value, the SDK will automatically classify the value. You need to enable the audio & video stream fallback of the publisher to degrade the video stream when the network is poor or the device performance is insufficient. To be specific, the sent stream will be degraded in sequence from high\-quality level. When the resolution of the high stream gets close to the medium level, the high\-quality stream is dropped, This process continues for the remaining stream levels; when the network and device performance improves, RTC resumes simulcasting.

At this point, the publisher's high stream begins to downgrade tier by tier. If the medium stream is 540p and the network environment still cannot support sending a 540p stream, the high stream is canceled and the medium stream begins to downgrade. This process continues sequentially until it finally downgrades to the low stream.

<span id="set-the-stream-fallback-policy-for-the-subscriber"></span>
#### Set the stream\-fallback policy for the subscriber

You can enable automatic stream fallback in case of poor downlink network or insufficient device performance. The SDK supports two methods.


* When the downstream network is poor or the device performance is insufficient, the received stream will be degraded in sequence from the current resolution. When the network and device performance improves, it will return to the original quality. Generally, this method is used when multiple streams are published on the publisher. This method does not take effect when simulcasting is not enabled on the publisher.

* The received streams fall back to an audio\-only stream and revert to video streams when network or device performance improves. Generally, this method is used when simulcasting is not enabled on the publisher.


<span id="client-api-reference"></span>
### Client API reference


|Feature description |Android |iOS |Windows |macOS |Web |
|---|---|---|---|---|---|
|Set the fallback option for the subscribed media stream |[setSubscribeFallbackOption](https://docs.byteplus.com/en/docs/12/docs-70080#setsubscribefallbackoption) |[setSubscribeFallbackOption:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-setsubscribefallbackoption) |[setSubscribeFallbackOption](https://docs.byteplus.com/en/docs/12/docs-70095#setsubscribefallbackoption) |/ |[setSubscribeFallbackOption](https://docs.byteplus.com/en/docs/12/docs-104478#setsubscribefallbackoption) |


<span id="predefine-the-stream-fallback-policy-on-the-server"></span>
## Predefine the stream\-fallback policy on the server

Contact technical support to help you configure the publisher/subscriber stream fallback on the RTC server. Server\-side configurations have a higher priority than client\-side API settings.

<span id="changelog"></span>
## Changelog

This feature has been available since Client SDK v3.45.
