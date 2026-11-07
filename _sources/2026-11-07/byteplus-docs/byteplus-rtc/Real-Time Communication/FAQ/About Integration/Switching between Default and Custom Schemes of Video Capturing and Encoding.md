---
title: "Switching between Default and Custom Schemes of Video Capturing and Encoding"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-100448"
---

<span id="problem-description"></span>
## Problem description

How do I switch between a custom video capture/encoding module and an internal video capture/encoding module during a call?

<span id="question-answer"></span>
## Question answer

In order to enable users to get a smoother video call experience, we do not recommend switching between custom and internal video capture/coding modules after users publish streams. If you need to switch between video capture/coding modules, it is recommended to select manual publish when users join the room.

Refer to the following steps to achieve switching.


1. Stop publishing stream. There are two situations:

   * Streams are automatically published: Since automatic publishing cannot be stopped manually, the user should leave room and select manual publishing when rejoining the room.

   * Streams are manually published: Call `unpublish` to stop publishing.

2. Call `setVideoSourceType` to switch the input video source type.

3. Enable the required video capture/encoding module. Here are the options:

   * [Enable custom video capture](https://docs.byteplus.com/en/docs/12/docs-70138)

   * Enable internal video capture:

   * Android: [startAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70080#startvideocapture)

      * iOS: [startAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70086#startvideocapture)

      * macOS: [startAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70092#startvideocapture)

      * Windows: [startAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70095#startvideocapture)

   * [Enable custom video encoding](https://docs.byteplus.com/en/docs/12/docs-82921). RTC SDK use internal video encoding scheme by default.
