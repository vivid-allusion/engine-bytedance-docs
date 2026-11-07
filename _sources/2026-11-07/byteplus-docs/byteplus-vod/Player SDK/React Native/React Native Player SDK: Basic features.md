---
title: "React Native Player SDK: Basic features"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-rn-player-features"
---

This article introduces how to implement the basic features of the React Native Player SDK.

<span id="eb35d0c2"></span>
## Initializing the SDK

Initialize the SDK before creating the player as shown in the code example below. Initialization only needs to be done once.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><code>initEnv</code> is an asynchronous function. To avoid authentication errors, ensure that the <code>initEnv</code> function has completed its execution before you create a player instance. It is recommended to invoke <code>initEnv</code> during the application's startup phase, rather than deferring it until the moment of player creation.</div>


```TypeScript
import { initEnv } from '@byteplus/react-native-vod-player';
import {Platform} from 'react-native';

initEnv({
  AppID: xxx,  // App ID, obtained from the BytePlus VOD console's SDK management page. See [Applications](https://docs.byteplus.com/en/docs/byteplus-vod/docs-sdk-management)
  AppName: 'democeshi', // Appl name, obtained from the BytePlus VOD console's SDK management page. See [Applications](https://docs.byteplus.com/en/docs/byteplus-vod/docs-sdk-management)
  PackageName: com.xxx.xxxx, // Android project package name, the value of applicationId in build.gradle
  BundleID: com.xxx.xxxx.x, // iOS project package name, the Bundle Identifier value under TARGETS in Xcode
  AppChannel: Platform.select({
    android: 'GoogleStore',
    ios: 'AppStore',
  }), // Channel number. Customized by you, such as Xiaomi App Store (xiaomi), Huawei AppMarket (huawei).
  AppVersion: '1.0.0', // App version number. A valid version number should contain 2 or more dots, such as "1.3.2".
  LicenseUri: Platform.select({
    android: 'assets:///VeVod.lic',
    ios: 'VeVod.lic',
  }), // License file path. Note that iOS and Android have different paths in their respective folders
  UserUniqueID: 'ReactNativeExample', // User ID, customized by you, can be used to view playback data of a single device in the BytePlus VOD console's Endpoint tracker page. See [Endpoint tracker](https://docs.byteplus.com/en/docs/byteplus-vod/docs-end-point-tracker)
  OpenLog: true, // Whether to enable log printing. For Android, logs can be captured through logcat. For iOS, logs can be captured through Xcode.
  MaxCacheSize: 300 * 1024 * 1024, // Maximum cache size, in bytes
})
```


When initializing the SDK, set the following parameters:


|Parameter |Type |Required |Default value |Description |
|---|---|---|---|---|
|AppID |String |Yes |`-` |App ID. Obtained from the BytePlus VOD console's SDK management page. See [Applications](https://docs.byteplus.com/en/docs/byteplus-vod/docs-sdk-management). |
|AppName |String |Yes |`-` |App name. Obtained from the BytePlus VOD console's SDK management page. See [Applications](https://docs.byteplus.com/en/docs/byteplus-vod/docs-sdk-management). |
|AppVersion |String |Yes |`-` |App version number. A valid version number should contain 2 or more dots, such as `"1.3.2"`. |
|AppChannel |String |Yes |`-` |Channel number. Customized by you, such as Xiaomi App Store (xiaomi), Huawei AppMarket (huawei). |
|PackageName |String |No |`-` |Android project package name, the value of applicationId in `build.gradle` |
|BundleID |String |No |`-` |iOS project package name, the Bundle Identifier value under TARGETS in Xcode |
|LicenseUri |String |Yes |`-` |License file path. Note that iOS and Android have different paths in their respective folders |
|OpenLog |Boolean |No |`false` |Whether to enable log printing.<br><br><br>* For Android, logs can be captured through logcat.<br><br>* For iOS, logs can be captured through Xcode. |
|UserUniqueID |string |No |`-` |The user ID, customized by you. Can be used to view playback data of a single device in the BytePlus VOD console's Endpoint tracker page. See [Endpoint tracker](https://docs.byteplus.com/en/docs/byteplus-vod/docs-end-point-tracker) |
|MaxCacheSize |number |No |100M |Maximum cache size, in bytes. |


<span id="5ce1e697"></span>
## **Creating the player**


1. Insert the `PlayerViewComponent` into the component where the player is needed and assign a unique ID to its `viewId` property.

   ```TypeScript
   import {PlayerViewComponent} from '@byteplus/react-native-vod-player';
   
   function Player() {
     // ...
   
     return (
       <PlayerViewComponent
             viewId="player_container"
             onLoad={onLoad}
             style={{
               width: '100%',
               height: '100%',
             }}
         >
         </PlayerViewComponent>
     );
   }
   ```
   

2. Call `initPlayer` in the `onLoad` callback of `PlayerViewComponent` and pass the `viewId` to create the player. Note that this method is asynchronous.

   ```TypeScript
   import { initPlayer, PlayerViewComponent } from '@byteplus/react-native-vod-player';
   // (Optional) If you need to specify the scaling mode during player initialization, additionally import FillModeType  
   // import { FillModeType } from '@byteplus/react-native-vod-player';  
   
   function Player() {
     const playerRef = useRef();
   
     const onLoad = useCallback(async () => {
       playerRef.current = await initPlayer({viewId: 'player_container'});
       // Set the initial video scaling mode (FillModeType) when creating the player.  
       // For enum values, refer to: https://docs.byteplus.com/en/docs/byteplus-vod/docs-rn-player-features#set-scaling-mode
       // playerRef.current = await initPlayer({ viewId: 'player_container', fillMode: FillModeType.FillModeAspectFill });  
     }, []);
   
     return (
       <PlayerViewComponent
             viewId="player_container"
             onLoad={onLoad}
             style={{
               width: '100%',
               height: '100%',
             }}
         >
         </PlayerViewComponent>
     );
   }
   ```
   


<span id="e005331e"></span>
## Setting the playback source

The Player SDK supports setting Vid and DirectUrl playback sources.


* To use a Vid playback source: Call `createVidSource` to create a `vidSource` object, and then set it to the player using the `setVideoSource` method. You need to set the `vid` parameter as the video ID generated by the BytePlus VOD service, and set the `playAuthToken` parameter as the temporary playback token. The video ID and temporary playback token are issued by the application server. For details, see [Playing videos with temporary playback tokens](https://docs.byteplus.com/docs/byteplus-vod/docs-playing-videos-with-temporary-playback-tokens).

   ```TypeScript
   import { createVidSource } from '@byteplus/react-native-vod-player';
   
   const vidSource = createVidSource({
     playAuthToken: playAuthTokenxxx, // Temporary playback token issued by the application server
     vid: xxxvid, // Video ID
   });
   playerRef.current.setVideoSource(vidSource);
   ```
   

* To use a DirectUrl playback source: Call `createDirectUrlSource` to create a `urlSource` object, then call `setVideoSource` to set this `urlSource` object to the player. You need to set the `url` parameter as the video playback address. The playback address can be a third\-party address or a playback address generated by the BytePlus VOD service. In addition, for DirectUrl playback sources, `vid` and `cacheKey` are required parameters, as explained below:

   * `vid`: This serves as the unique identifier for the video. The `vid` can either be a unique identifier from your video management system or an ID generated at the app level. This ID will be used for features such as logging, preloading, and prerendering.

   * `cacheKey`: It is recommended to use the MD5 of the URL as the cache key. The cache key must be distinct, free of special characters, and suitable for use as a file name.

   ```TypeScript
   import { createDirectUrlSource } from '@byteplus/react-native-vod-player';
   
   const urlSource = createDirectUrlSource({
     url: 'https://demo.video.com/1.mp4', // Video URL
     cacheKey: 'cacheKeyDemo01', // Unique key for source caching
     vid: 'xxxxxx',  // Video ID
   });
   playerRef.current.setVideoSource(urlSource);
   ```
   


<span id="c07f6401"></span>
## Playback control

```TypeScript
const player = playerRef.current;

// Play
player.play();

// Pause. Calling play again can resume playback from pause
player.pause();

// Prepare
player.prepare();

// Start playback from a specified position, unit: seconds
player.seek(value, success => {
  if (success) {
    // Seek successful
    // do something
  }
});

// Stop playback
player.stop();
```


<span id="9516cce0"></span>
## Releasing the player

When the player is no longer needed, promptly call the `close` method to release resources and prevent memory leaks.

```TypeScript
// Asynchronously release the player instance. After the player is released, no methods of the instance should be called
player.close();
```


To minimize memory usage and maintain a smooth user experience, limit the number of active player instances to 6 or fewer. In feed scrolling scenarios, adopting a pre\-rendering strategy to load players in advance is recommended for seamless playback.

<span id="7c1f3f9b"></span>
## Getting current playback time

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">Starting from version 1.2.4, you can obtain the current playback time via the <code>onCurrentPlaybackTimeUpdate</code> callback; for more details, see <a href="https://docs.byteplus.com/docs/byteplus-vod/docs-rn-player-features#d387836a">Set callbacks</a>.</div>


```TypeScript
// Unit: seconds
const currentTime = player.getCurrentPlaybackTime();
```


<span id="40b48dc4"></span>
## Getting cached video duration

```TypeScript
// Unit: seconds
const progress = player.getProgress();
```


<span id="395fda8b"></span>
## Getting playback state

```TypeScript
const playbackState = player.getPlaybackState();
```


The enumeration values of the playback state `PlaybackState` are shown in the table below.


|Enumeration Key |Value |Description |
|---|---|---|
|STOP |0 |Playback stopped |
|PLAYING |1 |Playback in progress |
|PAUSE |2 |Playback paused |
|ERROR |3 |Playback error |


<span id="a4979c49"></span>
## Getting loading state

```TypeScript
const loadState = player.getLoadState();
```


The enumeration values of the load state `TTVideoEngineLoadState` are shown in the table below.


|Enumeration Key |Value |Description |
|---|---|---|
|PLAYABLE |1 |Player has loaded and can start or resume playback |
|STALLED |2 |Player is buffering, loading data. You can add a loading icon based on the load state being `2`. |
|ERROR |3 |Error loading data for the player |
|UNKNOWN |4 |Unknown |


<span id="9cfbc35e"></span>
## Getting video information

```TypeScript
const duration = player.getDuration(); // Video duration
const videoWidth = player.getVideoWidth(); // Video width
const videoHeight = player.getVideoHeight(); // Video height
```


<span id="cfa25d20"></span>
## Getting device ID

If you did not set a custom user ID during SDK initialization, you can use the following example code to get the device ID. This ID can be used toview playback data of a single device in the BytePlus VOD console's Endpoint tracker page.

```TypeScript
import { getDeviceID } from '@byteplus/react-native-vod-player';

const did = getDeviceID();
```


<span id="adbd578b"></span>
## Setting playback speed

```TypeScript
// Set playback speed, range from 0.5 to 3
player.setPlaybackSpeed(2);

// Get the current playback speed
const speed = player.getPlaybackSpeed();
```


<span id="d0daaeab"></span>
## Setting loop playback

```TypeScript
// Set loop playback
player.setLooping(true);

// Get whether loop playback is currently enabled
const isLoop = player.getIsLooping();
```


<span id="e7fd7d26"></span>
## Mute

```TypeScript
// Mute
player.setMuted(true);

// Get whether the player is currently muted
const isMute = player.isMute();
```


<span id="61fe1853"></span>
## Adjusting volume

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">On iOS, only playback volume can be adjusted, so <code>setTrackVolumeEnabled</code> must be called before playback begins.</div>


```TypeScript
// Adjust volume, range from 0 to 1
player.setVolume(0.6);

// Get the volume, range from 0 to 1
player.getVolume();

// true: Adjust playback volume. Called before play() when changing to true
// false: Adjust system volume
// Default value is false
player.setTrackVolumeEnabled(true);
```


<span id="cb717a8e"></span>
## Audio\-only playback

The Player SDK supports decoding only the audio stream while playing videos, which is suitable for scenarios where only audio playback is required. Compared to implementing your own audio\-only playback logic, using the SDK to decode only the audio stream can save power.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This feature is only supported by the Premium Edition. Please make sure you have purchased the Premium Edition license and added the appropriate dependency.</div>


```TypeScript
player.setRadioMode(true);
```


<span id="17bae7bf"></span>
## Setting rotation angle

```TypeScript
// Set the video rotation angle. Supported values: 0, 90, 180, 270
player.setRotation(90);

// Get the video rotation angle
const rotation = player.getRotation();
```


<span id="a75ea3f6"></span>
## Setting scaling mode

```TypeScript
import { FillModeType } from '@byteplus/react-native-vod-player';

player.setDisplayMode(FillModeType.FillModeAspectFill);
```


The enumeration values of the fill mode `FillModeType` are shown in the table below.


|Enumeration Key |Value |Description |
|---|---|---|
|FillModeNone |1 |(Default) No stretching, no distortion, may have black bars. |
|FillModeAspectFit |2 |Resizes the video to fit the box while maintaining its aspect ratio. Areas that are not filled due to the disparity in the aspect ratio are filled with blackness. |
|FillModeAspectFill |3 |Resizes the video to fill the box while maintaining its aspect ratio. Part of the video might be cropped in the process. |
|FillModeFill |4 |Resizes the video to fill the box, regardless of its aspect ratio. The video may be distorted as a result. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>



* <div data-tips="true" data-tips-type="tip">When playing vertical videos, to fill the player container without black bars, set the fill mode to <code>fillModeType.fillModeAspectFill</code>.</div>


* <div data-tips="true" data-tips-type="tip">If using an <a href="https://reactnative.dev/docs/image#resizemode">image component</a> <code><image /></code> to display the video's first frame as a cover, ensure its <code>resizeMode</code> is set to <code>cover</code> to achieve a smooth, seamless transition into playback.</div>



<span id="49affeff"></span>
## Setting mirror mode

```TypeScript
// 0: No mirror, 1: Horizontal mirror, 2: Vertical mirror, 3: Both horizontal and vertical mirror
player.setMirror(1);
```


<span id="57cd206d"></span>
## Keeping the screen on

```TypeScript
// Sets the screen to stay on. 
// true: keeps the screen on, false: turns off the screen staying on.
player.setKeepScreenOn(true);

// Gets the current state of the screen staying on.
// true: screen stays on, false: screen does not stay on.
const flag = player.getKeepScreenOn();
```


<span id="4d9c9790"></span>
## Setting start time

```TypeScript
// Unit: seconds. The following example sets the start time to 20 seconds
player.setStartTime(20);
```


<span id="9f550d15"></span>
## Setting tags

The tag is used to distinguish different types of audio and video within the same application (appid). It can be divided based on video scenes, video durations, such as immersive feed stream, short videos, long videos. Example code:

```TypeScript
player.setTag('feed');
```


<span id="db70f39c"></span>
## Setting sub tags

The subtag is used to distinguish different subdivisions within the same tag, such as encrypted videos, non\-encrypted videos, audio. Example code:

```TypeScript
player.setSubTag('audio');
```


<span id="f6e4662d"></span>
## **Switching between multiple resolutions**

<span id="21b11f4b"></span>
### **Vid Mode**

In Vid playback mode, the Player SDK can automatically fetch all available resolutions for a video and supports dynamic switching during playback. The core workflow is as follows:


1. **Fetch resolution info:**  After the Player SDK successfully retrieves the video information using a `Vid` and a temporary playback token, the `onFetchedVideoInfo` callback is triggered.

2. **Get resolution list:**  Call the `supportedResolutionTypes()` method on the player instance to get an array of all available resolutions. You can use this array to dynamically generate a resolution selection menu in your UI.

3. **Perform switch:**  Call the `configResolution()` method, passing the enum value of the target resolution to complete the switch.


After the `onFetchedVideoInfo` callback is triggered, use the following method to get the list of available resolutions.

```TypeScript
// Call this after the onFetchedVideoInfo callback
const availableResolutions = player.supportedResolutionTypes();
```


After the `onPrepared` callback is triggered, you can get the currently playing resolution by calling `getCurrentResolution()`.

```TypeScript
// Get the video resolution info; must be called after onPrepared
const currentResolution = player.getCurrentResolution();
```


Call `configResolution()` and pass the target resolution defined in the `ResolutionType` enum.

```TypeScript
import { ResolutionType } from '@byteplus/react-native-vod-player';

// Switch to Standard Definition
player.configResolution(ResolutionType.Standard);
```


The enum values for `ResolutionType` are listed below.


|Enum Key |Value |Description |
|---|---|---|
|`Undefine` |`Undefine` |Unknown |
|`Standard` |`Standard` |Standard Definition (360p) |
|`High` |`High` |High Definition (480p) |
|`HighH` |`HighH` |540p |
|`SuperHigh` |`SuperHigh` |Super High Definition (720p) |
|`ExtremelyHigh` |`ExtremelyHigh` |1080p |
|`TwoK` |`TwoK` |2K |
|`FourK` |`FourK` |4K |
|`Auto` |`Auto` |**Adaptive bitrate**. This option is only applicable to **DASH** videos. It allows the player to automatically select the optimal resolution based on the current network conditions. |


<span id="2cc57ef2"></span>
#### Seamless switching **between multiple resolutions**

Seamless switching (or smooth switching) allows the video to transition to a new bitrate stream without interruption or black screens, providing a smooth viewing experience. This feature depends on the underlying streaming protocol (such as HLS or DASH) and is only available in Vid mode when the video source format supports it.

```TypeScript
import { ResolutionType } from '@byteplus/react-native-vod-player';

// Enable seamless switching for HLS videos
player.enableHLSSeamlessSwitch(true);

// Enable seamless switching for MP4 videos (if supported)
// player.enableMP4SeamlessSwitch(true);

// Subsequent switching operations are the same as regular switching
// Get resolution list
const list = player.supportedResolutionTypes();
// Switch resolution
player.configResolution(ResolutionType.Standard);
```


<span id="78e68d16"></span>
### **DirectUrl Mode**

Since `DirectUrl` mode plays a single, direct URL, it does not inherently support the concept of multiple resolutions. Therefore, the automatic switching capabilities described above are not available. If you need to implement resolution switching in `DirectUrl` mode, you must manually perform the following steps:


1. Get and store the current playback time.

2. Create and set a new video source with the new URL.

3. On the new video source, use the `setStartTime()` method to seek to the stored playback time.

4. Call `play()` to start the video.


This method essentially restarts playback with a new video file. It may cause a brief black screen and loading period and **cannot achieve seamless switching**.

**Example code:** 

```TypeScript
// 1. Store the current playback time
const currentTime = player.getCurrentPlaybackTime();

// 2. Create and set a new video source with the URL of the new resolution
const newSource = createDirectUrlSource({
  vid: 'your_vid_2',
  url: 'https://www.example.com/video_720p.mp4', // The new resolution URL
  cacheKey: 'newCacheKey',
});
player.setVideoSource(newSource);

// 3. Set the start time
player.setStartTime(currentTime);

// 4. Start playback
player.play();
```


<span id="d387836a"></span>
## Setting callbacks

Call the `setListener` method to set callbacks for various playback states such as preparation, loading, first frame display, completion, and errors. The example code is as follows.

```TypeScript
player.setListener({
  // When the video is prepared
  onPrepared(_engine: TTVideoEngine) {
    console.log('Video prepared');
  },
  // Load state changed
  onLoadStateChanged(engine: TTVideoEngine, loadState) {
    console.log(`Load state changed: ${loadState}`);
  },
  // Playback state changed
  onPlaybackStateChanged(engine: TTVideoEngine, playbackState) {
    console.log(`Playback state changed: ${playbackState}`);
  },
  // Current playback time
  onCurrentPlaybackTimeUpdate(currentTime) {
    console.log(`onCurrentPlaybackTimeUpdate: ${currentTime}`);
  },
  // First frame of the video is displayed
  onReadyToDisplay(_engine: TTVideoEngine) {
    console.log('Ready to display');
  },
  // Playback completed
  onDidFinish(_engine: TTVideoEngine) {
    console.log('Playback finished');
  },
  // Playback error, returns error message and error code, see [Player SDK Error Codes](https://docs.byteplus.com/en/docs/byteplus-vod/docs-error-code) for details
  onError(message: string, code: number) {
    console.log(`Error: code: ${code}, message: ${message || ''}`);
  },
  // Cache change callback, triggered when preloading is successful
  onCacheChange(cacheKey: string, cacheSize: number) {
    if (cacheSize > 0) {
       console.log('Video preloaded: ', cacheKey, cacheSize);
    }
  },
  // Get the video info in Vid mode
  onFetchedVideoInfo(videoModel) {
    console.log('fetched video info', videoModel);
  },
});
```
