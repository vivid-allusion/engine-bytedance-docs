---
title: "Publishing and Subscribing to Media Streams"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/145594"
---

WTN provides a set of HTTP APIs based on the WebRTC signaling protocol, enabling you to publish and subscribe to real\-time audio and video streams.

This document explains the overall logic, from completing the Offer/Answer SDP exchange to establishing a connection with the WTN media service. After connecting, you can effectively manage your media streams.


> * WTN offers a set of HTTP APIs based on the concept of **streams**.

> * A stream consists of one audio stream and one video stream, corresponding to two m\-lines in the SDP, with the `type` set to `audio` and `video`, respectively.


The basic logic is as follows:

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_9fa077d299b9b52d5ffa3607878b0360.png) </span>

> For more information on resources, see [Publish Resource and Subscription Resource](https://docs.byteplus.com/docs/byteplus-rtc/132443).


<span id="api-reference"></span>
## API Reference

WTN provides the following APIs for creating and destroying publishing/subscription resources:


* [Create Publishing Resource](https://docs.byteplus.com/docs/byteplus-rtc/132482)

* [Destroy Publishing Resource](https://docs.byteplus.com/docs/byteplus-rtc/132483)

* [Create Subscription Resource](https://docs.byteplus.com/docs/byteplus-rtc/132484)

* [Destroy Subscription Resource](https://docs.byteplus.com/docs/byteplus-rtc/132485)


<span id="code-implementation"></span>
## Code Implementation

For web applications, WTN provides a sample project. Refer to [Building a Basic Application](https://docs.byteplus.com/docs/byteplus-rtc/132450) to understand the specific code logic.
