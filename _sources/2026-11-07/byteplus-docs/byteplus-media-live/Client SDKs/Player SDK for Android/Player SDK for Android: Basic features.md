---
title: "Player SDK for Android: Basic features"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-implementing-basic-features-2"
---

This topic introduces how to implement the basic features of Player SDK for Android.

 &nbsp;

<span id="prerequisites"></span>
## Prerequisites

You have integrated and initialized the Player SDK by following the instructions provided in [Integrating the Player SDK for Android](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-android) and [Initializing the Player SDK for Android](https://docs.byteplus.com/docs/byteplus-media-live/docs-initializing-for-android).

 &nbsp;

<span id="notes"></span>
## Notes

The Player SDK uses various Android audio and video APIs that may not work properly on emulators. We recommend using a physical device for debugging.

 &nbsp;

<span id="creating-a-player"></span>
## Creating a player

To implement the basic features of the Player SDK, you must first create a player.

```Java
// Create a player.
VeLivePlayer mLivePlayer = new VideoLiveManager(Env.getApplicationContext());
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="warning">To ensure optimal playback, we recommend creating a new player instance for each playback session instead of reusing an existing instance.</div>


 &nbsp;

<span id="configuring-the-player"></span>
## Configuring the player

Use [VeLivePlayerConfiguration](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerConfiguration) to configure the initial settings of the player, and call [setConfig](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setconfig) to apply the configuration. Complete the configuration before calling [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-play). The following table describes the parameters in `VeLivePlayerConfiguration`.

&nbsp;


|Parameter |Type |Description |
|---|---|---|
|enableSei |boolean |Whether to enable the parsing of string SEI messages. The default value is `false`. |
|enableBinarySei |boolean |Whether to enable the parsing of binary SEI messages. The default value is `false`. When enabled, the player receives binary SEI messages and no longer triggers the string SEI message callback. |
|enableHardwareDecode |boolean |Whether to enable hardware decoding. The default value is `true`. When enabled, the player automatically switches to software decoding if hardware decoding fails to start or fails during playback. |
|networkTimeoutMs |int |The network timeout duration, in milliseconds. The default value is `5000`. After sending a network request, the player considers the request failed if no server response is received within this period. |
|retryIntervalTimeMs |int |The retry interval, in milliseconds. The default value is `5000`. If a network error or similar issue interrupts live playback, the player retries playback at this interval. |
|retryMaxCount |int |The maximum number of retries after a network connection error. The default value is `5`. A value of `0` disables the player's internal retries. |
|stallRetryTimeout |long |The timeout threshold for stopping retries due to stalling, in milliseconds. The default value is `10000` (10 seconds). When the stalling duration exceeds this threshold, the player stops retrying. |
|enableLiveDNS |boolean |Whether to enable local DNS prefetch. The default value is `false`. Enabling local DNS prefetch can reduce the time required to start playback.<br><br><div data-tips="true" data-tips-type="danger" data-tips-is-title="true">Warning</div><br><br><br><div data-tips="true" data-tips-type="danger">An error during local DNS prefetch may affect normal player operation.</div><br> |
|enableStatisticsCallback |boolean |Whether to enable periodic callbacks for playback information. The default value is `false`. |
|statisticsCallbackInterval |int |The time interval for periodic callbacks that provide playback information, in seconds. The default value is `5`. |


The following sample code shows how to configure the initial settings of the player.

```Java
// Create a VeLivePlayerConfiguration instance.
VeLivePlayerConfiguration config = new VeLivePlayerConfiguration();
// Enable periodic callbacks that provide playback information.
config.enableStatisticsCallback = true;
// Enable local DNS prefetch.
config.enableLiveDNS = true;
// Configure the initial settings of the player.
mLivePlayer.setConfig(config);
```


 &nbsp;

<span id="setting-a-player-observer"></span>
## Setting a player observer

Call [setObserver](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setobserver) to set the player observer, and implement the [VeLivePlayerObserver](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#veliveplayerobserver) interface to listen for player status updates, errors, first audio and video frame events, and periodic playback statistics. Set the observer before calling [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-play). The sample code is as follows.

```Java
// Create a player observer instance.
VeLivePlayerObserver mLivePlayerObserver = new VeLivePlayerObserver() {
        
   @Override
   public void onError(VeLivePlayer player, VeLivePlayerError error) {
      // Triggered when a player error occurs.
   }

   @Override
   public void onInfo(VeLivePlayer player, VeLivePlayerError error) {
      // Triggered when the player encounters an internal error.
   }
   
   @Override
   public void onFirstVideoFrameRender(VeLivePlayer player, boolean isFirstFrame) {
      // Triggered when the first video frame is rendered.
   }

   @Override
   public void onFirstAudioFrameRender(VeLivePlayer player, boolean isFirstFrame) {
      // Triggered when the first audio frame is rendered.
   }

   @Override
   public void onStallStart(VeLivePlayer player) {
    // Triggered when a playback stutter starts.
  }

  @Override
   public void onStallEnd(VeLivePlayer player) {
    // Triggered when a playback stutter stops.
  }

  @Override
   public void onVideoRenderStall(VeLivePlayer player, long stallTime) {
    // Triggered when video rendering stalls.
  }

  @Override
   public void onAudioRenderStall(VeLivePlayer player, long stallTime) {
    // Triggered when audio rendering stalls.
  }

  @Override
   public void onResolutionSwitch(VeLivePlayer player, VeLivePlayerDef.VeLivePlayerResolution resolution, VeLivePlayerError error, VeLivePlayerDef.VeLivePlayerResolutionSwitchReason reason) {
    // Triggered when the player switches to a different quality level.
  }

  @Override
   public void onVideoSizeChanged(VeLivePlayer player, int width, int height) {
    // Triggered when the video size changes.
  }

  @Override
   public void onReceiveSeiMessage(VeLivePlayer player, String message) {
    // Triggered when the player receives a string SEI message.
  }

  @Override
   public void onReceiveBinarySeiMessage(VeLivePlayer player, byte[] message) {
    // Triggered when the player receives a binary SEI message. Enable enableBinarySei to receive this callback. When enabled, the string SEI message callback is no longer triggered.
  }

  @Override
   public void onMainBackupSwitch(VeLivePlayer player, VeLivePlayerDef.VeLivePlayerStreamType streamType, VeLivePlayerError error) {
    // Triggered when the player switches between the primary and backup streams.
  }

  @Override
   public void onStreamFormatSwitch(VeLivePlayer player, VeLivePlayerDef.VeLivePlayerFormat fromStreamFormat, VeLivePlayerDef.VeLivePlayerFormat toStreamFormat, VeLivePlayerError error, Bundle extraInfo) {
    // Triggered when the player switches the stream format.
  }

  @Override
   public void onPlayerStatusUpdate(VeLivePlayer player, VeLivePlayerDef.VeLivePlayerStatus status) {
    // Triggered when the player status changes.
  }

  @Override
   public void onPlayerStatusUpdate(VeLivePlayer player, VeLivePlayerDef.VeLivePlayerStatus status, Bundle extraInfo) {
    // Triggered when the player status changes. The extraInfo parameter provides supplemental information about the current playback stream.
  }

  @Override
   public void onStatistics(VeLivePlayer player, VeLivePlayerStatistics statistics) {
    // Triggered periodically to report playback statistics.
  }

  @Override
   public void onSnapshotComplete(VeLivePlayer player, Bitmap bitmap) {
    // Triggered when a screenshot is taken.
  }

  @Override
   public void onRenderVideoFrame(VeLivePlayer player, VeLivePlayerVideoFrame videoFrame) {
    // Triggered when the player decodes a video frame.
  }

  @Override
   public void onRenderAudioFrame(VeLivePlayer player, VeLivePlayerAudioFrame audioFrame) {
    // Triggered when the player decodes an audio frame.
  }

  @Override
   public void onStreamFailedOpenSuperResolution(VeLivePlayer player, VeLivePlayerError error) {
    // Triggered when the SDK fails to enable super resolution.
  }

  @Override
   public void onStreamFailedOpenSharpen(VeLivePlayer player, VeLivePlayerError error) {
    // Triggered when the SDK fails to enable video sharpening.
  }
};

// Set the player observer.
mLivePlayer.setObserver(mLivePlayerObserver);
```


 &nbsp;

<span id="setting-the-player-view"></span>
## Setting the rendering view

For the player to display the video, you need to set a view for video rendering. The player provides two rendering view options: `SurfaceView` and `TextureView`.

&nbsp;


|Dimension |SurfaceView |TextureView |
|---|---|---|
|Characteristics |Provides an independent drawing surface and efficient rendering for complex UI. |Works as a regular view and supports animations and transformations. |
|Thread |Draws on a separate thread and does not occupy main\-thread resources. |Uses the same lifecycle as the `Activity` or `Fragment`. |
|Recommended scenarios |Complex UI rendering, efficient drawing, games, and similar scenarios. |Image display, animation effects, and scenarios that require compatibility with regular views. |


Choose the rendering view based on your needs and refer to the following sample code for configuration.

 &nbsp;

<span id="setting-surfaceview"></span>
### Setting SurfaceView


1. Declare `SurfaceView` in the layout XML file.

   ```XML
   <SurfaceView
       android:id="@+id/surfaceView"
       android:layout_width="match_parent"
       android:layout_height="match_parent" />
   ```
   

2. Call [setSurfaceHolder](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setsurfaceholder) to configure video rendering with `SurfaceView`.

   ```Java
   SurfaceView surfaceView = findViewById(R.id.surfaceView);
   mLivePlayer.setSurfaceHolder(surfaceView.getHolder());
   ```
   


<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="danger">If you use <code>SurfaceView</code> to render video frames, your device's API level must be 24 or higher. Otherwise, view hierarchy issues, out\-of\-sync animations, or other issues may occur. If your device's API level is lower than 24, we recommend that you use other rendering methods or upgrade the API level for the best playback experience.</div>


 &nbsp;

<span id="setting-textureview"></span>
### Setting TextureView


1. Declare `TextureView` in the layout XML file.

   ```XML
   <TextureView
       android:id="@+id/textureView"
       android:layout_width="match_parent"
       android:layout_height="match_parent"
       android:background="@null" />
   ```
   

2. Call [setSurface](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setsurface) to configure video rendering with `TextureView`.

   ```Java
   TextureView textureView = findViewById(R.id.textureView);
   
   // Configure the SurfaceTexture listener.
   textureView.setSurfaceTextureListener(new TextureView.SurfaceTextureListener() {
   
       @Override
       public void onSurfaceTextureAvailable(SurfaceTexture surfaceTexture, int width, int height) {
          // Triggered when the SurfaceTexture for the TextureView is available.
           mLivePlayer.setSurface(new Surface(surfaceTexture));
       }
       
       @Override
       public void onSurfaceTextureSizeChanged(SurfaceTexture surfaceTexture, int width, int height) { 
           // Triggered when the size of TextureView changes.
       }
       
       @Override
       public boolean onSurfaceTextureDestroyed(SurfaceTexture surfaceTexture) {
          // Triggered when the SurfaceTexture is about to be destroyed. Return true to have TextureView release the SurfaceTexture automatically. If this method returns false, manually release the SurfaceTexture by calling surfaceTexture.release().
           return true;
       }
       
       @Override
       public void onSurfaceTextureUpdated(SurfaceTexture surfaceTexture) {
          // Triggered when the TextureView is updated.    
       }
   });
   ```
   


 &nbsp;

<span id="setting-the-playback-url"></span>
## Setting the playback URL

Call [setPlayUrl](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setplayurl) to set a single playback URL. The method supports live streaming protocols such as RTMP, FLV, and HLS. Replace the URL in the sample code with your actual live playback URL. Call this method before calling [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-play). The sample code is as follows.

```Java
String playUrl = "http://pull.example.com/live/stream.flv";
mLivePlayer.setPlayUrl(playUrl); // Set the playback URL.
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">To configure multiple playback URLs, call <a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setplaystreamdata">setPlayStreamData</a>. This method supports features such as RTM stream pulling, QUIC stream pulling, primary\-backup stream switching, multiple quality levels, and adaptive bitrate (ABR). Call this method before calling <a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-play">play</a>. For more information, see <a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2">Player SDK for Android: Advanced features</a>.</div>


 &nbsp;

<span id="adjusting-the-playback-screen"></span>
## Adjusting the playback screen

You can configure the fill mode, mirroring, and rotation for a better playback experience.

 &nbsp;

<span id="setting-the-fill-mode"></span>
### Setting the fill mode

Call [setRenderFillMode](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setrenderfillmode) to set the fill mode of the playback screen. The player supports the following fill modes.

&nbsp;


|Fill mode |Description |
|---|---|
|VeLivePlayerFillModeAspectFit |Displays the complete video frame. The video frame is scaled proportionally until the entire frame fits within the canvas. If the aspect ratio of the video frame differs from that of the canvas, the unfilled area is displayed in black. |
|VeLivePlayerFillModeFullFill |Adapts the video frame to the canvas. The video frame is scaled non\-proportionally until the canvas is filled. The aspect ratio of the video frame may change during this process. |
|VeLivePlayerFillModeAspectFill |Fills the canvas with the video. The video frame is scaled proportionally until the canvas is filled. Parts of the video frame that extend beyond the screen are cropped. As a result, some parts of the video frame may not be visible. |


```Java
// Set the fill mode to aspect fill.
mLivePlayer.setRenderFillMode(VeLivePlayerFillModeAspectFill);
```


 &nbsp;

<span id="setting-the-mirroring"></span>
### Setting mirroring

Call [setRenderMirror](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setrendermirror) to set the mirroring mode of the playback screen. The player supports the following mirroring modes.

&nbsp;


|Mirroring mode |Description |
|---|---|
|VeLivePlayerMirrorNone |No mirroring. |
|VeLivePlayerMirrorHorizontal |Horizontal mirroring. |
|VeLivePlayerMirrorVertical |Vertical mirroring. |


```Java
// Set horizontal mirroring.
mLivePlayer.setRenderMirror(VeLivePlayerMirrorHorizontal);
```


 &nbsp;

<span id="setting-the-rotation-angle"></span>
### Setting the rotation angle

Call [setRenderRotation](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setrenderrotation) to set the rotation angle of the playback screen. The player supports the following rotation angles.

&nbsp;


|Rotation angle |Description |
|---|---|
|VeLivePlayerRotation0 |No rotation. |
|VeLivePlayerRotation90 |Rotates the video 90 degrees clockwise. |
|VeLivePlayerRotation180 |Rotates the video 180 degrees clockwise. |
|VeLivePlayerRotation270 |Rotates the video 270 degrees clockwise. |


```Java
// Rotate the video 90 degrees clockwise.
mLivePlayer.setRenderRotation(VeLivePlayerRotation90);
```


 &nbsp;

<span id="starting-playback"></span>
## Starting playback

Call [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-play) to start playback.

```Java
mLivePlayer.play(); // Start playback.
```


You can call [isPlaying](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-isplaying) to get the current playback status.

```Java
boolean isPlaying = mLivePlayer.isPlaying(); // Get the playback status.
```


 &nbsp;

<span id="stopping-playback"></span>
## Stopping playback

Call [stop](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-stop) to stop playback. Calling `stop` does not destroy the player.

```Java
mLivePlayer.stop(); // Stop playback.
```


 &nbsp;

<span id="destroying-the-player"></span>
## Destroying the player

After stopping playback, if you no longer need the player, call [destroy](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-destroy) to destroy the player and release its associated memory.

```Java
mLivePlayer.destroy(); // Destroy the player and release its associated memory.
```


 &nbsp;

<span id="setting-the-background-mode"></span>
## Handling app foreground and background transitions

By default, the player continues playing audio after the app enters the background. To prevent audio from continuing in the background, stop playback when the app enters the background and resume playback when the app returns to the foreground, as shown in the following code:

```Java
@Override
protected void onResume() {
    super.onResume();
    if (mLivePlayer != null) {
        mLivePlayer.play(); // Resume playback when the app switches to the foreground.
    }
}
 
@Override
protected void onPause() {
    super.onPause();
    if (mLivePlayer != null) {
        mLivePlayer.stop(); // Stop playback when the app switches to the background.
    }
}
```


 &nbsp;

<span id="muting"></span>
## Muting

Call [setMute](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setmute) to mute or unmute the audio.

```Java
mLivePlayer.setMute(true); // Mute playback.
```


You can query whether the audio is muted by calling [isMute](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-ismute).

```Java
boolean isMute = mLivePlayer.isMute(); // Get the mute status.
```


 &nbsp;

<span id="setting-the-player-volume"></span>
## Setting the player volume

Call [setPlayerVolume](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setplayervolume) to set the player volume. The parameter specifies the volume level. The default value is `1.0`. The valid range is `[0.0, 1.0]`.

```Java
mLivePlayer.setPlayerVolume(0.5f); // Set the player volume.
```


 &nbsp;

<span id="setting-log-level"></span>
## Setting the log level

Call [setLogLevel](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setloglevel) to set the level of logs printed to the console.

```Java
// Sets the log level to DEBUG. Logs at the DEBUG, INFO, WARNING, and ERROR levels will be output.
VeLivePlayer.setLogLevel(VeLivePlayerLogConfig.VeLivePlayerLogLevel.VeLivePlayerLogLevelDebug);
```
