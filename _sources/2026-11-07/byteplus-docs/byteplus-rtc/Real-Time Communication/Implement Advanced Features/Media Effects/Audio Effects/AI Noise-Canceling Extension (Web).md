---
title: "AI Noise-Canceling Extension (Web)"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-148647"
---

In real\-time audio and video calls, background noise can degrade call quality. The RTC SDK provides two noise reduction methods: browser's built\-in noise cancellation and AI noise\-canceling extension.

<span id="try-it-online"></span>
## **Try it Online**

We offer a web\-based demo that allows you to experience the feature without writing any code. [Try It Now](https://demo.byteplus.com/rtc/advance/aians)

<span id="choose-a-noise-reduction-method"></span>
## Choose a noise reduction method


|Noise Type |Characteristics |Recommended Method(s) |
|---|---|---|
|Steady Noise |Consistent and stable background noise, like the hum of an air conditioner, fan, or electronic device. |Browser's built\-in noise cancellation<br><br>AI noise\-canceling extension |
|Non\-steady Noise |Noise that is unpredictable in timing or loudness, such as keyboard typing, object collisions, and other sudden sounds. |AI noise\-canceling extension |


<span id="method-1-use-the-browser-s-built-in-noise-cancellation-feature"></span>
## Method 1: Use the browser's built\-in noise cancellation feature

To reduce steady noise you need to set `noiseSuppression`, `echoCancellation`, and `autoGainControl` to `true` using [setAudioCaptureConfig](https://docs.byteplus.com/en/docs/12/docs-104478#setaudiocaptureconfig) before initiating audio capture and publishing the stream.

> Refer to [MediaTrackConstraints](https://developer.mozilla.org/en-US/docs/Web/API/MediaTrackConstraints) for the complete description for the parameters.


```typescript
// Make sure to configure before calling startAudioCapture() and publishStream().
await engine.setAudioCaptureConfig({
    noiseSuppression: true,
    echoCancellation: true,
    autoGainControl:true,
});

await engine.startAudioCapture();
await engine.publishStream(MediaType.AUDIO);
```


<span id="method-2-use-ai-noise-canceling-extension"></span>
## Method 2: Use AI noise\-canceling extension

<span id="prerequisites"></span>
### Prerequisites


* You have integrated the RTC Web SDK 4.47 or a later version.

* You have implemented the real\-time voice call feature using the RTC SDK, and the local audio must be captured by the RTC SDK, not by an external audio collector.

* Supported browsers for PC:

   * Chrome 94+

   * Edge 94+

   * Firefox 80+

   * Safari 14.1+

* For best performance, the following specifications are recommended.

   * Dual\-core Intel Core i5+

   * 8 GB+ of RAM

   * 64\-bit operating system


<span id="procedures"></span>
### Procedures


1. Import the AI noise\-canceling extension into your project using either of the following methods:

   * Direct import

> Make sure to import the extension from the same source as the RTC SDK to prevent any version conflicts.


```typescript
import RTCAIAnsExtension from '@byteplus/rtc/extension-ainr';
```


   * UMD import (Supported in v4.51.1 and later)

   ```typescript
   const {RTCAinrExtension} = window.BytePlusRTCExtensions;
   ```
   

2. Initialize the plugin and check for browser compatibility.

   ```typescript
   // Create a plugin instance
   const AIAnsExtension = new RTCAIAnsExtension();
   
    // Check if the current browser environment supports the AI noise-canceling extension
   const isSupported = await AIAnsExtension.isSupported();
   ```
   

3. Register the AI plugin and set up event listeners.


```typescript
import BytePlusRTC from '@byteplus/rtc';
// Import the AI noise-canceling extension.
import RTCAIAnsExtension from '@byteplus/rtc/extension-ainr';
// Create an IRTCEngine instance.
const engine = BytePlusRTC.createEngine('appid');

// Create an AI noise-canceling extension instance.
const AIAnsExtension = new RTCAIAnsExtension();
// Register the AI noise-canceling extension.
try {
  await engine.registerExtension(AIAnsExtension);
} catch (error) {
  // Failed to register. See error.message.
}
AIAnsExtension.on(AIAnsEventTypes.onUnsupported, ({message}) => {
  // Handle cases where the extension is not supported. See `message`.
})
AIAnsExtension.on(AIAnsEventTypes.onOverload, ({elapsedTime}) => {
  // The system load is too high, causing high processing latency for the plugin. 
  // Consider lowering the mode or disabling the plugin.
})
AIAnsExtension.on(AIAnsEventTypes.onError, ({message}) => {
  // The plugin encounters an error during runtime. See `message` for details.
  // Based on the error, consider resuming or disabling the plugin.
  AIAnsExtension.resume();
})
```



4. Turn on internal audio capture.


```typescript
engine.startAudioCapture();
```



5. Enable/disable AI noise cancellation.

   You can enable/disable the extension during a call. It will take effect immediately.

* Since V4.65, you can specify the audio stream to be processed by the extension.

   ```typescript
   // Enable AI noise cancellation for the external screen stream.
   AIAnsExtension.enable({
     streamIndex: StreamIndex.STREAM_INDEX_SCREEN,
     sourceType: AudioSourceType.AUDIO_SOURCE_TYPE_EXTERNAL,
   });
   // Disable AI noise cancellation for the local audio stream.
   AIAnsExtension.disable({
     streamIndex: StreamIndex.STREAM_INDEX_MAIN,
     sourceType: AudioSourceType.AUDIO_SOURCE_TYPE_INTERNAL,
   });
   ```
   

* By default, the extension will process the audio stream captured by the RTC SDK from the local microphone. This is the default behavior if you do not specify an audio stream, and it is the only behavior in versions earlier than V4.65.

   ```typescript
   // Enable AI noise cancellation.
   AIAnsExtension.enable();
   // Disable AI noise cancellation.
   AIAnsExtension.disable();
   ```
   

5. Set the AI noise cancellation intensity.


```typescript
// Auto mode.
await AIAnsExtension.setAnsMode(AnsMode.AUTO);
```


The following table describes the AI noise cancellation intensity.


|Intensity |Value |Description |
|---|---|---|
|LOW |`'low'` |Use for minor or subtle steady noise. |
|MEDIUM |`'medium'` |Use for consistent and stable background noise, such as the hum of an air conditioner, fan, or electronic device. |
|HIGH |`'high'` |For non\-steady noise, such as keyboard typing, object collisions, and other sudden sounds. |
|AUTO |`'auto'` |The AI noise cancellation intensity is automatically adjusted based on the environment. |


<span id="more-operations"></span>
## More operations

<span id="using-both-noise-reduction-methods"></span>
### Using both noise reduction methods

If both noise reduction methods are required, the traditional noise reduction parameters set by [MediaTrackConstraints](https://developer.mozilla.org/en-US/docs/Web/API/MediaTrackConstraints) take effect as follows:


|Extension status |`autoGainControl` |`echoCancellation` |`noiseSuppression` |
|---|---|---|---|
|When the extension has been registered but not enabled. |Effective |Effective |Always `true` |
|When the extension has been registered and enabled. |Always `true` |Effective |Always `false` |


<span id="improve-extension-performance-by-disabling-resampling"></span>
### Improve extension performance by disabling resampling

By default, the AI noise\-canceling extension processes audio streams at a 48kHz sample rate with a frame size of 480 samples, and resampling is enabled to meet these requirements. If your source audio stream already meets these specifications, you can disable resampling to achieve better performance.

```typescript
const AIAnsExtension = new RTCAIAnsExtension({
  resample: false,
});
```
