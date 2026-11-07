---
title: "Broadcast SDK for Web: SDK overview"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-introduction-to-the-broadcast-sdk-for-web"
---

BytePlus MediaLive Broadcast SDK is specially designed for live streaming scenarios, helping streamers smoothly send audio and video content captured from their browsers to the video live streaming server. It supports a variety of streaming scenarios, including camera streaming, screen sharing, online video streaming, local video mixing, and audio mixing. With [BytePlus MediaLive's streaming service](https://www.byteplus.com/en/product/medialive), you can quickly enable live streaming capabilities on the web.

<span id="912d74c3"></span>
## Protocol support

The Broadcast SDK supports streaming content encoded in H.264 using the RTM protocol.

<span id="7ecc10a5"></span>
## Browser support

We recommend that you use the **latest stable version** of a web browser to enhance your live streaming experience.


|**Platform** ||**Chrome 70 and Higher** |**Edge 83 and Higher** |**Safari 12 and Higher** |**Firefox 80 and Higher** |
|---|---|---|---|---|---|
|PC |Windows 10 |Supported<br><br>(Screen sharing requires Chrome 74 or higher.) |Supported<br><br>(Screen sharing requires Edge 99 or higher.) |Not supported |Supported |
||macOS 15 |Supported<br><br>(Screen sharing requires Chrome 74 or higher.) |Supported |Supported<br><br>(Screen sharing requires Safari 13 or higher.) |Supported |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">You can use the Broadcast SDK for Web on mobile devices. We recommend using the latest stable version of Chrome.</div>


* <div data-tips="true" data-tips-type="tip">You can use the Broadcast SDK for Web in Electron, but the Chromium version used by Electron cannot be lower than the minimum version required for desktop Chrome.</div>



<span id="a26cb472"></span>
## Features

BytePlus MediaLive Broadcast SDK supports various streaming scenarios, including:


* Camera Streaming: Supports streaming video and audio captured from the camera to the server.

* Microphone Streaming: Supports capturing and streaming audio from the microphone.

* Screen Sharing: Supports streaming screen content as video.

* Local/Online Video Streaming: Supports streaming from local video files and online video sources.

* Local Video Mixing: Supports mixing multiple video streams locally, with built\-in templates and customizable mixing parameters.


<span id="bc9faa42"></span>
## Limitations

Streams pushed using the Broadcast SDK are not currently supported for LL\-HLS playback.
