---
title: "Mirroring"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70143"
---

Mirroring a video is a technique that can be used to create interesting visual effects or correct orientation issues in recorded videos. It involves reversing the horizontal direction of each frame in the video so that it appears as if it was reflected by a mirror.

<span id="use-cases"></span>
## Use cases

You can set a mirroring effect for video streams in the following scenarios.


|Industry |Scenarios |
|---|---|
|Online Education |Build realistic, interactive, and engaging virtual classroom sessions, including flashcard learning, gaming activities, and music teaching. |
|Interactive Entertainment |Follow on\-screen directional instructions during interactive sessions. |
|Video Calling |View the speaker's video feed during a call. |
|Tele\-medicine |Provide clearer visual guidance during remote consultations, such as in physical therapy sessions. |


This document explains how to use the RTC SDK to configure video mirroring effects.

<span id="glossary"></span>
## Glossary


* Video preprocessing is the process of applying corrections or effects to video images before encoding or publishing them. It enables you to fix issues like interlacing and noise, adjust colors and brightness, enhance your face, and add fun elements like filters, stickers or virtual backgrounds.

* Local preview mirroring. You see your own image flipped and displayed on your local device, so you can check your appearance and gestures.

* Encoding mirroring. Your image will be flipped during encoding and displayed on the devices of all remote users.

* Remote image mirroring. This setting flips a remote user's video feed only on your local device.


<span id="prerequisite"></span>
## Prerequisite

You have integrated SDK 4.35 or later for audio and video communications.

<span id="limitations"></span>
## Limitations


* The mirroring effect applies to video from camera sources (such as front\-facing, rear, and external cameras).

* This effect doesn’t apply to screen\-sharing videos.

* If you use an external render, you can specify either `MIRROR_TYPE_RENDER_AND_ENCODER (3)` or `MIRROR_TYPE_NONE (0)` as the mirroring type when calling `setLocalVideoMirrorType`. You can’t use `MIRROR_TYPE_RENDER(1)`, which isn’t supported by external renders.


<span id="default-setting"></span>
## Default Setting

See the following table for the default mirroring modes for different video sources and devices.


| |Front\-facing Camera / Webcam |Rear Camera |External Video Sources |
|---|---|---|---|
|Mobile Devices |* Local preview: Mirrored<br><br>* Encoding: Non\-mirrored |* Local preview: Non\-mirrored<br><br>* Encoding: Non\-mirrored |* Local preview: Non\-mirrored<br><br>* Encoding: Non\-mirrored |
|PC |* Local preview: Mirrored<br><br>* Encoding: Non\-mirrored |/ |* Local preview: Non\-mirrored<br><br>* Encoding: Non\-mirrored |


<span id="mirroring-modes"></span>
## Mirroring Modes

Mirror modes supported by the RTC SDK are as follows:


* Enable local preview mirroring

* Enable encoding mirroring

* Enable local preview mirroring and encoding mirroring

* Disable mirroring


<span id="displaying-effect"></span>
### Displaying Effect

The following figure shows how you see people and objects in reality.

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_92407c681ccd5057a71cb3b81362c8c8) </span>

The following table shows what local and remote users will see under different mirroring modes.


|Mirroring Modes |Local Users |Remote Users |
|---|---|---|
|Local preview mirroring |<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_2c647e8aa5a16495e05b8765079ae541.png) </span> |<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_b43b95b0687a6e4c15f84aa44259fd19.png) </span> |
|Enable encoding mirroring |<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_b43b95b0687a6e4c15f84aa44259fd19.png) </span> |<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_2c647e8aa5a16495e05b8765079ae541.png) </span> |
|Local preview and encoding mirroring |<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_2c647e8aa5a16495e05b8765079ae541.png) </span> |<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_2c647e8aa5a16495e05b8765079ae541.png) </span> |
|Disable Mirroring |<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_b43b95b0687a6e4c15f84aa44259fd19.png) </span> |<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_b43b95b0687a6e4c15f84aa44259fd19.png) </span> |


<span id="sticker-display-effects"></span>
### Sticker Display Effects

You can add various effects, including dynamic stickers and virtual backgrounds, to accommodate your needs.

The following figures show how you see people and stickers in reality.


|<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_b43b95b0687a6e4c15f84aa44259fd19.png) </span> |<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_bc00f34344df7e99397957e63b6c11a8.png) </span> |
|---|---|
|People and objects in reality |Smiley sticker added in RTC |


The following table shows the sticker display effects under different mirroring modes.


|Mirroring Modes |Local User |Remote User |Consistency |
|---|---|---|---|
|Local preview mirroring |<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_4019e482af04a387297ae3122c1eb007.png) </span> |<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_5ba9986a03499cc9456e8e5bca3fccf4.png) </span> |No |
|Enable encoding mirroring |<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_4019e482af04a387297ae3122c1eb007.png) </span> |<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_9fdc615c273c4c8e1e9b7e19613cfb5e.png) </span> |No |
|Local preview and encoding mirroring |<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_9fdc615c273c4c8e1e9b7e19613cfb5e.png) </span> |<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_9fdc615c273c4c8e1e9b7e19613cfb5e.png) </span> |Yes |
|Disable Mirroring |<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_5ba9986a03499cc9456e8e5bca3fccf4.png) </span> |<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_5ba9986a03499cc9456e8e5bca3fccf4.png) </span> |Yes |


**Notes**


* If you call `switchCamera` before calling `setLocalVideoMirrorType`, the mirroring mode will be set to the default mode.

   For example, if you switch from the rear camera to the front\-facing camera before calling setLocalVideoMirrorType, the local video frames will be mirrored.

* After you call `setLocalVideoMirrorType`, the mirroring mode will not return to the default mode, even if you `call switchCamera`.


<span id="video-stream-flow"></span>
## Video Stream Flow

The following diagrams illustrate the video stream processing for different mirror modes.


* Local preview mirroring


<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/advancedFeatures/mirrorrender.png) </span>


* Local preview and encoding mirroring


<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/advancedFeatures/mirrorforrenderandencoder.png) </span>

<span id="api-reference"></span>
## API Reference

View API details and parameters here.


|Platform |Android |iOS |macOS |Windows |
|---|---|---|---|---|
|Version |3.29 and later |3.29 and later |3.44 and later |3.29 and later |
|Set mirror mode |[setLocalVideoMirrorType](https://docs.byteplus.com/en/docs/12/docs-70080#setlocalvideomirrortype) |[setLocalVideoMirrorType:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-setlocalvideomirrortype) |[setLocalVideoMirrorType:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCEngine-setlocalvideomirrortype) |[setLocalVideoMirrorType](https://docs.byteplus.com/en/docs/12/docs-70095#setlocalvideomirrortype) |
|Switch camera |[switchCamera](https://docs.byteplus.com/en/docs/12/docs-70080#switchcamera) |[switchCamera:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-switchcamera) |Not supported |Not supported |
