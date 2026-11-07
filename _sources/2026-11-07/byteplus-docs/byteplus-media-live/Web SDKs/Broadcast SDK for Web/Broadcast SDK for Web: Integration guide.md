---
title: "Broadcast SDK for Web: Integration guide"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-integrating-the-broadcast-sdk-for-web"
---

By following the Integration Guide, you can seamlessly implement web\-based live streaming using the BytePlus MediaLive Broadcast SDK. This document provides end\-to\-end instructions—from installing the SDK to configuring and broadcasting your stream. It covers camera and microphone setup, sample streaming code, and common FAQs. You can complete the integration in just a few minutes and start streaming audio/video right away.

<span id="be143904"></span>
## Prerequisites

Before integrating the **BytePlus MediaLive Broadcast SDK**, ensure the following:


* **Environment Requirements**:

   * **Streaming URL**: Log in to the [BytePlus MediaLive Console](https://console.byteplus.com/live/main/locationGenerate) and use the address generator to obtain an RTM push stream address.

* **Hardware Setup**:

   * Verify that your devices (e.g., camera, microphone) are properly connected.

   * Grant the browser permission to access the camera, microphone, and screen sharing.

* **Required Tools**:


If using the SDK via **NPM**, ensure that **Node.js** and a package manager are installed.

<span id="e912e634"></span>
## Procedure

<span id="0fb66f1b"></span>
### 1. Import the SDK

You can import the SDK **via CDN** or **via NPM**, depending on your development needs.


* **Via CDN**: Ideal for quick tests or prototypes, with no need for complex build tools.

* **Via NPM**: Best suited for modern development setups using Webpack, Vite, or other build tools.



<Tabs>
<Tab zoneid="X6kGP0g2OM" title="Via CDN">
<TabTitle>Via CDN</TabTitle>

1. Create an `index.html` file.

2. In the HTML file, include the SDK via a `<script>` tag. Once included, it automatically attaches the `LivePusher` class to the global object.


```HTML
<script src="https://sf-unpkg.bytepluscdn.com/obj/byteplusfe-sg/sdk/@byteplus/vepusher/2.0.1/index.umd.js"></script>
```



</Tab>
<Tab zoneid="dMafwbFVgz" title="Via NPM">
<TabTitle>Via NPM</TabTitle>

1. Install the SDK:


```Bash
npm install @byteplus/vepusher@2.0.1 --save
```



2. Import the SDK:


```JavaScript
import LivePusher from '@byteplus/vepusher';
```



</Tab>
</Tabs>


<span id="7c3aca7c"></span>
### 2. Start Live Streaming


1. Initialize the SDK:


```JavaScript
const livePusher = new LivePusher();
```



2. Create a local preview container in your HTML:


```HTML
<div id="preview"></div>
```



3. Bind the preview container and start rendering:


```JavaScript
livePusher.setRenderView('preview');
livePusher.startPreview();
```



4. Optionally set video/audio quality before capturing:


```JavaScript
livePusher.setVideoQuality('720p-1'); // Default video quality
livePusher.setAudioQuality('STANDARD'); // Default audio quality
```



5. Capture media sources. The SDK supports camera, microphone, screen sharing, and more. Once captured, the preview updates automatically:


```JavaScript
livePusher.startCamera();       // Capture camera
livePusher.startMicrophone();   // Capture microphone
```



6. Start pushing the stream. Use the URL from the BytePlus MediaLive console:


```JavaScript
livePusher.startPush('https://{{domain}}/{{appName}}/{{streamName}}.sdp');
```


<span id="5bd75e48"></span>
### 3. End the Live Stream


1. Stop pushing:


```JavaScript
livePusher.stopPush();
```



2. Release media devices (camera/microphone):


```JavaScript
livePusher.stopCamera();
livePusher.stopMicrophone();
```


<span id="3304c6ec"></span>
## FAQ

<span id="75db841d"></span>
### Why did streaming fail?


* Ensure the streaming URL is valid.

* Make sure you have a video track; purely audio\-only streaming is not currently supported.

* Verify that your network bandwidth can handle the push stream.


<span id="bbe22907"></span>
### Why does video lag?


* Check your network for sufficient and stable uplink bandwidth.

* Lower the video quality (e.g., from `720p-1` to `360p`).


<span id="fb5edc19"></span>
## Complete API Documentation

For more details on available methods and parameters, see the [API Documentation](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-overview_1).
