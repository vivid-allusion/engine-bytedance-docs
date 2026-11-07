---
title: "Screen Sharing on Web"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-80226"
---

Screen sharing lets you show your screen to remote users. You can use screen sharing to share slides or documents with others during video conferences.

<span id="prerequisites"></span>
## Prerequisites


1. You have integrated the web SDK and implemented [real-time communications](https://docs.byteplus.com/en/docs/12/docs-106914).

2. Browser requirements:

* Chrome 74 or later

* Firefox 66 or later

* Edge 99 or later

* Safari 13 or later

> To share your screen, use a PC browser and the latest version of Chrome.


<span id="to-share-the-screen-on-a-pc"></span>
## To share the screen on a PC

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/advancedFeatures/80266_api_en.png) </span>

<span id="optional-step-1-set-the-encoding-configuration"></span>
### [Optional] Step 1: Set the encoding configuration

Call [setScreenEncoderConfig](https://docs.byteplus.com/en/docs/12/docs-104478#setscreenencoderconfig) to set the encoding configuration of the screen\-sharing stream, which is also applied in video capture. We recommend that you set the encoding configuration before video capture. Otherwise, the video will be captured based on the default configuration (1080p@15fps). If the configuration is not supported by your browser, the video will be captured based on the supported configuration. You will also receive the callback [onLocalVideoSizeChanged](https://docs.byteplus.com/en/docs/12/docs-104479#onlocalvideosizechanged).

```typescript
setScreenEncoderConfig(config:{ 
   width: number,
   height: number,
   frameRate: number,
   maxKbps:number,
   // You can only set contentHint on Chrome. 
   contentHint?: 'text' | 'motion' | 'detail',   
   }
)
```


Set the recommended parameters in the following scenarios:


|Scenario |Resolution (WxH) |Framerate (fps) |Bitrate (kbps) |Note |
|---|---|---|---|---|
|Share static content like slides and Word files |1920 x 1080 |5 |2000 | |
|Share dynamic content like videos |1920 x 1080 |30 |4000 |For optimal results, share your Chrome tab. |


> You can only set the resolution to a lower level after the initial capture. To increase the resolution, recapture your screen.


<span id="step-2-start-capturing-and-sharing-screen-streams"></span>
### Step 2: Start capturing and sharing the screen stream.


1. Call [startScreenCapture](https://docs.byteplus.com/en/docs/12/docs-104478#startscreencapture) to start screen capture.

2. Call [publishScreen](https://docs.byteplus.com/en/docs/12/docs-104478#publishscreen) to start publishing the screen stream.


```javascript
await IRTCEngine.startScreenCapture({
enableAudio: true,// To share audio when sharing the screen.
});
await IRTCEngine.publishScreen(MediaType.AUDIO_AND_VIDEO);
```



3. Stop publishing the screen stream.


```javascript
await IRTCEngine.unpublishScreen(MediaType.AUDIO_AND_VIDEO);
```


<span id="step-3-subscribe-to-and-play-screen-streams"></span>
### Step 3: Subscribe to and play screen streams


1. After receiving [onUserPublishScreen](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onuserpublishscreen), call [subscribeScreen](https://docs.byteplus.com/en/docs/12/docs-104478#subscribescreen) to subscribe to the screen stream.

2. After receiving [onUserPublishScreen](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onuserpublishscreen), call [setRemoteVideoPlayer](https://docs.byteplus.com/en/docs/12/docs-104478#setremotevideoplayer) to set the player for the remote audio and video stream.

> When the host shares their screen, you should switch their camera to a lower\-resolution stream for display in a small window.


```typescript
IRTCEngine.on(IRTCEngine.events.onUserPublishScreen, async ({ userId, mediaType }) =>{
// Subscribe to the remote screen stream after receiving the onUserPublishScreen callback. await IRTCEngine.subscribeScreen(userId, mediaType)
  const player = $(`<div id="player-wrapper-${userId}" class="player-wrapper re-player"><p class="player-name">${userId}</p></div>`);
  $('#player-list').append(player);
  IRTCEngine.setRemoteVideoPlayer(BytePlusRTC.StreamIndex.STREAM_INDEX_SCREEN,{
        renderDom: `player-wrapper-${userId}`,
        userId,
        renderMode: BytePlusRTC.VideoRenderMode.RENDER_MODE_HIDDEN,
  })  
})；
```
