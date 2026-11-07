---
title: "Player SDK for iOS: Basic features"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-implementing-basic-features-3"
---

This topic introduces how to implement the basic features of Player SDK for iOS.

 &nbsp;

<span id="prerequisite"></span>
## Prerequisite

You have integrated and initialized the Player SDK by following the instructions provided in [Integrating the Player SDK for iOS](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-ios) and [Initializing the Player SDK for iOS](https://docs.byteplus.com/docs/byteplus-media-live/docs-initializing-for-ios).

 &nbsp;

<span id="notes"></span>
## Notes

The Player SDK uses various iOS audio and video APIs that may not work properly on simulators. We recommend using a physical device for debugging.

 &nbsp;

<span id="creating-a-player"></span>
## Creating a player

The player class in the Player SDK for iOS is `TVLManager`. The following sample code creates a player.

```objectivec
TVLManager *livePlayer = [[TVLManager alloc] init];
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>



* <div data-tips="true" data-tips-type="tip">Select an initialization method based on the player type:</div>


   * <div data-tips="true" data-tips-type="tip"><code>VeLivePlayerTypeOwn</code>: The SDK's built\-in player. Calling <a href="https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#init">init</a> creates this type of player. You can also call <a href="https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#initwithtype">initWithType:</a> and pass <code>VeLivePlayerTypeOwn</code>. Only this type supports <a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#picture-in-picture">Picture in Picture</a>.</div>


   * <div data-tips="true" data-tips-type="tip"><code>VeLivePlayerTypeSystem</code>: The system player. To create this type of player, call <a href="https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#initwithtype">initWithType:</a> and pass <code>VeLivePlayerTypeSystem</code>. Use this type to play DRM\-encrypted streams. For more information, see <a href="https://docs.byteplus.com/en/docs/byteplus-media-live/docs-implementing-advanced-features-3#playing-a-drm-encrypted-stream">Playing a DRM\-encrypted stream</a>. This type supports only M3U8 pull stream addresses and does not support the following features:</div>


      * <div data-tips="true" data-tips-type="tip">Primary\-backup stream switching</div>


      * <div data-tips="true" data-tips-type="tip">Adaptive bitrate (ABR) stream pulling</div>


      * <div data-tips="true" data-tips-type="tip">Snapshot capturing</div>


      * <div data-tips="true" data-tips-type="tip">Video mirroring</div>


      * <div data-tips="true" data-tips-type="tip">Custom audio and video rendering</div>


      * <div data-tips="true" data-tips-type="tip">Super\-resolution</div>


      * <div data-tips="true" data-tips-type="tip">Supplemental Enhancement Information (SEI)</div>


* <div data-tips="true" data-tips-type="tip">To ensure optimal playback, we recommend creating a new player instance for each playback session instead of reusing an existing instance.</div>



 &nbsp;

<span id="configuring-the-player"></span>
## Configuring the player

Use [VeLivePlayerConfiguration](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#veliveplayerconfiguration) to configure the initial settings of the player, and call [setConfig:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#setconfig) to apply the configuration. Complete the configuration before calling [play](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#play). The following table describes the parameters in `VeLivePlayerConfiguration`.

&nbsp;


|Parameter |Type |Description |
|---|---|---|
|enableSei |BOOL |Whether to enable the parsing of string SEI messages. The default value is `NO`. |
|enableBinarySei |BOOL |Whether to enable the parsing of binary SEI messages. The default value is `NO`. When enabled, the player receives binary SEI messages and no longer triggers the string SEI message callback. |
|enableHardwareDecode |BOOL |Whether to enable hardware decoding. The default value is `YES`. When enabled, the player automatically switches to software decoding if hardware decoding fails to start or fails during playback. |
|networkTimeoutMs |NSInteger |The network timeout duration, in milliseconds. The default value is `5000`. After sending a network request, the player considers the request failed if no server response is received within this period. |
|retryIntervalTimeMs |NSInteger |The retry interval, in milliseconds. The default value is `5000`. If a network error or similar issue interrupts live playback, the player retries playback at this interval. |
|retryMaxCount |NSInteger |The maximum number of retries after a network connection error. The default value is `5`. A value of `0` disables the player's internal retries. |
|stallRetryTimeout |NSInteger |The timeout threshold for stopping retries due to stalling, in milliseconds. The default value is `10000` (10 seconds). When the stalling duration exceeds this threshold, the player stops retrying. |
|enableLiveDNS |BOOL |Whether to enable local DNS prefetch. The default value is `YES`. Enabling local DNS prefetch can reduce the time required to start playback.<br><br><div data-tips="true" data-tips-type="danger" data-tips-is-title="true">Warning</div><br><br><br><div data-tips="true" data-tips-type="danger">An error during local DNS prefetch may affect normal player operation.</div><br> |
|enableStatisticsCallback |BOOL |Whether to enable periodic callbacks for playback information. The default value is `NO`. |
|statisticsCallbackInterval |NSInteger |The time interval for periodic callbacks that provide playback information, in seconds. The default value is `5`. |


The following sample code shows how to configure the initial settings of the player.

```objectivec
// Create a VeLivePlayerConfiguration instance.
VeLivePlayerConfiguration *config = [[VeLivePlayerConfiguration alloc] init];
// Enable periodic callbacks that provide playback information.
config.enableStatisticsCallback = YES;
// Enable local DNS prefetch.
config.enableLiveDNS = YES;
// Configure the initial settings of the player.
[self.livePlayer setConfig:config];
```


 &nbsp;

<span id="setting-a-player-observer"></span>
## Setting a player observer

Call [setObserver:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#setobserver) to set the player observer, and use the [VeLivePlayerObserver](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver) protocol to listen for player status updates, errors, first audio and video frame events, and periodic playback statistics. Set the observer before calling [play](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#play). The sample code is as follows.


1. Set the player observer.

   ```objectivec
   @interface VeLivePullViewController () <VeLivePlayerObserver>
   @end
   
   // Set the player observer.
   [self.livePlayer setObserver:self];
   ```
   

2. Handle the player events.

   ```objectivec
   - (void)onError:(TVLManager *)player error:(VeLivePlayerError *)error {
       // Triggered when a player error occurs.
   }
   
   - (void)onInfo:(TVLManager *)player info:(VeLivePlayerError *)info {
       // Triggered when the player encounters an internal error.
   }
   
   - (void)onFirstVideoFrameRender:(TVLManager *)player isFirstFrame:(BOOL)isFirstFrame {
       // Triggered when the first video frame is rendered.
   }
   
   - (void)onFirstAudioFrameRender:(TVLManager *)player isFirstFrame:(BOOL)isFirstFrame {
       // Triggered when the first audio frame is rendered.
   }
   
   - (void)onStallStart:(TVLManager *)player {
       // Triggered when a playback stutter starts.
   }
   
   - (void)onStallEnd:(TVLManager *)player {
       // Triggered when a playback stutter stops.
   }
   
   - (void)onVideoRenderStall:(TVLManager *)player stallTime:(int64_t)stallTime  {
       // Triggered when video rendering stalls.
   }
   
   - (void)onAudioRenderStall:(TVLManager *)player stallTime:(int64_t)stallTime  {
       // Triggered when audio rendering stalls.
   }
   
   - (void)onResolutionSwitch:(TVLManager *)player resolution:(VeLivePlayerResolution)resolution error:(VeLivePlayerError *)error reason:(VeLivePlayerResolutionSwitchReason)reason  {
       // Triggered when the player switches to a different quality level.
   }
   
   - (void)onVideoSizeChanged:(TVLManager *)player width:(int)width height:(int)height  {
       // Triggered when the video size changes.
   }
   
   - (void)onReceiveSeiMessage:(TVLManager *)player message:(NSString *)message  {
       // Triggered when the player receives a string SEI message.
   }
   
   - (void)onReceiveBinarySeiMessage:(TVLManager *)player message:(NSData *)message  {
       // Triggered when the player receives a binary SEI message. Enable enableBinarySei to receive this callback. When enabled, the string SEI message callback is no longer triggered.
   }
   
   - (void)onMainBackupSwitch:(TVLManager *)player streamType:(VeLivePlayerStreamType)streamType error:(VeLivePlayerError *)error  {
       // Triggered when the player switches between the primary and backup streams.
   }
   
   - (void)onStreamFormatSwitch:(TVLManager *)player fromStreamFormat:(VeLivePlayerFormat)fromStreamType toStreamFormat:(VeLivePlayerFormat)toStreamType error:(VeLivePlayerError *)error extraInfo:(NSDictionary *)extraInfo {
       // Triggered when the player switches the stream format.
   }
   
   - (void)onPlayerStatusUpdate:(TVLManager *)player status:(VeLivePlayerStatus)status  {
       // Triggered when the player status changes.
   }
   
   - (void)onPlayerStatusUpdate:(TVLManager *)player status:(VeLivePlayerStatus)status extraInfo:(NSDictionary *)extraInfo  {
       // Triggered when the player status changes. The extraInfo parameter provides supplemental information about the current playback stream.
   }
   
   - (void)onStatistics:(TVLManager *)player statistics:(VeLivePlayerStatistics *)statistics {
       // Triggered periodically to report playback statistics.
   }
   
   - (void)onSnapshotComplete:(TVLManager *)player image:(UIImage *)image  {
       // Triggered when a screenshot is taken.
   }
   
   - (void)onRenderVideoFrame:(TVLManager *)player videoFrame:(VeLivePlayerVideoFrame *)videoFrame  {
       // Triggered when the player decodes a video frame.
   }
   
   - (void)onRenderAudioFrame:(TVLManager *)player audioFrame:(VeLivePlayerAudioFrame *)audioFrame  {
       // Triggered when the player decodes an audio frame.
   }
   
   - (void)onStreamFailedOpenSuperResolution:(TVLManager *)player error:(VeLivePlayerError *)error {
       // Triggered when the SDK fails to enable super resolution.
   }
   ```
   


 &nbsp;

<span id="setting-the-player-view"></span>
## Setting the player view

Add [playerView](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#playerview) to your custom view to render the video.

```objectivec
// Use Metal for rendering.
self.livePlayer.playerViewRenderType = TVLPlayerViewRenderTypeMetal;

// Set the size of the playerView.
self.livePlayer.playerView.frame = UIScreen.mainScreen.bounds;

// Add playerView as a subview to your custom view.
[self.view addSubview:self.livePlayer.playerView];
```


 &nbsp;

<span id="setting-the-playback-url"></span>
## Setting the playback URL

Call [setPlayUrl:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#setplayurl) to set a single playback URL. The method supports live streaming protocols such as RTMP, FLV, and HLS. Replace the URL in the sample code with your actual live playback URL. Call this method before calling [play](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#play). The sample code is as follows.

```objectivec
NSString *playUrl = @"http://pull.example.com/live/stream.flv";
[self.livePlayer setPlayUrl:playUrl]; // Set the playback URL.
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">To configure multiple playback URLs, call <a href="https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#setplaystreamdata">setPlayStreamData:</a>. This method supports features such as RTM stream pulling, QUIC stream pulling, primary\-backup stream switching, multiple quality levels, and adaptive bitrate (ABR). Call this method before calling <a href="https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#play">play</a>. For more information, see <a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3">Player SDK for iOS: Advanced features</a>.</div>


 &nbsp;

<span id="adjusting-the-playback-screen"></span>
## Adjusting the playback screen

You can configure the fill mode, mirroring, and rotation for a better playback experience.

 &nbsp;

<span id="setting-the-fill-mode"></span>
### Setting the fill mode

Call [setRenderFillMode:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#setrenderfillmode) to set the fill mode of the playback screen. The player supports the following fill modes.

&nbsp;


|Fill mode |Description |
|---|---|
|VeLivePlayerFillModeAspectFit |Displays the complete video frame. The video frame is scaled proportionally until the entire frame fits within the canvas. If the aspect ratio of the video frame differs from that of the canvas, the unfilled area is displayed in black. |
|VeLivePlayerFillModeFullFill |Adapts the video frame to the canvas. The video frame is scaled non\-proportionally until the canvas is filled. The aspect ratio of the video frame may change during this process. |
|VeLivePlayerFillModeAspectFill |Fills the canvas with the video. The video frame is scaled proportionally until the canvas is filled. Parts of the video frame that extend beyond the screen are cropped. As a result, some parts of the video frame may not be visible. |


```objectivec
// Set the fill mode to aspect fill.
[self.livePlayer setRenderFillMode:VeLivePlayerFillModeAspectFill];
```


 &nbsp;

<span id="setting-mirroring"></span>
### Setting mirroring

Call [setRenderMirror:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setrendermirror) to set the mirroring of the playback screen. The player supports the following mirroring modes.

&nbsp;


|Mirroring mode |Description |
|---|---|
|VeLivePlayerMirrorNone |No mirroring. |
|VeLivePlayerMirrorHorizontal |Horizontal mirroring. |
|VeLivePlayerMirrorVertical |Vertical mirroring. |


```objectivec
// Set horizontal mirroring.
[self.livePlayer setRenderMirror:VeLivePlayerMirrorHorizontal];
```


 &nbsp;

<span id="setting-the-rotation-angle"></span>
### Setting the rotation angle

Call [setRenderRotation:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#setrenderrotation) to set the rotation angle of the playback screen. The player supports the following rotation angles.

&nbsp;


|Rotation angle |Description |
|---|---|
|`VeLivePlayerRotation0` |No rotation. |
|`VeLivePlayerRotation90` |Rotates the video 90 degrees clockwise. |
|`VeLivePlayerRotation180` |Rotates the video 180 degrees clockwise. |
|`VeLivePlayerRotation270` |Rotates the video 270 degrees clockwise. |


```objectivec
// Rotate the video 90 degrees clockwise.
[self.livePlayer setRenderRotation:VeLivePlayerRotation90];
```


 &nbsp;

<span id="starting-playback"></span>
## Starting playback

Call [play](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#play) to start playback.

```objectivec
[self.livePlayer play]; // Start playback.
```


You can call [isPlaying](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#isplaying) to get the current playback status.

```objectivec
BOOL isPlaying = [self.livePlayer isPlaying]; // Get the playback status.
```


 &nbsp;

<span id="stopping-playback"></span>
## Stopping playback

Call [stop](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#stop) to stop playback. Calling `stop` does not destroy the player.

```objectivec
[self.livePlayer stop]; // Stop playback.
```


 &nbsp;

<span id="destroying-the-player"></span>
## Destroying the player

After stopping playback, if you no longer need the player, call [destroy](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#destroy) to destroy the player and release its associated memory.

```objectivec
[self.livePlayer destroy]; // Destroy the player and release its associated memory.
```


 &nbsp;

<span id="setting-the-background-mode"></span>
## Handling app foreground and background transitions

By default, the player continues playing audio after the app enters the background. To prevent audio from continuing in the background, stop playback when the app enters the background and resume playback when the app returns to the foreground, as shown in the following code:

```objectivec
// Add an observer to listen for the notification when the app switches to the foreground.
[NSNotificationCenter.defaultCenter addObserver:self
            selector:@selector(applicationDidBecomeActive:)
            name:UIApplicationDidBecomeActiveNotification
            object:nil];
// Add an observer to listen for the notification when the app switches to the background.
[NSNotificationCenter.defaultCenter addObserver:self
            selector:@selector(applicationWillResignActive:)
            name:UIApplicationWillResignActiveNotification
            object:nil];

- (void)applicationDidBecomeActive:(NSNotification *)notification {
    [self.livePlayer play]; // Resume playback when the app switches to the foreground.
}

- (void)applicationWillResignActive:(NSNotification *)notification {
    [self.livePlayer stop]; // Stop playback when the app switches to the background.
}
```


 &nbsp;

<span id="muting-playback"></span>
## Muting playback

Call [setMute:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#setmute) to mute or unmute the audio.

```objectivec
[self.livePlayer setMute:YES]; // Mute playback.
```


You can query whether the audio is muted by calling [isMute](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#ismute).

```objectivec
BOOL isMute = [self.livePlayer isMute]; // Get the mute status.
```


 &nbsp;

<span id="setting-the-player-volume"></span>
## Setting the player volume

Use the [volume](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#volume) property to set the player volume. The property specifies the volume level. The default value is `1.0`. The valid range is `[0.0, 1.0]`.

```objectivec
[self.livePlayer setVolume:0.5];
```


 &nbsp;

<span id="setting-log-level"></span>
## Setting the log level

Call [setLogLevel:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#setloglevel) to set the level of logs printed to the console.

```objectivec
// Sets the log level to INFO. Logs at the INFO, WARNING, and ERROR levels will be output.
[TVLManager setLogLevel:VeLivePlayerLogLevelInfo];
```


 &nbsp;

<span id="troubleshooting"></span>
## Troubleshooting

Error: Cannot remove an observer <TTAVPlayerItem 0x2806577a0\> for the key path "status" from <TVLOwnPlayer 0x2817e9290\> because it is not registered as an observer

This error may occur if the live player's methods are called from different threads. To prevent this error, ensure that the live player's methods are called from the main thread.
