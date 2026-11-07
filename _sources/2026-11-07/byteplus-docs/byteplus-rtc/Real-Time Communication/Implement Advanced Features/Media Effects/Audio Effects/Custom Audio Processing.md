---
title: "Custom Audio Processing"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-80635"
---

To apply custom audio effects or perform other processing on audio data, you can integrate a custom audio frame processor with the RTC SDK. This guide explains how to register your processor to handle audio frames before they are encoded and transmitted to remote users.

<span id="prerequisites"></span>
## Prerequisites

Integrate the RTC SDK for audio and video communications in your project.

<span id="process-a-custom-audio-source-on-android"></span>
## Process a custom audio source on Android


1. Create your audio processor by implementing the `IAudioFrameProcessor` interface according to your business needs.

2. Call `registerAudioProcessor` to use the audio processor.


To disable the audio processing, call `registerAudioProcessor` and set the parameter to `null`.

**Notes**


* For compatibility with the RTC SDK, your audio processor should support the sample rate and number of audio channels specified in the API reference.

* You must not alter the audio format or the number of samples per frame.


<span id="api-reference"></span>
## API Reference

View API details and parameters here.


* Android:

   * [IAudioFrameProcessor](https://docs.byteplus.com/en/docs/12/docs-70081#iaudioframeprocessor)

   * [registerAudioProcessor](https://docs.byteplus.com/en/docs/12/docs-70080#registeraudioprocessor)

* iOS:

   * [onProcessRecordAudioFrame:](https://docs.byteplus.com/en/docs/12/docs-70085#onprocessrecordaudioframe)

   * [registerAudioProcessor:](https://docs.byteplus.com/en/docs/12/docs-70086#registeraudioprocessor)

* Windows:

   * [onProcessRecordAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70096#IAudioFrameProcessor-onprocessrecordaudioframe)

   * [registerAudioProcessor](https://docs.byteplus.com/en/docs/12/docs-70095#registeraudioprocessor)

* macOS:

   * [onProcessRecordAudioFrame:](https://docs.byteplus.com/en/docs/12/docs-70093#onprocessrecordaudioframe)

   * [registerAudioProcessor:](https://docs.byteplus.com/en/docs/12/docs-70092#registeraudioprocessor)
