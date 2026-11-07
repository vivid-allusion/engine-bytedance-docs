---
title: "Screen Sharing on Electron with Web SDK"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1340581"
---

If you want to let remote users view your screen or window, you can use the screen sharing feature. This topic describes how to implement screen sharing using the Web SDK in the Electron framework.

<span id="applicable"></span>
## Applicable

You can use the screen sharing feature in various industries and scenarios, such as


* A speaker shares slides during presentations or document pages in a meeting.

* A teacher shares slides and notes with students or conducts a live demonstration on the screen.


<span id="prerequisites"></span>
## Prerequisites


* You have integrated Web SDK v4.63 or later versions and implemented basic real\-time functions.

* Operating system requirements:

   * Windows 7 and later versions.

   * macOS 10.8 and later versions.


<span id="electron-environment-configurations"></span>
## Electron environment configurations


* Disable `contextIsolation`.

   ```javascript
   new BrowserWindow({
       webPreferences: {
       nodeIntegration: true,
       contextIsolation: false,
       },
   });
   ```
   

* If you use Electron 17 or later versions, add the following code to the main process file. Otherwise, you can skip this step.

   ```javascript
   const {  ipcMain, desktopCapturer } = require("electron");
   
   ipcMain.handle("DESKTOP_CAPTURER_GET_SOURCES", (event, opts) => desktopCapturer.getSources(opts));
   ```
   


<span id="optional-set-screen-stream-parameters"></span>
## [Optional] Set screen stream parameters

You can set screen stream parameters via [setScreenEncoderConfig](https://docs.byteplus.com/en/docs/12/docs-104478#setscreenencoderconfig) after creating the engine. If you do not set the parameters before starting to capture, the default parameters are used: resolution 1080P, frame rate 15fps, bitrate 3000kbps.

If the specified parameters are not supported by the browser, the SDK adapts them to the supported range. In this case, you are notified via the `onLocalVideoSizeChanged` callback.

```javascript
setScreenEncoderConfig(config:{ 
   width: number,
   height: number,
   frameRate: number,
   maxKbps:number,
   }
)
```


We recommend the following parameters for different scenarios:


|Scenarios |Width x Height |Frame rate (fps) |bitrate (kbps) |
|---|---|---|---|
|Sharing slides and texts. |1920 x 1080 |5 |2000 |
|Sharing videos, animation, and video games. |1920 x 1080 |30 |4000 |


> After screen capture has started, the profile can only be downgraded. To upgrade the profile, you need to stop screen capture and restart it.


<span id="start-screen-capture-and-share-screen-stream"></span>
## Start screen capture and share screen stream

> Sharing system audio is only supported on Windows. Sharing audio from a specific application is not supported.


<span id="build-your-own-selection-pop-up-window"></span>
### Build your own selection pop\-up window

You can build a custom pop\-up window that allows the user to choose the sharing source, as shown in the following steps.


1. Get the screen sources [ElectronDesktopCapturerSource[]](https://docs.byteplus.com/en/docs/12/docs-104481#electrondesktopcapturersource) via [getElectronScreenSources](https://docs.byteplus.com/en/docs/12/docs-104478#getelectronscreensources).

2. Build the selection pop\-up window based on the screen source information, including the screen source name and thumbnail, using HTML and CSS.

3. When the user selects a screen source, record the `sourceId` of the selected screen source and pass it to [startScreenCapture](https://docs.byteplus.com/en/docs/12/docs-104478#startscreencapture) when starting screen capture.

4. Publish the screen\-sharing stream via [publishScreen](https://docs.byteplus.com/en/docs/12/docs-104478#publishscreen).


<span id="use-the-default-selection-pop-up-window"></span>
### Use the default selection pop\-up window

You can use the default selection pop\-up window provided by the SDK, as shown in the following steps.


1. Call [startScreenCapture](https://docs.byteplus.com/en/docs/12/docs-104478#startscreencapture) to start screen capture without a `sourceId`.

2. Publish the screen\-sharing stream via [publishScreen](https://docs.byteplus.com/en/docs/12/docs-104478#publishscreen).


```javascript
await IRTCEngine.startScreenCapture({
        systemAudio: "include", // Sharing system audio is only supported on Windows.
        sourceId: "", // When no sourceId is provided, users will be prompted by the default pop-up window.
});

await IRTCEngine.publishScreen(MediaType.AUDIO_AND_VIDEO);
```



3. Stop sharing the screen stream.


```javascript
await IRTCEngine.unpublishScreen(MediaType.AUDIO_AND_VIDEO);
```


<span id="subscribe-to-a-screen-sharing-stream"></span>
## Subscribe to a screen\-sharing stream


1. Subscribe to the screen\-sharing stream via [subscribeScreen](https://docs.byteplus.com/en/docs/12/docs-104478#subscribescreen) when receiving [onUserPublishScreen](https://docs.byteplus.com/en/docs/12/docs-104479#onuserpublishscreen)

2. Add the screen\-sharing stream to a video player via [setRemoteVideoPlayer](https://docs.byteplus.com/en/docs/12/docs-104478#setremotevideoplayer) when receiving [onUserPublishScreen](https://docs.byteplus.com/en/docs/12/docs-104479#onuserpublishscreen).

> When the speaker shares their screen, the camera stream often needs to be switched to a small window display. We recommend that the receiver switch the speaker's camera stream to a lower\-resolution video stream. For details, see Push Multiple Streams.


```javascript
IRTCEngine.on(IRTCEngine.events.onUserPublishScreen, async ({ userId, mediaType }) =>{
// Subscribe to the new screen-sharing stream.
  await IRTCEngine.subscribeScreen(userId, mediaType)
  
  
  const player = $(`
    <div id="player-wrapper-${userId}" class="player-wrapper re-player">
      <p class="player-name">${userId}</p>
    </div>
  `);
  
  $('#player-list').append(player);
  
  IRTCEngine.setRemoteVideoPlayer(VERTC.StreamIndex.STREAM_INDEX_SCREEN,{
        renderDom: `player-wrapper-${userId}`,
        userId,
        renderMode: VERTC.VideoRenderMode.RENDER_MODE_HIDDEN,
  })  
})；
```
