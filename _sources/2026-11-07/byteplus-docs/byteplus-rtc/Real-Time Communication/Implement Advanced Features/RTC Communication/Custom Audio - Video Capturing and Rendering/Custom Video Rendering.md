---
title: "Custom Video Rendering"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-81201"
---

RTC provides internal modules for video rendering when you use the service. However, these default modules might not meet your needs, such as in the following scenarios:


* Your application already has custom video rendering modules, for example, in game development.

* You want to process the video frame before rendering, such as storing it as a picture, adding video effects, etc.


<span id="prerequisites"></span>
# Prerequisites

You have integrated the RTC SDK, v3.25 or a later version for basic audio & video calling.

You are familiar with building a video app with the RTC SDK.

<span id="introduction"></span>
# Introduction

Render the video images captured locally by the RTC SDK or the video images from remote users through a custom rendering module.

> Note: The steps are similar across platforms, but interface and parameter names may differ. This guide uses the Android RTC SDK as an example. For details on other platforms, refer to their respective API references.


<span id="step-1-build-a-custom-renderer"></span>
## Step 1: Build a custom renderer

To build a custom renderer, create a class that inherits from [IVideoSink](https://docs.byteplus.com/en/docs/12/docs-70083#ivideosink) and implement your custom rendering logic.

> Note: Due to hardware differences, video frames received via `IVideoSink.onFrame` may be presented at a certain angle. You can call `RTCVideoFrame.getRotation` to get the angle and process it with the custom renderer.


<span id="step-2-bind-a-custom-renderer"></span>
## Step 2: Bind a custom renderer

After getting the video stream, bind the video stream to the custom renderer. Specify the pixel format for the video data using the `requidFormat` parameter.


* Local video rendering


Call the `setLocalVideoSink` to specify a custom renderer for the local media stream. When the device starts capturing, video frames will be transmitted to the custom rendering module via `IVideoSink.onFrame`.

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/%E9%AB%98%E7%BA%A7%E5%8A%9F%E8%83%BD/RTC_Communication/custom-video-rendering-local.png) </span>


* Remote video rendering


Call `setRemoteVideoSink` to specify a custom renderer for the remote media stream. Get the required media stream parameters from the `onStreamAdd` callback. When a user joins the room and subscribes to the remote video stream, video frames are transmitted to the custom rendering module through `IVideoSink.onFrame`.

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/%E9%AB%98%E7%BA%A7%E5%8A%9F%E8%83%BD/RTC_Communication/custom-video-rendering-remote.png) </span>

<span id="step-3-unbind-the-custom-renderer"></span>
## Step 3: Unbind the custom renderer

Call the corresponding interface mentioned in step 2 and set `videoSink` to `null`. After unbinding, video frames are rendered by the SDK's default renderer.

<span id="api-reference"></span>
# API Reference


|Function/Platform |Android |iOS |macOS |Windows |
|---|---|---|---|---|
|Bind local video source to custom renderer |[setLocalVideoSink](https://docs.byteplus.com/en/docs/12/docs-70080#setlocalvideosink-2) |[setLocalVideoSink:withLocalRenderConfig:](https://docs.byteplus.com/en/docs/12/docs-70086#setlocalvideosink-withlocalrenderconfig) |[setLocalVideoSink:withLocalRenderConfig:](https://docs.byteplus.com/en/docs/12/docs-70092#setlocalvideosink-withlocalrenderconfig) |[setLocalVideoSink](https://docs.byteplus.com/en/docs/12/docs-70095#setlocalvideosink-2) |
|Start internal video capturing |[startVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70080#startvideocapture) |[startVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70086#startvideocapture) |[startVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70092#startvideocapture) |[startVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70095#startvideocapture) |
|Bind remote video source to external renderer |[setRemoteVideoSink](https://docs.byteplus.com/en/docs/12/docs-70080#setremotevideosink-2) |[setRemoteVideoSink:withSink:withPixelFormat:](https://docs.byteplus.com/en/docs/12/docs-70086#setremotevideosink-withsink-withpixelformat) |[setRemoteVideoSink:withSink:withPixelFormat:](https://docs.byteplus.com/en/docs/12/docs-70092#setremotevideosink-withsink-withpixelformat) |[setRemoteVideoSink](https://docs.byteplus.com/en/docs/12/docs-70095#setremotevideosink-2) |
