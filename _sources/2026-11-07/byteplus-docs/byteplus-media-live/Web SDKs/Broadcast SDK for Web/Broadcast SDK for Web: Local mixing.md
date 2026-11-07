---
title: "Broadcast SDK  for Web: Local mixing"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-local_mixing"
---

Below is a step\-by\-step guide on how to use the **BytePlus MediaLive Broadcast SDK** to perform **local mixing** of multiple video streams (e.g., camera, screen sharing) and multiple audio streams (e.g., microphone, system audio). By leveraging local mixing, you can:


* **Reduce Bandwidth Usage**: Merge multiple streams locally into a single outgoing stream, minimizing uplink bandwidth consumption.

* **Customize Layout**: Freely adjust each video’s size, position, and layering.

* **Flexible Audio Management**: Mix different audio sources and control individual volumes.


<span id="922d04f5"></span>
## How It Works

In the **BytePlus MediaLive Broadcast SDK**, how audio and video are handled depends on whether **local mixing** is enabled. The SDK provides two modes:


* **Default Mode (Local Mixing Disabled, Automatic Merging)** 

   * **Use Case**: Simple streaming with only a camera and microphone.

   * **Behavior**:

      * The captured audio and video streams **are automatically included** in the outgoing stream—no manual action needed.

      * The SDK handles audio/video mixing internally and pushes the final stream to the server.

* **Local Mixing Mode (Manual Stream Management)** 

   * **Use Case**: Multiple video sources (e.g., camera + screen sharing) or more complex audio mixing (e.g., microphone + system audio).

   * **Behavior**:

      * The captured audio and video streams **are not automatically included** in the outgoing stream. You must manually add them.

      * You need to call:

         * `addVideoStream()` to add video tracks to the mixing canvas.

         * `addAudioStream()` to add audio tracks to the mixer.


<span id="962898ec"></span>
## Prerequisites


* You have followed the [Integration Guide](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-integrating-the-broadcast-sdk-for-web) to complete SDK initialization and obtained the `livePusher` object.

* You have logged in to the [BytePlus MediaLive console](https://console.byteplus.com/live/main/locationGenerate) to generate an RTM push stream address.


<span id="6d5c9766"></span>
## Procedure


1. **Enable Local Mixing**


Before starting the push stream, call the following method to enable local mixing so that the SDK can combine multiple audio and video streams:

```JavaScript
livePusher.enableMixing(true);
```



2. **Configure Mixing Properties**


Use the `setMixingConfig` method to specify the mixed video resolution, frame rate, background color, and other properties:

```JavaScript
livePusher.setMixingConfig({
  width: 1080,               // Width of the mixing canvas
  height: 720,               // Height of the mixing canvas
  frameRate: 30,             // Frame rate of the merged video
  backgroundColor: '#000000',// Background color of the canvas
});
```



3. **Capture Multiple Media Sources**


Once local mixing is enabled, captured sources will not automatically be added to the stream. You must manually add each source’s ID to the mixing canvas or audio mixer. Below is an example of how to capture camera, screen sharing, and microphone streams:

```JavaScript
const cameraStreamId = await pushClient.startCamera();
const screenStreamId = await pushClient.startScreenCapture();
const micStreamId = await pushClient.startMicrophone();
```



* These methods may trigger browser permission prompts. Ensure the user grants access to the camera and microphone.

* Screen sharing implementations vary among browsers. Handle permissions and compatibility based on your target browsers.

4. **Manually Add Streams to the Mixing Session**


In local mixing mode, streams are not added automatically. You must explicitly add them:


* **Add Video Streams to the Mixing Canvas**

   ```JavaScript
   livePusher.addVideoStream([{
     streamId: screenStreamId,
     width: 1280,
     height: 720,
     x: 1280 / 2,
     y: 720 / 2,
     zOrder: 1,
     keepRatio: true,
   }, {
     streamId: cameraStreamId,
     width: 320,
     height: 180,
     x: 320 / 2,
     y: 180 / 2,
     zOrder: 2,
     keepRatio: true,
   }]);
   ```
   

   * `x` and `y` define the position of the video relative to the top\-left corner of the canvas. The video’s reference point is its center.

   * `zOrder` controls layering; higher numbers appear in front of lower numbers.

   * When `keepRatio` is set to `true`, the original aspect ratio of the video is preserved during scaling.

* **Add Audio Streams to the Mixer**

   ```JavaScript
   livePusher.addAudioStream({
     streamId: micStreamId,
     volume: 100,
   });
   ```
   

   * For multiple audio sources (e.g., external files or custom audio sources), call `addAudioStream` separately for each source.

   * Use `volume` to adjust the initial volume for each audio stream.

5. **Start Streaming**


Finally, call the `startPush` method and provide the push stream address (generated through the console) to begin the live push:

```JavaScript
livePusher.startPush('https://{{domain}}/{{appName}}/{{streamName}}.sdp');
```
