---
title: "Custom Audio Capturing and Rendering (Native)"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-96197"
---

RTC SDK includes audio modules for capturing and rendering. However, these default modules might not meet your needs, such as in the following scenarios:


* Audio capture and rendering modules already exist in your audio & video applications;

* You want to process the captured audio and video data before transmission.

* Your audio capture device is in use by another application.


This guide provides the complete workflow and API calls required to push your own captured audio data to the SDK and pull remote audio data for custom local rendering.

<span id="prerequisites"></span>
## Prerequisites

You have integrated RTC SDK v3.40 or later into your project.

You are familiar with the process of building a video app using the RTC SDK.

<span id="procedure"></span>
## Procedure

The following steps use Android as an example to show how to implement custom audio capture and rendering.

<span id="custom-audio-capture"></span>
### Custom Audio Capture


1. Call `setAudioSourceType` to enable custom audio capture.

2. Capture audio and process the data.

3. Call `pushExternalAudioFrame` every 10 ms to provide the SDK with the processed audio data.


To switch back to the internal capture mode, call `setAudioSourceType` and then `startAudioCapture`.

<span id="custom-audio-rendering"></span>
### Custom Audio Rendering


1. Call `setAudioRenderType` to enable custom audio rendering.

2. After joining the room, call `pullExternalAudioFrame` every 10 ms to retrieve remote audio data.

3. Render the pulled audio data locally.


<span id="limitations"></span>
## Limitations

To use custom audio capture and rendering, you will also need to apply your own 3A processing to the audio.

<span id="api-reference"></span>
## API Reference


* Android

   * [setAudioSourceType](https://docs.byteplus.com/en/docs/12/docs-70080#setaudiosourcetype)

   * [setAudioRenderType](https://docs.byteplus.com/en/docs/12/docs-70080#setaudiorendertype)

   * [pushExternalAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70080#pushexternalaudioframe)

   * [pullExternalAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70080#pullexternalaudioframe)

* iOS

   * [setAudioSourceType:](https://docs.byteplus.com/en/docs/12/docs-70086#setaudiosourcetype)

   * [setAudioRenderType:](https://docs.byteplus.com/en/docs/12/docs-70086#setaudiorendertype)

   * [pushExternalAudioFrame:](https://docs.byteplus.com/en/docs/12/docs-70086#pushexternalaudioframe)

   * [pullExternalAudioFrame:](https://docs.byteplus.com/en/docs/12/docs-70086#pullexternalaudioframe)

* Windows

   * [SetAudioSourceType](https://docs.byteplus.com/en/docs/12/docs-70095#setaudiosourcetype)

   * [SetAudioRenderType](https://docs.byteplus.com/en/docs/12/docs-70095#setaudiorendertype)

   * [PushExternalVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70095#pushexternalvideoframe)

   * [PullExternalAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70095#pullexternalaudioframe)

* Linux

   * [setAudioSourceType](https://docs.byteplus.com/en/docs/12/docs-85516#setaudiosourcetype)

   * [setAudioRenderType](https://docs.byteplus.com/en/docs/12/docs-85516#setaudiorendertype)

   * [pushExternalAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85516#pushexternalaudioframe)

   * [pullExternalAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85516#pullexternalaudioframe)
