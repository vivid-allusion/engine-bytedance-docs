---
title: "Casting"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/docs-casting"
---

BytePlus VideoOne demo supports casting a playing video to an external display. On Android, the demo casts through Chromecast (Google Cast); on iOS, it casts through AirPlay, so viewers can move playback from a mobile device to a larger screen.

<span id="cast-instruction"></span>
## Instruction


1. Install and log in to the [BytePlus VideoOne Demo app](https://docs.byteplus.com/en/byteplus-vos/docs/byteplus-videoone-demo-app_1#499f90c7).

2. On the home page, switch to the **Function** tab and enter the **Video player** function.

3. Start playing a video, and then tap the casting icon on the player.

   * On **Android**, select a Chromecast\-enabled device from the device list to start casting.

   * On **iOS**, select an AirPlay\-enabled device from the route list to start casting.

4. Control playback (play, pause, seek) from the app while the video plays on the external device. To stop casting, disconnect from the device or select the local device again.


<span id="cast-support"></span>
## Supported casting protocols and media

The following casting protocols are supported per platform:


|**Platform** |**Casting protocol** |
|---|---|
|Android |Chromecast (Google Cast) |
|iOS |AirPlay |


The following media types are supported for casting on Android (Chromecast):


|**Media type** |**Format** |
|---|---|
|Video |`.mp4`, `.dash`, `.m3u8` |
|Audio |`.aac`, `.mp3` |


On iOS (AirPlay), casting supports whatever media formats the system AVPlayer supports.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The following playback capabilities are <strong>not supported</strong> during casting on either platform:</div>



* <div data-tips="true" data-tips-type="warning">DRM\-protected content</div>


* <div data-tips="true" data-tips-type="warning">Ads</div>


* <div data-tips="true" data-tips-type="warning">Multiple audio tracks or audio\-track switching</div>


* <div data-tips="true" data-tips-type="warning">Multiple bitrates or quality switching</div>


* <div data-tips="true" data-tips-type="warning">608/708 closed captions</div>


* <div data-tips="true" data-tips-type="warning">DVR and live streams</div>



<span id="cast-implementation"></span>
## Implementation


* iOS


In iOS, we obtain video URLs from TTVideoEngine that are directly compatible with the system's AVPlayer. By implementing a bridge for playback control, we enable screen casting from TTVideoEngine to other devices that support the AirPlay protocol. Refer to the code to integrate this feature into your app: [AirPlay](https://github.com/byteplus-sdk/VideoOneSolutions/tree/main/Client/iOS/Component/VodSingleFunction/Classes/AirPlay).


* Android


On Android, we cast the playing video to Chromecast (Google Cast) devices using the Google Cast framework together with AndroidX MediaRouter for device discovery and route selection. Refer to the code to integrate this feature into your app: [vod-cast](https://github.com/byteplus-sdk/VideoOneSolutions/tree/main/Client/Android/solutions/vod-cast).
