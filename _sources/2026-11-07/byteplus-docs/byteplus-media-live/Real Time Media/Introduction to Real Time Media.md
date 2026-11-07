---
title: "Introduction to Real Time Media"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-introduction-to-real-time-media"
---

The ultra\-low latency live streaming feature, known as Real Time Media (RTM), utilizes advanced audio and video processing technologies as well as large\-scale content distribution technologies. By converting the link transmission protocol to UDP and optimizing other underlying technologies, it overcomes the inherent limitations of the TCP protocol and reduces latency caused by network jitter. Working alongside the BytePlus MediaLive Player SDKs, RTM can achieve millisecond latency when streaming to tens of millions of concurrent users. It is significantly faster than FLV, HLS, and other TCP streaming protocols that typically have a latency of 3 to 10 seconds. Additionally, RTM provides a high\-quality viewing experience that is low in lag, fast to load, and compatible with most audio and video encoding formats used in the industry.

<span id="bc9ec5a6"></span>
## Highlights

**Smooth integration**

RTM is compatible with BytePlus MediaLive's existing media processing capabilities, such as transcoding, recording, and screenshot capturing.

It is compatible with the TCP push streaming protocol. Streams pushed in the RTMP protocol can be pulled using the RTM, RTMP, FLV, and HLS protocols. You can easily integrate the RTM feature into your current live streaming setup by using your existing domain names.

**High\-quality experience**

RTM leverages features from various protocols such as WebRTC and QUIC and utilizes UDP to reduce latency to less than one second. This leads to faster first\-frame rendering and reduced stutter, resulting in improved core performance indicators.

**Broad compatibility**

RTM caters to the specific needs of the live streaming industry by offering support for advanced audio and video codecs such as AAC, B frames, and H.265.

**Secure and reliable**

RTM uses a UDP\-based MiniSDP signaling instead of HTTP signaling to optimize the connection time and success rate, especially in weak network conditions.

**Large\-scale and high concurrency**

RTM is used extensively in ByteDance's commercial apps and has been continuously optimized, field\-tested with hundreds of millions of concurrent users.

<span id="99821b12"></span>
## Use cases

RTM is ideal for the following scenarios:


* E\-commerce: Live streaming to improve buyer\-seller interactions and boost sales.

* Education: RTM is ideal for large online classes. Its low latency enables students to answer the teacher's questions and receive real\-time feedback.

* Sports: RTM enables online audiences to experience competitions and e\-sports in real time.

* Entertainment: The host can use RTM to provide real\-time feedback and interact with viewers who send gifts.


<span id="044fb363"></span>
## Using RTM

If you use the RTM feature, live\-streaming service fees will be charged. Upstream is charged as standard streaming, while downstream is charged as RTM streaming. For details, see [Live-streaming service fees](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-live-streaming-service-fees).

<span id="12a942c4"></span>
### Activating the service

When you create a domain name on BytePlus MediaLive, the RTM service is enabled by default. You do not have to activate the service manually.

There is no requirement to have a separate domain name in order to pull a stream using RTM. RTM is integrated with RTMP, FLV, and HLS. Instead, you can simply use an RTM\-specific playback address.

<span id="34760cd6"></span>
### Getting an RTM address for stream pulling


1. Log in to the [BytePlus MediaLive console](https://console.byteplus.com/live).

2. Use the [address generator](https://docs.byteplus.com/en/byteplus-media-live/docs/address-generator) to generate an RTM address. You can also manually construct the address. For more information, see [Generating live-stream addresses](https://docs.byteplus.com/docs/byteplus-media-live/docs-generating-live-stream-addresses).


<span id="2bec02df"></span>
### Using RTM with the Player SDKs

For optimal experience, we recommend that you use the BytePlus MediaLive SDKs for RTM stream pulling. The following versions of BytePlus MediaLive Player SDKs support RTM.


|**Operating system** |**SDK name** |**SDK edition and version** |**Use Cases** |
|---|---|---|---|
|Android |Player SDK |Advanced edition, v1.25.2 and higher |[Android RTM stream pulling](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-implementing-advanced-features-2#rtm-stream-pulling) |
|iOS |Player SDK |Advanced edition, v1.25.2 and higher |[iOS RTM stream pulling](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-implementing-advanced-features-3#rtm-stream-pulling) |
|Web |Player SDK |v1.0.0 and higher |[Web RTM stream pulling](https://docs.byteplus.com/en/docs/byteplus-media-live/RTM-Streaming-Integration) |
