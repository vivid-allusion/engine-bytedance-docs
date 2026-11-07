---
title: "Video Orientation"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-128787"
---

<span id="changelog"></span>
## Changelog

This feature is available in Client SDK v3.45 and later.

<span id="introduction"></span>
## Introduction

By default, video frames from mobile devices contain rotation data that can lead to incorrect rendering in players or misalignment of video effects. This guide explains how to use the `setVideoOrientation` API to process the video frame's rotation angle before encoding. Following the instructions in this document will help you ensure that videos display correctly in all scenarios, including single\-stream media push and custom video preprocessing, providing a consistent user experience.


* In a single\-stream media push, the player cannot process rotation angle information during decoding. As a result, the rendered video frame is displayed without the correct orientation.

* When you enable video effects or use custom video preprocessing on a mobile device, most effects are designed for portrait mode. An uncorrected rotation angle will cause stickers to appear with an incorrect orientation and position.


<span id="prerequisites"></span>
## Prerequisites

You have integrated the RTC SDK for real\-time communications.

<span id="function"></span>
## Function

In the scenarios mentioned above, an uncorrected rotation angle will cause incorrect display effects. To resolve this, call 'setVideoOrientation' to reset the video frame's rotation angle to 0 before custom video processing and encoding. The adjusted video frame is then passed through the entire RTC link. For single\-stream media push scenarios, we recommend setting the video frame orientation to either 'Portrait' or 'Landscape' mode, depending on your use case. When enabling video effects or using custom video preprocessing on a mobile device, we recommend setting the video frame orientation to 'Portrait' mode.

In the images below, "Status Bar" refers to the mobile device's system status bar, and "Sticker" refers to an applied video effect sticker.

<span id="adaptive-mode"></span>
### Adaptive mode

This mode does not support single\-stream media push, video effect stickers, or custom video preprocessing.


|Render |Capture Device (Portrait) |Capture Device (Landscape) |
|---|---|---|
|Local render |<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_ef636f5699ffef199eee200bd7447042) </span> |<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_1d37837f02a58a20cf10deaaee4dabef) </span> |
|Remote render |<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_09e5112fb7f23d1bfde2a011e0efa354) </span> |<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_88864ccce29adc3e905b946b7776855d) </span> |


<span id="portrait-mode"></span>
### Portrait mode


|Render |Capture Device (Portrait) |Capture Device (Landscape) |
|---|---|---|
|Local render |<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_3225aaeb3332ce1e95625d627e194dad) </span> |<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_dbea32e9d96caa71203b4ca66526cbcd) </span> |
|Remote render |<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_75ee3c6e7ed9744b3f999f8c508419dd) </span> |<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_9b0791612c674ac2b4d8890bdaa0f732) </span> |
|Single\-stream media push player |<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_b52c23ee4212b56c18513b7629e5e648) </span> |<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_601b2b08dd2a9f4eed3f45639abdec12) </span> |


<span id="landscape-mode"></span>
### Landscape mode


|Render |Capture Device (Portrait) |Capture Device (Landscape) |
|---|---|---|
|Local render |<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_938469b7cab0346abe6e18aeb06c0a4c) </span> |<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_e30ca2c83f1fe563f3122716194836fa) </span> |
|Remote render |<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_3d9cf5dc17844163cff208a80c4f2c64) </span> |<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_18dea6ff08f7e2507b6045a3640326b4) </span> |
|Single\-stream media push player |<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_35a179e5959e6a916cc4d28ac6d7a9e5) </span> |<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_18dea6ff08f7e2507b6045a3640326b4) </span> |


<span id="api-reference"></span>
## API Reference


* Android

   * [setVideoOrientation](https://docs.byteplus.com/en/docs/12/docs-70080#setvideoorientation)

* iOS

   * [setVideoOrientation:](https://docs.byteplus.com/en/docs/12/docs-70086#setvideoorientation)
