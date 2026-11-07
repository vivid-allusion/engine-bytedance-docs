---
title: "Audio-only or Video-only Live Streams"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/audioonly"
---

BytePlus MediaLive supports audio\-only or video\-only live streams. You can push audio\-only or video\-only live streams to the live stream edge nodes. You can also pull audio\-only or video\-only live streams directly from the live stream edge nodes.

<span id="c89e0453"></span>
## Procedure

<span id="8114c44c"></span>
### Pushing live streams

You can push audio\-only and video\-only live streams that use **RTMP**, **RTMPS**, and **QUIC** protocols.

The types of live streams that you can push will differ depending on your live stream method. The details are as follows.


* Audio\-only live streams: Only regular or audio\-only streams can be pushed.

* Video\-only live streams: Only regular or video\-only streams can be pushed.


<span id="bba6ca8c"></span>
### Pulling live streams

You can pull audio\-only and video\-only live streams that use **RTMP**, **FLV**, and **QUIC** protocols.

You will need to add a query parameter to the [pull stream address](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generating-live-stream-addresses) of the corresponding protocol to set it to audio\-only or video\-only mode.


* Audio\-only: Add the query parameter "only_audio"

   * When `only_audio=1`, the stream will be pulled in audio\-only mode.

   * When `only_audio` is 0 or the parameter is omitted, the stream will be pulled in regular mode.

* Video\-only: Add the query parameter "only_video"

   * When `only_video=1`, the stream will be pulled in video\-only mode. When it is 0 or omitted, the stream will be pulled in regular mode.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning"><code>only_audio</code> and <code>only_video</code> cannot both be 1. If both parameters are 1, neither of them will take effect.</div>


The examples below show the pull stream address formats of audio\-only streams that use RTMP, FLV, and RTM protocols.


* RTMP: `rtmp://{Domain}/{AppName}/{StreamName}?{AuthenticationInfo}&only_audio=1`

* FLV: `https://{Domain}/{AppName}/{StreamName}.flv?{AuthenticationInfo}&only_audio=1`

* RTM: `https://{Domain}/{AppName}/{StreamName}.sdp?{AuthenticationInfo}&only_audio=1`
