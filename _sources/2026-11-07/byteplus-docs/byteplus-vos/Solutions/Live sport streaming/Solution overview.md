---
title: "Solution overview"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/docs-live-sport-streaming-solution-overview"
---

The Live Sport Streaming solution delivers a sports live\-viewing experience built on BytePlus MediaLive. It combines low\-latency stream pulling, adaptive bitrate (ABR) playback, and multi\-camera angle switching with real\-time interactions such as gifts, comments, and likes, so you can build an engaging second\-screen experience for live matches and events.

<span id="ls-billing"></span>
## Billing

This solution incurs fees for live streaming services. For details, refer to [BytePlus MediaLive pricing overview](https://docs.byteplus.com/en/byteplus-media-live/docs/overview-1).

<span id="ls-highlights"></span>
## Highlights


* **Multi\-camera angle switching**: The demo provides multiple camera feeds for the same event, so viewers can switch between angles during a live match.

* **Adaptive bitrate (ABR) playback**: Each stream is published at multiple quality tiers (from ultra\-high definition down to low definition), and the player can automatically switch quality based on network conditions.

* **Low\-latency streaming protocols**: The solution supports RTM, low\-latency FLV, standard FLV, HLS, and RTMP(S), letting you balance latency, compatibility, and cost per scenario.

* **Interactive viewing**: Viewers can send gifts, post comments and bullet comments (danmaku), and send likes, with a dedicated landscape mode for fullscreen viewing.

* **Latency, quality, and cost comparison**: A built\-in comparison tool demonstrates the trade\-offs between streaming protocols (latency), image\-enhancement processing, and codec choice (H.265 vs. H.264) for cost saving.


<span id="ls-architecture"></span>
## Architecture

The client pulls the live stream from the BytePlus MediaLive CDN and renders it with the BytePlus MediaLive player. For each event, the demo maintains a list of camera channels; every channel can be pulled over different protocols and at different quality tiers. When a viewer switches camera or quality, the client re\-binds the player to the corresponding pull URL. Interactive events (gifts, comments, likes) are layered on top of the playback view.

<span id="ls-protocols"></span>
### Supported streaming protocols

The demo supports the following protocols for stream pulling:


|**Protocol** |**Typical use** |
|---|---|
|RTM |Ultra\-low\-latency real\-time viewing |
|FLV (low latency) |Low\-latency viewing over FLV |
|FLV |Standard\-latency viewing with broad compatibility |
|HLS |High compatibility, higher latency |
|RTMP |Secure streaming over RTMP |


<span id="ls-comparison"></span>
### Comparison experiences

The demo includes a comparison view that plays two streams side by side to illustrate three trade\-offs:


* **Low latency**: Compares the end\-to\-end delay of different pull protocols (for example, RTM against low\-latency FLV) for the same source.

* **Image enhancement**: Compares an enhanced stream (super\-resolution and sharpening) against the original stream from the same source.

* **Cost saving**: Compares an H.265 (HEVC) stream against an H.264 stream, at either the same quality or the same bitrate, to show the bandwidth savings of H.265.


<span id="ls-implementation"></span>
## Implementation

For implementation details, see the following topics:


* [Implementing live sport streaming for Android](https://docs.byteplus.com/docs/byteplus-vos/docs-implementing-live-sport-streaming-for-android)

* [Implementing live sport streaming for iOS](https://docs.byteplus.com/docs/byteplus-vos/docs-implementing-live-sport-streaming-for-ios)
