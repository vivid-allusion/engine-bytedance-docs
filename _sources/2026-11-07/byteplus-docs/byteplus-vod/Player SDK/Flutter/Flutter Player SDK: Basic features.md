---
title: "Flutter Player SDK: Basic features"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-flutter-player-basic-features"
---

To integrate video playback into your Flutter application, you can use the BytePlus Player SDK. This guide provides step\-by\-step instructions and code examples covering the entire process, from initializing the SDK and creating a player instance to setting various playback sources such as Vid, DirectUrl, and VideoModel. You will also learn how to control playback, manage the player lifecycle, and implement other essential features.

<span id="255755db"></span>
## Import header files

```Dart
import 'package:byteplus_vod/ve_vod.dart';
```


<span id="fbe0cdb4"></span>
## Initialize the SDK

It is recommended to initialize the SDK in the `runApp` method of the `main.dart` file of your project to ensure the initialization order.

```Dart
Future<void> initTTSDK() async {
    // Enable logging
    FlutterTTSDKManager.openAllLog();

    // Register plugin logs
    TTFLogger.onLog = (logLevel, msg) {
      print(msg);
    };

    // Provide a valid license file path, such as 'assets/VEVod.lic'
    String licPath = 'your license file path'; 
    // For Android, provide a valid channel ID for statistics; for iOS, it is optional and defaults to App Store
    String channel = Platform.isAndroid ? 'your channel' : 'App Store';
    // Initialize VOD configuration
    TTSDKVodConfiguration vodConfig = TTSDKVodConfiguration();
    // Set the maximum cache size (default: 100 MB) and adjust it based on your business scenario. When the cache exceeds this limit, eviction is performed based on LRU rules
    vodConfig.cacheMaxSize = 300 * 1024 * 1024;
    
    // Provide the AppID obtained from the BytePlus VOD console
    TTSDKConfiguration sdkConfig =
        TTSDKConfiguration.defaultConfigurationWithAppIDAndLicPath(
            appID: 'your AppID', licenseFilePath: licPath, channel: channel);
    sdkConfig.vodConfiguration = vodConfig;
    FlutterTTSDKManager.startWithConfiguration(sdkConfig);
   
    // If you need to support multiple regions, please submit a ticket to contact technical support
  }
```


<span id="4aa5d533"></span>
## Set custom device ID

By configuring a custom device ID, you can view the playback data of a single device on the BytePlus VOD console. For details, see [Endpoint tracker](https://docs.byteplus.com/en/docs/byteplus-vod/docs-end-point-tracker.).

```Dart
Future<void> initTTSDK() async {
    // ... 
    FlutterTTSDKManager.startWithConfiguration(sdkConfig);
   
    // Set the unique ID after SDK initialization, which is used for individual user tracking and troubleshooting, usually the user ID or device ID
    FlutterTTSDKManager.setCurrentUserUniqueID('your uniqueID');
  }
```


<span id="ca23a48d"></span>
## Create a player

```Dart
// Create a player instance
VodPlayerFlutter player = VodPlayerFlutter();

// If using a prerendering strategy, you need to set the vid and preCreated parameters when calling createPlayer; if not using a prerendering strategy, you don't need to pass parameters.
// When calling createPlayer, you need to use await; after it's complete, you can call other methods of the player.
await player.createPlayer();

// Android: Sets the native view type; defaults to NativeViewType.TextureView.
NativeViewType nativeViewType = NativeViewType.TextureView;
// Create a TTVideoPlayerView for rendering the video. The TTVideoPlayerView is constructed internally using a NativeView
TTVideoPlayerView playerView = TTVideoPlayerView(
  onPlatformViewCreated: (int viewId) {
    // After the NativeView is created, the player and viewId need to be bound
    player.setPlayerContainerView(viewId);
  },
);
 
// Reference the created TTVideoPlayerView in the Build method
@override
Widget build(BuildContext context) {
    return Scaffold(
        body: playerView,
    );
}
```


<span id="fde3b4dd"></span>
## Set the playback source

The Player SDK supports setting Vid, DirectUrl, VideoModel, and local files as playback sources.


<Tabs>
<Tab zoneid="ShJdfx2axr" title="Vid">
<TabTitle>Vid</TabTitle>

To use the Vid playback source, you need to set two parameters for the player: Vid and PlayAuthToken. Vid and PlayAuthToken are signed and issued by the application server. The client needs to call the interface provided by the server to obtain them. For details, see [Playing videos with temporary playback tokens](https://docs.byteplus.com/docs/byteplus-vod/docs-playing-videos-with-temporary-playback-tokens).

```Dart
TTVideoEngineVidSource source = TTVideoEngineVidSource.init( 
        vid: <vid>, 
        playAuthToken: <playAuthToken>, 
        resolution: <TTVideoEngineResolutionType>); 
 
player.setMediaSource(source);
```



</Tab>
<Tab zoneid="mTtLSMt7Vo" title="DirectUrl">
<TabTitle>DirectUrl</TabTitle>

To use the DirectUrl playback source, you need to set the playback URL for the player. The playback URL can be a third\-party URL or a playback URL generated by the BytePlus VOD service.

```Dart
import 'dart:convert';
import 'package:crypto/crypto.dart';

String generateVideoCacheKey(String videoUrl) {
  final path = Uri.parse(videoUrl).path;
  return md5.convert(utf8.encode(path)).toString();
}

final cacheKey = generateVideoCacheKey(videoUrl);
TTVideoEngineUrlSource source = TTVideoEngineUrlSource.initWithURL(videoUrl, cacheKey);

player.setMediaSource(source);
```



</Tab>
<Tab zoneid="zcmuX08DoX" title="VideoModel">
<TabTitle>VideoModel</TabTitle>

VideoModel is a proprietary protocol for an optimal playback experience in multi\-resolution scenarios. It allows you to achieve reduced first\-frame time and supports fine\-grained control over multi\-resolution information. Compared to the Vid mode (the Player SDK requests playback information from the VOD server via a Vid), VideoModel skips this client\-to\-server network request. Your business server can directly generate or your client can assemble the VideoModel playback source, and then pass it to the Player SDK to initiate loading.

**Core concepts:** 


* `VideoModel`: Refers to a complete video playback source. It does not directly contain the video address itself but manages video streams of different resolutions via a video information list `playInfoList`. The VideoModel also includes metadata such as `vid`, `resolution`(default playback resolution), and `duration`.

* `PlayInfoListItem`：Refers to a specific entry of the video information list and represents video stream information for a specific resolution. It contains detailed parameters such as `urls`, `cacheKey`, `resolution`, and `codecType` for that specific resolution.

* Relationship: A `VideoModel` contains multiple `PlayInfoListItem`s. Each `PlayInfoListItem` corresponds to a specific resolution. The `resolution` field of `VideoModel` determines the default `PlayInfoListItem` during the first playback.


The following are the specific steps to set up the VideoModel playback source:


1. Prepare video data: The client needs to fetch video data from your business server. Video data can come from third\-party services or the VOD service. If the data comes from VOD, your business server needs to call the [GetPlayInfo](https://docs.byteplus.com/docs/byteplus-vod/reference-getplayinfo) API to obtain JSON data similar to the format below, where each JSON object represents video information for one resolution:

   ```JSON
   [
     {
       "FileId": "a549b7a3c920427f8ca8a33465a306c8",
       "Format": "hls",
       "Codec": "h264",
       "Definition": "480p",
       "MainPlayUrl": "https://example.com/video_480p.m3u8",
       "BackupPlayUrl": "https://backup.example.com/video_480p.m3u8",
       "Bitrate": 459230,
       "Width": 854,
       "Height": 480,
       "Duration": 152.132,
       "MainUrlExpire": "1856870593",
       "BackupUrlExpire": "1856870593"
     }
     // ... It may contain information for 720p, 1080p and more
   ]
   ```
   

2. Create `PlayInfoListItem` list: You need to map and convert the raw data returned by the server interface into `PlayInfoListItem` objects, and then use this object list to initialize the final `TTVideoEngineVideoModelSource`. During the process, pay attention to the mapping of the following key fields:

   * **`resolution`** **:**  The resolution identifier returned by the server (such as "1080p") needs to be converted to the enumeration type `TTVideoEngineResolutionType` defined internally by the SDK. You can use the provided utility function `TTVideoEngineResolutionType.transFromDefinition()` to convert.

   * **`codecType`** **:**  Similarly, the codec format string returned by the server (such as "h264") needs to be converted to the SDK's enumeration type `TTVideoEngineEncodeType` via the `TTVideoEngineEncodeType.transFromString()` function.

   * **`cacheKey`** **:**  To ensure that offline caching works correctly, each `PlayInfoListItem` needs a globally unique `cacheKey`. It is recommended to use the `FileId` returned by the server as the `cacheKey`.

      Below is the complete example code for conversion and creation:

   ```Dart
   import 'dart:convert';
   
   // Assume rawJson is the raw JSON string obtained from the server
   // 1. Parse the JSON string into a Dart List<Map<String, dynamic>> structure
   final List<Map<String, dynamic>> playInfos = jsonDecode(rawJson) as List<dynamic>
       .cast<Map<String, dynamic>>();
   
   // Define a conversion function to map the raw data list returned by the server to the PlayInfoListItem list required by the SDK
   List<PlayInfoListItem> toPlayInfoList(List<Map<String, dynamic>> infos) {
     // Iterate through the raw data list and convert each item (Map) into a PlayInfoListItem object
     return infos.map((item) {
       // Extract main and backup playback URLs and store them in a list
       // Check if the URL string is null or empty to avoid errors
       final urls = <String>[
         if ((item['MainPlayUrl'] as String?)?.isNotEmpty ?? false)
           item['MainPlayUrl'] as String,
         if ((item['BackupPlayUrl'] as String?)?.isNotEmpty ?? false)
           item['BackupPlayUrl'] as String,
       ];
   
       // Extract expiration timestamps for main and backup playback URLs
       final expireTimes = <String>[
         if ((item['MainUrlExpire'] as String?)?.isNotEmpty ?? false)
           item['MainUrlExpire'] as String,
         if ((item['BackupUrlExpire'] as String?)?.isNotEmpty ?? false)
           item['BackupUrlExpire'] as String,
       ];
   
       // Create and return a PlayInfoListItem instance
       return PlayInfoListItem(
         // Required: List of video playback URLs; the player will try them in order
         urls: urls,
         // Optional: List of URL expiration timestamps, corresponding one-to-one with URLs. Pass null if the list is empty
         urlExpiredTimes: expireTimes.isEmpty ? null : expireTimes,
         // Required: Unique identifier for caching. It is recommended to use the `FileId` returned by the server
         cacheKey: item['FileId'] as String, 
         // Required: Video codec format. Use the utility function provided by the SDK to convert from string (such as "h264") to enum type
         // Provide a default value 'h264' to increase code robustness
         codecType: TTVideoEngineEncodeType.transFromString(
           (item['Codec'] as String?) ?? 'h264',
         ),
         // Required: Video resolution. Use the utility function provided by the SDK to convert from string (such as "1080p") to enum type
         resolution: TTVideoEngineResolutionType.transFromDefinition(
           (item['Definition'] as String?) ?? '',
         ),
         // Optional: File type, such as "video" or "audio". Required for DASH protocol
         fileType: item['FileType'] as String?,
         // Optional: Video container format, such as "hls" or "mp4". This is a necessary field for ABR or smooth switching.
         format: item['Format'] as String?,
         // Optional: Video width. A necessary field for ABR playback.
         width: (item['Width'] as num?)?.toInt(),
         // Optional: Video height. A necessary field for ABR playback.
         height: (item['Height'] as num?)?.toInt(),
         // Optional: Video bitrate. A necessary field for ABR or smooth switching.
         bitrate: (item['Bitrate'] as num?)?.toInt(),
       );
     }).toList(); // Convert the map result to a List
   }
   
   // 2. Call the conversion function to generate the PlayInfoListItem list
   final playInfoList = toPlayInfoList(playInfos);
   
   // 3. Use the generated playInfoList to create a VideoModelSource
   final modelSource = TTVideoEngineVideoModelSource.init(
     // Unique ID of the video, ensure it is globally unique. It is recommended to use the vid returned by the server.
     vid: 'your_vid',
     // Required: Set default playback resolution. The first one in the list is used as an example.
     resolution: playInfoList.first.resolution,
     // Required: Pass in the constructed resolution info list.
     playInfoList: playInfoList,
     // Optional: Set total video duration. It can be obtained from raw data.
     duration: (playInfos.first['Duration'] as num?)?.toDouble(),
   );
   ```
   

3. Set playback source: Set the created `modelSource` object to the player instance via the setMediaSource method.

   ```Dart
   await player.setMediaSource(videoModelSource);
   ```
   


</Tab>
<Tab zoneid="hn0mty6fQL" title="Local file playback source">
<TabTitle>Local file playback source</TabTitle>

Use a local file playback source to play a device\-local video file that your application has permission to access. Create the player first, and then set the playback source using the local file path. This scenario uses `setLocalURL` and does not require you to construct a `TTVideoEngineUrlSource` or call `setMediaSource`.

```Dart
final player = VodPlayerFlutter();

await player.createPlayer();
await player.setLocalURL('/absolute/path/to/video.mp4');
await player.play();
```


**Parameters and call constraints:** 


* `path` must not be empty. The SDK trims leading and trailing whitespace, and throws an `ArgumentError` if the result is empty.

* Call this method after `createPlayer()` completes. Otherwise, it throws a `StateError`.

* On Android, pass a local absolute path that your application can access.

* On iOS, both a plain local path and a `file://` URL are supported. A plain path is converted to a file URL on the native side.

* Your application is responsible for obtaining the path and the required storage permissions. The file picker is only a demo implementation, not a required dependency of the SDK.

* Local file playback does not use the [automatic playback source refresh](https://docs.byteplus.com/docs/byteplus-vod/docs-flutter-player-automatic-playback-source-refresh) flow that applies to network playback sources.


</Tab>
</Tabs>


<span id="f541c3ec"></span>
## Playback control

```Dart
// Play
player.play();
 
// Pause, calling play again can resume playback from the pause state
player.pause()

// Start playback from a specified position, in milliseconds. Set before calling play to start playback from a specific time or skip the beginning of the video
player.setStartTimeMs(<double);
// Seek to a specified position for playback, in milliseconds. This can be used to implement dragging the progress bar to start playback at a specific time
player.seekToTimeMs(time:<double);
// Seek and listen to seek status callbacks
player.seekToTimeMs(
    time: <double,
    seekCompleted: (bool success) {
        // Callback when seek is completed
    },
    seekRenderCompleted: () {
        // Callback when the first frame is rendered after seeking
    });

// Refreshes the current video frame to the Surface. When the player is paused, this displays the video data on the Surface, resolving black screen issues.  Only effective on Android.
player.forceDraw();

// Stop playback
player.stop();

// Asynchronously release the player instance. After the player is released, no method of the instance should be called
player.closeAsync();
```


<span id="0d466fec"></span>
## Set the scaling mode

```Dart
// Set the scaling mode of the video, supports the following modes:
// TTVideoEngineScalingModeNone: No stretching, no deformation, may have black bars
// TTVideoEngineScalingModeAspectFit: Aspect fit, no deformation, maintains the video's aspect ratio, may have black bars
// TTVideoEngineScalingModeAspectFill: Aspect fill, no deformation, fills the screen while maintaining the video's aspect ratio, may crop the image
// TTVideoEngineScalingModeFill: Stretches to fill the view, which causes deformation if the video's aspect ratio is different from the view's
player.setScalingMode(<TTVideoEngineScalingMode>);

// (Only for iOS) When scaleMode = AspectFill, on some older devices (such as iPhone 8 and below), there may be cases where the rendering area exceeds the layout size. You can call the setClipToBounds method to set whether to clip the rendering area. Default is false.
player.setClipToBounds(<bool>);
```


<span id="bc65ecbb"></span>
## Set the rotation angle

```Dart
// Set the rotation angle, can be set to 0, 90, 180, 270
player.setRotation(<int>);
```


<span id="3fafac94"></span>
## Set the mirroring mode

```Dart
// Enable horizontal mirroring
player.setMirrorHorizontal(<bool>);
// Enable vertical mirroring
player.setMirrorVertical(<bool>);
```


<span id="f92e26e0"></span>
## Screenshots

```Dart
// Pass in the complete screenshot storage path. The SDK will save the screenshot based on the provided path and return the screenshot result:
// - iOS: It is recommended to use the sandbox documents directory, combined with a timestamp and format to save the screenshot, for example: /var/mobile/Containers/Data/Application/<xxxx>/Documents/timestamp.png.
// - Android: It is recommended to save the screenshot to the app's file directory, using a path combined from a directory, timestamp, and format to save the screenshot, for example: /storage/emulated/0/Android/data/com.xxxx/files//timestamp.png. If you need to save it to a subdirectory of the system directory, you need to create the subdirectory first.
player?.snapshot(path: <String>, completion: (bool success, String filePath) {},);
```


<span id="2940c5b7"></span>
## Enable looping playback

```Dart
player.setLooping(<bool>);
```


<span id="ec4c3046"></span>
## Set playback speed

```Dart
// Set the playback speed, value range from 0.1 to 3.0
player.setPlaybackSpeed(<double>);
```


<span id="c2aef9e1"></span>
## Set custom headers

```Dart
// Set custom HTTP headers for the playback request
player.setCustomHeader(<String key, String value>);
```


<span id="5218e077"></span>
## Mute

```Dart
// Mute the player
player.setMuted(<bool>);
```


<span id="f757beef"></span>
## Set the volume

The volume is adjusted on a normalized scale from `0.0` (mute) to `1.0` (maximum volume).

```Dart
Future<void> setNormalizedVolume(double volume)
```


By default, this method controls the system volume. If you need to control the player's individual volume (also known as track volume) independently of the system, you must call `setTrackVolumeEnabled(true)` before playback begins.

```Dart
// true: Adjusts the individual player volume.
// If set to true, this method must be called before `play()`
// false (default): Adjusts the system-wide volume.
player.setTrackVolumeEnabled(true);
```


<span id="b8922776"></span>
## Get the volume

This method returns the current volume on a normalized scale from `0.0` to `1.0`.

```Dart
Future<double?> getNormalizedVolume()
```


<span id="8e385f76"></span>
## Set tags

The tag is used to distinguish different types of audio and video within the same application (appid). You can use tags to categorize videos by scene or duration, such as for an immersive feed stream, short videos, or long videos. Example code:

```Dart
player.setTag(<String>);
```


<span id="57bc9d16"></span>
## Set sub tags

The subtag is used to distinguish different subdivisions within the same tag, such as encrypted videos, non\-encrypted videos, audio. Example code:

```Dart
player.setSubTag(<String>);
```


<span id="2e3b9405"></span>
## Audio\-only playback

The Player SDK supports decoding only the audio stream while playing videos, which is suitable for scenarios where only audio playback is required. Compared to implementing your own audio\-only playback logic, using the SDK to decode only the audio stream can save power.

This feature is only available in the Premium Edition.

```Dart
// true: Enable audio-only playback, video rendering stops
// false: Resume audio and video playback, video rendering resumes
player.setRadioMode(<bool); 
```


<span id="f2be05b2"></span>
## Get playback information

```Dart
// Get playback position, in milliseconds
Duration position = await player.position; 
// Get total duration of the audio/video, in milliseconds
Duration duration = await player.duration;
// Get the duration of playable content that has been buffered, in milliseconds
Duration playableDuration = await player.playableDuration;
// Get the video width and height, in pixels
int videoWidth  = await player.videoWidth;
int videoHeight = await player.videoHeight;
// Check if the current playback is using hardware decoding
bool isHardwareDecode = await player.isHardwareDecode;
// Get the playback state
enum TTVideoEnginePlaybackState {
  stopped(0),
  playing(1),
  paused(2),
  error(3);
}
TTVideoEnginePlaybackState state = await player.getPlaybackState();
```


<span id="6ffe13c6"></span>
## Set callbacks

```Dart
// The player instance provides the following event callbacks:
// Player onPrepared
void Function()? onPrepared;
// Playback state change
void Function(TTVideoEnginePlaybackState playbackState)? playbackStateDidChanged;
// Video load state change
void Function(TTVideoEngineLoadState loadState, Map<Object?, Object?? extraInfo)?
      loadStateDidChanged;

// Callback when the first frame of the video is ready to be displayed
void Function()? readyToDisplay;
// Callback when playback finishes
void Function(TTError? error)? didFinish;
```


In addition to the callbacks above, the player instance provides the following callbacks for the current playback time, the video size, and the video stream bitrate.

```Dart
final player = VodPlayerFlutter();

// Current playback time. position is a non-negative Duration.
player.onCurrentPlaybackTimeUpdate = (position) {
  debugPrint('position=${position.inMilliseconds}ms');
};

// Actual decoded video size, in pixels.
player.onVideoSizeChanged = (width, height) {
  debugPrint('video size: ${width}x$height');
};

// Change in the current video stream bitrate. bitrate is in bps, and resolution can be null.
player.onVideoStreamBitrateChanged = (resolution, bitrate) {
  debugPrint('resolution=$resolution, bitrate=$bitrate bps');
};

await player.createPlayer();

// Optional: The default interval is about 400 ms. You can adjust it after creating the player.
await player.setPlaybackTimeUpdateInterval(
  const Duration(milliseconds: 500),
);
```



|Callback |Parameters |Description |
|---|---|---|
|`onCurrentPlaybackTimeUpdate` |`Duration position` |Receives a non\-negative playback position. Setting a non\-null callback enables the native event, and setting it to null disables the event. The default interval is about 400 ms. |
|`onVideoSizeChanged` |`int width, int height` |Called when the actual decoded video size changes, in pixels. Use it to update the aspect ratio and layout. |
|`onVideoStreamBitrateChanged` |`TTVideoEngineResolutionType? resolution, int bitrate` |Called when the native player reports a change in the video stream bitrate. `bitrate` is in bps. `resolution` is null when it is not reported or the resolution cannot be identified. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">The bitrate callback is triggered when the native player reports a change in the video stream bitrate. It is not necessarily triggered on every manual resolution switch. Whether the callback fires depends on whether the native player produces a corresponding bitrate change event.</div>


When a page is destroyed or high\-frequency events are no longer needed, set the three callbacks to null and call `closeAsync()` to release the player. `closeAsync()` stops the native playback time events.

<span id="87da817d"></span>
## Display current video download progress

The Video SDK supports callbacks for obtaining the size of video data downloaded within a certain time period. This can be used to display the current video download speed during video start, seek, buffering, and other scenarios.

This feature is only available in the Premium Edition.

```Dart
// 1. Set the delegate
TTVideoEnginePreload.setMediaDataLoaderDelegate(<widget>);

// Receive network module callback
  @override
  void ttvideoEngineTestSpeedInfo(Duration durationMs, int sizeByte) {
    double time = durationMs.inMilliseconds / 1000;
    // Time interval in seconds
    double dataSize = sizeByte / 1024;
    // Downloaded data size in KB within the time interval
    double downloadSpeed = dataSize / time;
    // Current video download speed
    print(
        "TTF --  TestSpeedInfo callback, timeInternalMs: $time, size: $sizeByte, speed: $downloadSpeed KB/s");
  }
```


<span id="18e23277"></span>
## Test and debug in arm64 simulator (iOS)

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">This section describes how to test and debug using the simulator. While the simulator provides a convenient environment for UI debugging and early testing, it's essential to remember that it doesn't perfectly replicate real device performance, especially for playback\-related features. For optimal results, we recommend testing these features on a real device.</div>


The BytePlus Player SDK defaults to using [Metal rendering](https://developer.apple.com/metal/). Since simulators do not support Metal rendering, you must configure the SDK to use OpenGL rendering.

```Dart
// Set before calling play(); defaults to false.
 player.setSimulatorEnable(true)
```
