---
title: "Player SDK for Flutter: Basic features"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/player-sdk-for-flutter-basic-features"
---

This topic introduces how to implement the basic features of Player SDK for Flutter.

<span id="b3349bc1"></span>
## Prerequisites

You have integrated and initialized the Player SDK for Flutter. For more information, see [Integrating the Player SDK for Flutter](https://docs.byteplus.com/docs/byteplus-media-live/integrating-the-player-sdk-for-flutter) and [Initializing the Player SDK for Flutter](https://docs.byteplus.com/docs/byteplus-media-live/initializing-the-player-sdk-for-flutter).

<span id="cd2e09da"></span>
## Creating a player and configuring a rendering view

To use the Player SDK for Flutter, you must first create a player. To display the video in the player, you must configure a rendering view.

```Dart
// Create a player. The following example creates a player with a width equal to the screen width and a height equal to 9/16 of the screen height. 
VeLivePlayer manager = await VeLivePlayer.createManager();

@override
Widget build(BuildContext context) {
  return Scaffold(
    body: Container(
      height: MediaQuery.of(context).size.height * 9 / 16,
      width: MediaQuery.of(context).size.width,
      // Configure a rendering view.
      child: VeliveFlutterPlayerView(manager: manager),
    ),
  );
}
```


<span id="72224c5b"></span>
## Initializing player settings

After creating the player, you can initialize its settings using `VeLivePlayerConfiguration`. The following table lists the detailed parameters.


|Parameter |Type |Description |
|---|---|---|
|enableSei |boolean |Whether to enable parsing Supplemental Enhancement Information (SEI) messages. The default value is `false`. Valid values:<br><br><br>* `true`: Enable.<br><br>* `false`: Disable.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">SEI messages are a data channel synchronized with video frames, commonly used to display interactive content at specific time points, such as questions, bullet comments, and virtual props, providing the audience with a richer interactive experience.</div><br> |
|enableHardwareDecode |boolean |Whether to enable hardware decoding. The default value is `true`. Valid values:<br><br><br>* `true`: Enable. If hardware decoding fails, the player automatically switches to software decoding.<br><br>* `false`: Disable. |
|enableLiveDNS |boolean |Whether to enable local DNS pre\-resolution. The default value is `false`. Valid values:<br><br><br>* `true`: Enable. Enabling local DNS pre\-resolution can reduce the playback start time.<br><br>* `false`: Disable.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Problems during pre\-resolution may affect the player's normal operation.</div><br> |
|enableStatisticsCallback |boolean |Whether to enable periodic callback of playback information. The default value is `false`. Valid values:<br><br><br>* `true`: Enable.<br><br>* `false`: Disable. |
|statisticsCallbackInterval |int |Time interval for the periodic callback of playback information. The unit is seconds. The default value is `5`. |
|networkTimeoutMs |int |Network timeout period. The unit is milliseconds. The default value is `5000`.<br><br>If the network request does not receive a server response within the timeout period, the request is considered to have failed. |
|retryIntervalTimeMs |int |Retry interval. The unit is milliseconds. The default value is `5000`.<br><br>During the live stream, if network errors or similar issues cause an interruption, the player will immediately attempt a retry. After a retry attempt fails, the player retries at each retry interval.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter takes effect only when no backup stream is present. If a backup stream is available, the player will directly switch to the backup stream and continue playback in the event of network errors or similar issues.</div><br> |
|retryMaxCount |int |Maximum number of retries for the player in case of network connection errors. The default value is `5`. The value `0` disables the player's internal retry mechanism. |


```Dart
// Initialize the player settings. In the following example, SEI message parsing and hardware decoding are enabled.
VeLivePlayerConfiguration configuration = await VeLivePlayerConfiguration(
      enableSei: true
      enableHardwareDecode: true
    );
await manager.setConfig(configuration);    
```


<span id="9b96cdda"></span>
## Configuring the playback URL

Configure a playback URL supporting RTM, FLV, and HLS live streaming protocols.

```Dart
// Play via URL.
String playUrl = "http://pull.example.com/live/stream.flv"
// Configure the playback URL.
manager.setPlayUrl(playUrl)
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To configure different playback URLs for the player to switch between during playback, use the <code>setPlayStreamData</code> method. This method supports primary and backup streams and adaptive bitrate (ABR) features. For more information, see <a href="https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-advanced-features">Player SDK for Flutter: Advanced features</a>.</div>


<span id="180ccac5"></span>
## Starting playback

```Dart
Future<void> play();
```


<span id="23a7e6fe"></span>
## Checking if the player is playing

```Dart
Future<bool?> isPlaying();
```


<span id="865bd15c"></span>
## Pausing playback

```Dart
Future<void> pause();
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">During the live stream, pausing and stopping playback have the same effect. If you call the <code>play</code> method again after pausing playback, the player will pull stream again.</div>


<span id="e5800925"></span>
## Stopping playback

```Dart
Future<void> stop();
```


<span id="e46d574a"></span>
## Destroying the player

Call this method after playback has stopped to destroy the player and release its associated memory.

```Dart
Future<void> destroy();
```


<span id="19b4ddf5"></span>
## Setting the video scaling mode

You can use the player's `setRenderFillMode` method to set the video scaling mode. The player supports the following video scaling modes.


|Video Scaling Mode |Description |
|---|---|
|aspectfill |Maintain the video's original aspect ratio and fill the player. If the video's aspect ratio differs from that of the player, areas of the video that extend beyond the player's boundaries will be cropped, which may result in an incomplete view. |
|aspectfit |Maintain the video's original aspect ratio until the video is fully displayed within the player. If the video's aspect ratio differs from that of the player, areas not filled by the video will appear black. |
|fullfill |The video completely fills the player, but the video's aspect ratio may change. |


The following sample code sets the video scaling mode.

```Dart
Future<void> setRenderFillMode(VeLivePlayerFillMode fillMode);
```


<span id="343a19dc"></span>
## Muting and unmuting playback

Set whether playback is muted. By default, playback is not muted.

```Dart
Future<void> setMute(bool mute);
```


<span id="348f6dda"></span>
## Getting whether playback is muted

```Dart
Future<bool?> isMute();
```


<span id="83ca7099"></span>
## Setting the video rotation angle

```Dart
enum VeLivePlayerRotation {
  // Disable rotation.
  rotation0,
  // Rotate 90 degrees clockwise.
  rotation90,
  // Rotate 180 degrees clockwise.
  rotation180,
  // Rotate 270 degrees clockwise.
  rotation270,
}

Future<void> setRenderRotation(VeLivePlayerRotation rotation);
```


<span id="18faede6"></span>
## Configuring event listeners

You can receive information about the player's internal status by configuring event listeners, including playback status, error information, audio/video first frame callbacks, and periodic statistical data. The sample code is as follows.


1. Configure the player callback.

   ```Dart
   Future<void> setObserver(VeLivePlayerObserver observer);
   ```
   

2. Handle player callbacks.

   ```Dart
     // This callback is triggered when the player encounters an error.
     void Function(VeLivePlayerError error)? onError;
     
     // This callback is triggered when the first video frame is rendered successfully. This also applies to the first video frame rendered after a successful retry.
     void Function(bool isFirstFrame)? onFirstVideoFrameRender;
     
     // This callback is triggered when the first audio frame is rendered successfully. This also applies to the first audio frame rendered after a successful retry.
     void Function(bool isFirstFrame)? onFirstAudioFrameRender;
     
     // This callback is triggered when the resolution changes.
     void Function(VeLivePlayerResolution resolution, VeLivePlayerError? error, VeLivePlayerResolutionSwitchReason reason)? onResolutionSwitch;
     
     // This callback is triggered when playback stuttering starts.
     void Function()? onStallStart;
     
     // Playback stuttering end callback. This callback is triggered when the audio buffer meets the playback condition and playback starts.
     void Function()? onStallEnd;
     
     // This callback is triggered when the video width or height changes.
     void Function(int width, int height)? onVideoSizeChanged;
     
     // This callback is triggered when video rendering stuttering occurs.
     void Function(int stallTime)? onVideoRenderStall;
     
     // This callback is triggered when audio rendering stuttering occurs.
     void Function(int stallTime)? onAudioRenderStall;
     
     // This callback is triggered when the playback status changes.
     void Function(VeLivePlayerStatus status)? onPlayerStatusUpdate;
     
     // A periodic callback that provides playback statistics, such as the current playback URL, bitrate, and frame rate.
     void Function(VeLivePlayerStatistics statistics)? onStatistics;
     
     // This callback is triggered when the SDK receives SEI messages.
     void Function(String message)? onReceiveSeiMessage;
     
     // This callback is triggered when the primary and backup streams switch.
     void Function(VeLivePlayerStreamType streamType, VeLivePlayerError? error)? onMainBackupSwitch;
   ```
   


<span id="26f4730d"></span>
## Getting the SDK version

```Dart
static Future<String?> getVersion();
```


<span id="a65c2aaa"></span>
## Setting the log level

Set the log level for logs printed to the console.

```Dart
enum VeLivePlayerLogLevel {
  // Output logs at VERBOSE, DEBUG, INFO, WARNING, and ERROR levels.
  verbose,
  // Output logs at DEBUG, INFO, WARNING, and ERROR levels.
  debug,
  // Output logs at INFO, WARNING, and ERROR levels.
  info,
  // Output logs at WARNING and ERROR levels.
  warn,
  // Output logs at ERROR level.
  error,
  // Disable log output.
  none,
}

static Future<void> setLogLevel(VeLivePlayerLogLevel level);
```
