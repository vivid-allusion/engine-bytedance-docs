---
title: "Live streaming"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/docs-live-streaming"
---

To implement live stream pushing and pulling, this guide introduces how to use VideoOne with the BytePlus MediaLive Broadcast SDK and Player SDK. It provides a high\-level overview and links to detailed implementation guides and code samples, helping you quickly set up live broadcasting and viewing functionalities.

<span id="a53bbaf7"></span>
# MediaLive Integration Guide

<span id="99037d3e"></span>
## Generating live stream addresses

To enable a complete live streaming workflow, you need a push URL to send the live video and audio feed to the server, and a pull URL to retrieve and play the live stream. Refer to [Generating live stream addresses](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generating-live-stream-addresses) to generate push and pull stream URLs.

<span id="0fc04b5e"></span>
## Implement features

<span id="807a6c98"></span>
### Pushing a live stream

VideoOne demonstrates how to use the BytePlus MediaLive Broadcast SDK to push captured, encoded, and packaged live streams to the MediaLive service. Currently, it supports four streaming methods: camera capture, audio\-only streaming, screen sharing, and streaming local or online media files. For more details on implementing these functionalities, please refer to the following documentation:


|Platform |Android |iOS |
|---|---|---|
|Broadcast SDK reference documentation |* [Basic features](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-implementing-basic-features)<br><br>* [Advanced features](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-implementing-advanced-features) |* [Basic features](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-implementing-basic-features-1)<br><br>* [Advanced features](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-implementing-advanced-features-1) |


<span id="3bb31ef3"></span>
### Pulling a live stream

VideoOne demonstrates how to use the BytePlus MediaLive Player SDK to retrieve real\-time audio and video data from the server for playback. Currently, it supports pulling and playing live streams using multiple streaming protocols such as FLV, HLS, and RTMP. For more details on implementing these functionalities, please refer to the following documentation:


|Platform |Android |iOS |
|---|---|---|
|Player SDK reference documentation |* [Basic features](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-implementing-basic-features-2)<br><br>* [Advanced features](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-implementing-advanced-features-2) |* [Basic features](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-implementing-basic-features-3)<br><br>* [Advanced features](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-implementing-advanced-features-3) |


For a complete implementation of push and pull streaming, refer to the VideoOne open\-source code:


* [Android](https://github.com/byteplus-sdk/VideoOneSolutions/tree/main/Client/Android/solutions/media-live)

* [iOS](https://github.com/byteplus-sdk/VideoOneSolutions/tree/main/Client/iOS/Component/MediaLive)
