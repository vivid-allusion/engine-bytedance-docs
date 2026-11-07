---
title: "Custom Audio and Video Capturing (Web)"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-128914"
---

Generally, BytePlus RTC uses default audio & video modules for video capturing and rendering. However, these default modules might not meet your requirements, such as in the following scenarios:


* Your app has its own video capturing and rendering modules;

* You want to use video from other sources, such as screen recordings;

* You want to perform pre\-transmission processing on the captured audio and video, such as image enhancement;

* The video capture device is already in use.


In these scenarios, you can use the RTC SDK to encode and transmit a custom video source.

<span id="get-custom-audio-and-video-source"></span>
## Get custom audio and video sources

<span id="media-stream-captured-by-custom-device"></span>
### Media stream from a custom device

Get the custom audio/video source via [getUserMedia](https://developer.mozilla.org/en-US/docs/Web/API/MediaDevices/getUserMedia).

```typescript
const stream = new navigator.mediaDevices.getUserMedia({
    video: true,
    audio: true
});
//Get custom video track and audio track
const videoTrack = stream.getVideoTracks()[0];
const audioTrack = stream.getAudioTracks()[0];
```


<span id="animation-in-the-canvas"></span>
### Animation in the Canvas

Get the animation in the Canvas via [captureStream](https://developer.mozilla.org/en-US/docs/Web/API/HTMLCanvasElement/captureStream).

```typescript
const canvas = document.getElementById('your-canvas-element-ID');

const stream = canvas.captureStream();
const videoTrack = stream.getVideoTracks()[0];
```


<span id="media-element-being-played"></span>
### Media element being played

Get the media element being played via [captureStream](https://developer.mozilla.org/en-US/docs/Web/API/HTMLMediaElement/captureStream).

```typescript
const video = document.getElementById('your-video-element-ID');

const stream = video.captureStream();
const audioTrack = stream.getAudioTracks()[0];
const videoTrack = stream.getVideoTracks()[0];
```


<span id="switch-video-input-to-external-source"></span>
## Switch video input to external source


1. By default, the RTC SDK uses the internal capturing module. Call [setVideoSourceType](https://docs.byteplus.com/en/docs/12/docs-104478#setvideosourcetype) to switch the video source to external capturing module `VIDEO_SOURCE_TYPE_EXTERNAL`.


```typescript
engine.setVideoSourceType(
    BytePlusRTC.StreamIndex.STREAM_INDEX_MAIN, 
    BytePlusRTC.VideoSourceType.VIDEO_SOURCE_TYPE_EXTERNAL
);
```



2. Call [setExternalVideoTrack](https://docs.byteplus.com/en/docs/12/docs-104478#setexternalvideotrack) to pass the external video track to the SDK.


```typescript
// Pass the custom video track to the SDK
engine.setExternalVideoTrack(
    StreamIndex.STREAM_INDEX_MAIN,
    videoTrack
);
```


<span id="switch-audio-input-to-external-source"></span>
## Switch audio input to external source


1. By default, the RTC SDK uses the internal capturing module. Call [setAudioSourceType](https://docs.byteplus.com/en/docs/12/docs-104478#setaudiosourcetype) to switch the audio source to external capturing module `AUDIO_SOURCE_TYPE_EXTERNAL`.


```typescript
engine.setAudioSourceType(
    BytePlusRTC.StreamIndex.STREAM_INDEX_MAIN, 
    BytePlusRTC.AudioSourceType.AUDIO_SOURCE_TYPE_EXTERNAL
);
```



2. Call [setExternalAudioTrack](https://docs.byteplus.com/en/docs/12/docs-104478#setexternalaudiotrack) to pass the external audio track to the SDK.


```typescript
// Pass the custom audio track to the SDK
engine.setExternalAudioTrack(
    StreamIndex.STREAM_INDEX_MAIN,
    audioTrack
);
```
