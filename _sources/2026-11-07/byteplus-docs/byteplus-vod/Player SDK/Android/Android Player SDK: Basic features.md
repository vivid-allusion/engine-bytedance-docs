---
title: "Android Player SDK: Basic features"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-implementing-basic-features-android"
---

This article introduces how to implement the basic features of the Android Player SDK.

<span id="5246d934"></span>
## Prerequisites

To create the environment necessary to implement the basic features in your app, ensure that you have integrated the SDK and implemented the playback feature in [Getting Started with the SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-getting-started-with-the-android-player-sdk).

<span id="34302a94"></span>
## Playback control

`TTVideoEngine` offers a playback control method similar to the Android system's `MediaPlayer`.

<span id="04ecb4f8"></span>
### Play

Call `play` to start or resume video playback. The example code is shown below.

```Java
ttVideoEngine.play(); // "Start playing or resume playback"
```


<span id="eb1e09e1"></span>
### Pause

Call `pause` to pause video playback. Call `play` again to pause the status and resume playback. The example code is shown below.

```java
ttVideoEngine.pause(); // Pause the playback
ttVideoEngine.play(); // The player transitions from pause to play state.
```


<span id="96e695ab"></span>
### Seek to a specific position and play

Call `seekTo` to seek to a specific position and play. This realizes the function of dragging the progress bar to a specific time and playing. The example code is shown below.

```java
/** Demonstrate seeking to the 1-second position. */
ttVideoEngine.seekTo(1000, new SeekCompletionListener() {
    @Override
    public void onCompletion(boolean success) {
        // Callback after the seek operation is completed. The success parameter indicates whether the seek was successful. true: successful.
    }
});

ttVideoEngine.setVideoEngineInfoListener(new VideoEngineInfoListener() {
    @Override
    public void onVideoEngineInfos(VideoEngineInfos videoEngineInfos) {
        if (TextUtils.equals(videoEngineInfos.getKey(), VideoEngineInfos.USING_RENDER_SEEK_COMPLETE)) {
            // Seek render completion callback.
        }
    }
});
```


<span id="935717bb"></span>
### Play from a specific time

Before calling `play`, specify the playback start time using `setStartTime` to realize functions such as starting playback from a specific time or skipping the title sequence. Example code:

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="warning">Combining pre\-rendering with a specified playback start time requires the Android Player SDK <code>1.52.100.5</code> or later. Set the start time before calling <code>prepare</code> and enable <code>PLAYER_OPTION_ENABLE_START_TIME_SKIP_AVSKIPSERIAL</code>. For configuration details, see <a href="https://docs.byteplus.com/docs/byteplus-vod/docs-android-player-short-video-best-practices#prerender-with-start-time">Pre\-rendering with a specified start time</a>.</div>


```java
int startPlayPositionMS = 1000; // Unit ms
ttVideoEngine.setStartTime(startPlayPositionMS); // Start playing from 1 second.
ttVideoEngine.play();
```


<span id="aabffa02"></span>
### Stop

Call `stop` to stop video playback. The example code is shown below.

```java
ttVideoEngine.stop(); // Stop playback.
```


<span id="9c40bf02"></span>
### Release

Call `releaseAsync` to asynchronously release the player instance. The example code is shown below.

```java
ttVideoEngine.releaseAsync(); // Asynchronously release the player instance.
boolean isReleased = ttVideoEngine.isReleased(); //Get release status.
ttVideoEngine = null; // Prevent repeated calls.
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>



* <div data-tips="true" data-tips-type="tip">Once the player is released, no further functions should be called.</div>


* <div data-tips="true" data-tips-type="tip">After release, you can set the <code>TTVideoEngine</code> to <code>null</code> to prevent it from being called again.</div>



<span id="ea0a7789"></span>
### Audio\-only playback

The Player SDK supports only decoding audio instead of video when playing videos, which is suitable for audio\-only playback scenarios. The SDK is more energy\-efficient than audio\-only playback implemented according to your own business logic, as it only decodes the audio.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="warning">This feature is only supported by the Premium and Enterprise editions. Make sure you have purchased a Premium or Enterprise license. For details, see <a href="https://docs.byteplus.com/en/docs/byteplus-vod/docs-license-management">Licenses</a>.</div>


```java
// Play audio only
ttVideoEngine.setRadioMode(true);
// play both audio and video
ttVideoEngine.setRadioMode(false);
```


<span id="2387b893"></span>
## Play DASH videos

To play DASH videos smoothly, enable the following options before playing:

```Java
ttVideoEngine.setIntOption(TTVideoEngineInterface.PLAYER_OPTION_ENABLE_DASH, 1);
ttVideoEngine.setIntOption(TTVideoEngineInterface.PLAYER_OPTION_ENABLE_BASH, 1);
```


To play standard DASH videos, enable the following options before playing:

```Java
// Global setting. Must be called before initializing the SDK.
TTVideoEngine.setIntValue(DataLoaderHelper.DATALOADER_KEY_ENABLE_DASH_PROXY, 1);

// Per-instance setting to enable the DASH proxy for this specific playback.
mVideoEngine.setIntOption(TTVideoEngine.PLAYER_OPTION_ENABLE_DASHPROXY_VV, 1);
```


<span id="665ec4e3"></span>
## Display mode

The Android Player SDK supports display modes such as fill, rotate, and mirror.

<span id="7a988183"></span>
### Fill mode

If the **video aspect ratio** is not consistent with the **size of the playback controls**, this can result in the video being stretched. You can set different display modes by configuring the `displayMode` and `disPlayView` parameters. The example code is shown below.

```java
// "No distortion; proportional scaling; the image is not cropped; there may be black borders.
int displayMode1 = TTVideoEngineInterface.IMAGE_LAYOUT_ASPECT_FIT;
// May be distorted; the image fills the entire width and height of the control; the image is not cropped; no black borders.
int displayMode2 = TTVideoEngineInterface.IMAGE_LAYOUT_TO_FILL;
// No distortion; proportional scaling; the image may be cropped; no black borders.
int displayMode3 = TTVideoEngineInterface.IMAGE_LAYOUT_ASPECT_FILL;
// No distortion; the width fills the control, and the height is adapted according to the video aspect ratio; the image may be cropped; there may be black borders. This does not take effect when Texturerender is enabled.
int displayMode4 = TTVideoEngineInterface.IMAGE_LAYOUT_ASPECT_FILL_X;
// No distortion; the height fills the control, and the width is adapted according to the video aspect ratio; the image may be cropped; there may be black borders. This does not take effect when Texturerender is enabled.
int displayMode5 = TTVideoEngineInterface.IMAGE_LAYOUT_ASPECT_FILL_Y;

View disPlayView = findViewById(R.id.textureView);
// View disPlayView = findViewById(R.id.surfaceView);

// The parameter disPlayView is the TextureView or SurfaceView that displays the image.
// The parameter displayMode values are shown in the table below.
ttvideoEngine.setDisplayMode(disPlayView, displayMode1);
```


<span id="161eace3"></span>
### Rotation

Follow the steps below to implement the rotation function:


1. After initializing the player and before calling `play`, use `setIntOption` to enable Texture Render. Example code:

   ```java
   // Set before calling play.
   ttvideoEngine.setIntOption(TTVideoEngine.PLAYER_OPTION_USE_TEXTURE_RENDER, 1);
   ```
   

2. After calling `play`, call `setRotation` to set the rotation angle for video display. After configuring, the video will rotate clockwise. Example code:

   ```java
   int rotation = 90; // Rotation angles only support 0°/90°/180°/270°, other values are invalid.
   ttvideoEngine.setRotation(rotation); // Set the rotation angle for video display, to be configured after calling play.
   ```
   


<span id="a6f92c89"></span>
### Mirroring

Call `setMirrorHorizontal` and `setMirrorVertical` to configure horizontal and vertical mirroring.

```java
// Set horizontal mirroring.
boolean  mirrorHorizontal = true;
ttVideoEngine.setMirrorHorizontal(mirrorHorizontal);
// Set vertical mirroring.
boolean  mirrorVertical = true;
ttVideoEngine.setMirrorVertical(mirrorVertical);
```


<span id="f3c51f32"></span>
## Fetching the video width and height

After the `TTVideoEngine` triggers the `onPrepared` callback, call `getVideoWidth` and `getVideoHeight` to fetch the width and height of the video. Example code:

```Java
int videoWidth = ttVideoEngine.getVideoWidth();  //Get the width of the video.
int videoHeight = ttVideoEngine.getVideoHeight(); // Get the height of the video.
```


<span id="c6dedc9b"></span>
## Screenshots


1. After initializing the player and before calling `play`, use `setIntOption` to enable Texture Render. Example code:

   ```java
   // Config prior to calling 'Play'
   ttvideoEngine.setIntOption(TTVideoEngine.PLAYER_OPTION_USE_TEXTURE_RENDER, 1);
   ```
   

2. After calling `play`, configure the screenshot callback notification via `snapshot`. Call the `onSnapShot method defined in the`SnapshotListener interface to fetch and process the video screenshot bitmap, screenshot width, and screenshot height using the callback function. Example code:

   ```java
   mVideoEngine.snapshot(new SnapshotListener() {
       @Override
       public void onSnapShot(final Bitmap bitmap, final int with, final int height) {
   
           }
      });
   ```
   


<span id="d16129ab"></span>
## Fetching playback information

The Android Player SDK supports fetching playback information such as current playback progress, playback duration, cache progress, and cache progress callback.

<span id="243a9011"></span>
### Current playback progress


* Call `getCurrentPlaybackTime` to fetch the current playback position. The example code is shown below.

   ```java
   int currentPostion = ttVideoEngine.getCurrentPlaybackTime(); // Get the current playback position, unit: ms.
   ```
   

* Use the `onCurrentPlaybackTimeUpdate` callback to fetch the time progress. The example code is shown below.

   ```java
   // Enable the callback by setting the progress callback interval, configured before calling play.
   ttVideoEngine.setIntOption(TTVideoEngine.PLAYER_OPTION_POSITION_UPDATE_INTERVAL, 200); 
   ttVideoEngine.setVideoEngineCallback(new VideoEngineCallback() {
       // ...Omit the implementation of the remaining methods.
       @Override
       public void onCurrentPlaybackTimeUpdate(TTVideoEngine engine, int currentPlaybackTime) {
           Log.v("VideoPlay", "onCurrentPlaybackTimeUpdate " + engine + " " + currentPlaybackTime);
       }
   });
   ```
   


<span id="79ffe84f"></span>
### Playback duration

Call `getDuration` to fetch the playback duration. The example code is shown below.

```java
int duration = ttVideoEngine.getDuration(); // Video duration retrieval, unit: MS.
```


<span id="620309b8"></span>
### Cache progress


* Call `getLoadedProgress` to fetch the cache progress. The example code is shown below.

   ```java
   int loadedProgress = ttVideoEngine.getLoadedProgress(); // Cache progress retrieval, range: 1-100.
   ```
   

* Use the `onBufferingUpdate` callback to fetch the cache progress. The example code is shown below.

   ```java
   ttVideoEngine.setListener(new VideoEngineListener() {
     // ...Omit the rest of the implementation methods.
     @Override
     public void onBufferingUpdate(TTVideoEngine engine, int percent) {
         Log.v("VideoPlay", "onBufferingUpdate " + engine + " " + percent);
         // Cache progress callback, which can be used to display secondary cache progress on the playback progress bar. Range: 1-100.
     }
   });
   ```
   


<span id="d437cd4f"></span>
## Loop

Call `setLooping` with a value of `true` to enable looping. The example code is shown below.

```java
ttVideoEngine.setLooping(true); // Enable loop playback.
boolean isLooping = ttVideoEngine.isLooping(); // Check if loop playback is enabled.
```


<span id="e66d6719"></span>
## Playback speed

Call `setPlaybackParams` to set the speed. The default value is 1, and the value range is (0, 3]. The example code is shown below.

```java
PlaybackParams params = new PlaybackParams();
params.setSpeed(1f); // The default is 1x speed, with a range of (0, 3].
ttVideoEngine.setPlaybackParams(params);
```


<span id="9ba1280d"></span>
## Volume configuration

The Android Player SDK supports volume configuration functions such as audio focus, volume adjustment, and mute.

<span id="43303cfd"></span>
### Mute

Call `setIsMute` with a value of `true` to mute. The example code is shown below.

```java
ttVideoEngine.setIsMute(true); // Mute
boolean isMute = ttVideoEngine.isMute(); // whether to unmute
```


<span id="1e1b8ef8"></span>
### Volume adjustment

Volume adjustment includes adjusting the system volume and adjusting the playback volume.


<Tabs>
<Tab zoneid="Hwdu9anWJX" title="Adjust system volume">
<TabTitle>Adjust system volume</TabTitle>

Call `setVolume` The method sets the system left and right channel volume. Example code is as follows:```java
{`float
```



</Tab>
<Tab zoneid="r96w6IKvpx" title="Adjust playback volume (does not affect system volume)">
<TabTitle>Adjust playback volume (does not affect system volume)</TabTitle>

call first `setIntOption` The method switches the volume adjustment mode from system volume to playback volume, then call. `setVolume` The method sets the playback volume. Example code is as follows:```java
{`ttVideoEngine.setIntOption(TTVideoEngine.PLAYER\_OPTION\_SET\_TRACK\_VOLUME,
```



</Tab>
</Tabs>


<span id="c02ed50a"></span>
### Audio focus

The Player SDK does not handle audio focus internally. The requester needs to listen to `AudioManager.OnAudioFocusChangeListener` to handle the fetching and release of audio focus. See the official document: [Manage audio focus](https://developer.android.com/guide/topics/media-apps/audio-focus).

<span id="b30c3e47"></span>
## Resolution configuration

When playing with a **VideoID video asset**, the server issues multiple resolution playback addresses. When the player receives the `onFetchedVideoInfo` callback, `supportedResolutionTypes` can be called to fetch the `Resolution []` array for all resolutions. You can use this array to display the resolution list and select the resolution logic.

<span id="2add0a0f"></span>
### Fetching the current resolution

Call `getCurrentResolution` to fetch the current resolution. The example code is shown below.

```java
// Get the current resolution
Resolution currentResolution = ttVideoEngine.getCurrentResolution();
```


<span id="ac279d8d"></span>
### Fetching the resolution list

```java
ttVideoEngine.setVideoInfoListener(new VideoInfoListener() {
    @Override
    public boolean onFetchedVideoInfo(VideoModel videoModel) {
       // Callback for successfully retrieving video data.
        Log.v("VideoPlay", "onFetchedVideoInfo " + videoModel);
        if (videoModel == null) return false;
        
        // Get the current VideoModel's resolution array, which can be used for displaying the resolution list.
        Resolution[] resolutions = ttVideoEngine.supportedResolutionTypes();
          
        return false;
    }
});
```


<span id="3870d533"></span>
### Switching the resolution


1. Set the start\-up resolution: If the preset resolution information is not displayed before playback, the configured start\-up resolution may not be in the supported resolution list. You can determine the final start\-up resolution by calling `findDefaultResolution`.

   ```java
   // The default resolution is 360p.
   Resolution defaultResolution = Resolution.Standard；
   // The VideoModel may not contain defaultResolution. Use findDefaultResolution to find the resolution closest to defaultResolution.
   Resolution resolution = TTVideoEngine.findDefaultResolution(videoModel, defaultResolution);
   // Set the selected initial playback resolution.
   ttVideoEngine.configResolution(resolution,
       new VideoEngineConfigResolutionListener() {
       
           // Resolution switch success callback
           void onFinished() {
              // Resolution switch successful, you can add logic handling after success here
           }
           
           // Resolution switch failure callback
           void onError(Error error) {
              // Resolution switch failed, error contains detailed error information
              // Refer to the error code meanings: 
              // Pay attention to the following resolution error codes: https://docs.byteplus.com/en/docs/byteplus-vod/docs-error-code
              // ConfigResolutionSameParameter = -110001; // The parameter passed in when switching resolution is the same as the current resolution
              // ConfigResolutionNoVideoModel = -110002;  // No available playback source data
           }   
       });
   ```
   

2. After playback starts, you need to specify which video resolutions are supported and switch to the specified resolution grade.

   ```java
   // Get the current available resolution list.
   Resolution[] resolutions = ttVideoEngine.supportedResolutionTypes();
   // Determine the resolution to switch to. The logic here is simplified, and the business should select the appropriate resolution based on its own logic.
   Resolution resolution = resolutions[0];
   // Set the selected initial playback resolution.
   ttVideoEngine.configResolution(resolution);
   ```
   


The resolution enumerations are shown in the table below.


|Enum |Video resolution |Audio quality |Video description |Audio description |
|---|---|---|---|---|
|Standard |360p |Medium |Standard definition |Normal sound quality |
|High |480p |Higher |High definition |High sound quality |
|SuperHigh |720p |Highest |Ultra\-high definition |Music sound quality |
|ExtremelyHigh |1080p |Original |1080p |Original resolution |
|TwoK |2k |N/A |2K |This grade does not affect audio |
|FourK |4k |N/A |4K |This grade does not affect audio |
|Auto |Automatic adjustment |N/A |DASH supports dynamic adjustment of the resolution according to the network speed |This grade does not affect audio |


<span id="c4951e31"></span>
## Enabling seamless switching

For frame\-aligned MP4 and HLS videos generated by the VOD service, seamless switching between multiple resolutions during playback is supported to enhance the user experience. The following example code demonstrates how to enable seamless switching in Vid mode:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">For information on encoding frame\-aligned videos and enabling seamless switching in DirectUrl mode, please <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00001112">submit a ticket</a> to our technical support team.</div>


```Java
// Seamless switching for HLS playback sources
ttVideoEngine.setIntOption(TTVideoEngine.PLAYER_OPTION_ENABLE_HLS_SEAMLESS_SWITCH, 1); 
ttVideoEngine.setIntOption(TTVideoEngine.PLAYER_OPTION_ENABLE_MASTER_M3U8_OPTIMIZE, 1);

// Seamless switching for MP4 playback sources
ttVideoEngine.setIntOption(PLAYER_OPTION_SEGMENT_FORMAT_FLAG, (1 << SEGMENT_FORMAT_FMP4) | (1 << SEGMENT_FORMAT_MP4));
ttVideoEngine.setIntOption(TTVideoEngine.PLAYER_OPTION_ENABLE_BASH, 1);

// Seamless switching completion callback
ttVideoEngine.setVideoEngineCallback(new VideoEngineCallback() {
    @Override
    public void onVideoStreamBitrateChanged(Resolution resolution, int bitrate) {
    }
});
```


<span id="e9860cc6"></span>
## Playing HLS videos

<span id="a9091ca1"></span>
### Configuring the HLS expiration time

The method for configuring the expiration time differs depending on the method used to play the HLS video.

<span id="5bcec406"></span>
#### DirectUrl mode

If you play HLS videos in DirectUrl mode, you can set the expiration time using the `urlExpiredTimes` parameter during playback asset configuration and preloading.

<span id="d1e2f8dd"></span>
##### Configuring the playback asset

When configuring the DirectUrl playback asset, pass in the expiration time when creating the `StrategySource`, and then call `setStrategySource` to play. The example code is shown below:

```java
StrategySource directUrlSource = new DirectUrlSource.Builder()
        .setVid(vid)
        .addItem(new DirectUrlSource.UrlItem.Builder()
                .setUrl(url)
                .setCacheKey(cacheKey)
                .setUrlExpires(new String[]{"xxx"}) // unit in seconds
                .build())
        .build();
mEngine.setStrategySource(directUrlSource); 
```


<span id="cd530dda"></span>
##### Preloading

When playback preloading is configured and you create a `DirectUrlSource`, pass in the expiration time using `setUrlExpires`, and then call `addTask` to preload according to the preloading process. The example code is shown below:

```java
DirectUrlSource directUrlSource = new DirectUrlSource.Builder()
    .setVid(vid)
    .addItem(new DirectUrlSource.UrlItem.Builder()
            .setUrl(url)
            .setCacheKey(cacheKey)
            .setUrlExpires(new String[]{"xxx"}) // unit in second
            .build())
    .build();
PreloaderURLItem preloaderUrlItem =
        mFactory.createUrlItem(directUrlSource, preloadSize);
preloaderUrlItem.setCallBackListener(new PreloadCallback(vid, this));
TTVideoEngine.addTask(preloaderUrlItem);
```


<span id="c363683b"></span>
##### Determining whether the expiration time has been set

You can check whether the playback address contains the `hlsproxyQuery` keyword by viewing the log in Debug mode. For example:

```Plain
hlsproxyQuery=expirteTime%03Dxxxxxxxxxx
```


<span id="2d028e42"></span>
#### Vid mode

If you play HLS videos in Vid mode, no additional settings need to be made on the client side. Just make sure that the `VideoModel` returned in the [GetPlayInfo](https://docs.byteplus.com/docs/byteplus-vod/reference-getplayinfo) interface contains expiration time information.

<span id="4e387004"></span>
### Playing HLS standard encrypted videos

<span id="3f291605"></span>
#### Server\-side configuration

Before implementing the client\-side playback logic, ensure you have completed the following server\-side configurations.


1. **Complete server\-side configuration:**  Complete all preparatory work, including setting up the decryption service and configuring encrypted transcoding. For more details, please refer to [HLS standard encryption](https://docs.byteplus.com/docs/byteplus-vod/docs-standard-encryption).

2. **Set the correct** \*\*`FileType`: \*\*Different from playing regular videos, your application server must set the `FileType` \*\*\*\* parameter to `standard_evideo` (encrypted video) or `standard_eaudio` (encrypted audio) when calling the `GetPlayInfo` interface to retrieve the playback URL or when issuing a `PlayAuthToken`.


<span id="4a52783e"></span>
#### Client\-side implementation

After you have completed the above server\-side configuration, you can refer to the following client implementation examples based on the playback method and whether the HLS encryption rewrite is enabled.


<Tabs>
<Tab zoneid="Bo5IM1wIKt" title="Vid mode">
<TabTitle>Vid mode</TabTitle>

In this scenario, the client\-side playback code is largely the same as for playing regular Vid videos. The SDK automatically handles the decryption process internally. If you have enabled the[ HLS encryption rewrite](https://docs.byteplus.com/en/docs/byteplus-vod/docs-standard-encryption#step-3-configuring-hls-encryption-rewrite-recommended) feature, you need to additionally set the `urlExtendParams` parameter to pass the authentication parameter `AppAuthToken`.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">If you enable the HLS encryption rewrite feature, you can pass the <code>AppAuthToken</code> via the <code>urlExtendParams</code> parameter throughout the entire lifecycle of playback, download, and preloading:</div>



* <div data-tips="true" data-tips-type="tip"><strong>Playback</strong>: Set in the <code>VidPlayAuthTokenSource.Builder</code> via the <code>setUrlExtendParams()</code> method.</div>


* <div data-tips="true" data-tips-type="tip"><strong>Download:</strong> Set on the <code>DownloadVidTask</code> object via the <code>setUrlExtendParams()</code> method.</div>


* <div data-tips="true" data-tips-type="tip"><strong>Preloading</strong>:</div>


   * <div data-tips="true" data-tips-type="tip"><strong>Custom preloading</strong>: Set on the <code>PreloaderVidItem</code> object via the <code>setUrlExtendParams()</code> method.</div>


   * <div data-tips="true" data-tips-type="tip"><strong>Preload strategy:</strong> Set the <code>urlExtendParams</code> property and pass the <code>VidPlayAuthTokenSource</code> instance to the preload strategy. The strategy reads and applies this property to the internal preload tasks.</div>



```Java
// 1. (Configure as needed) Prepare your authentication parameter Map
// If "HLS encryption rewrite" is enabled, create and populate this Map.
// Map<String, String> authParams = new HashMap<>();
// authParams.put("AppAuthToken", "<your_token>");

// 2. Construct the Vid playback source
VidPlayAuthTokenSource.Builder builder = new VidPlayAuthTokenSource.Builder()
        .setVid("your_hls_encrypted_vid")
        .setPlayAuthToken("your_play_auth_token");

// 3. (Configure as needed) Set the authentication parameters to the playback source
// Execute this step if "HLS encryption rewrite" is enabled.
// The SDK automatically converts the key-value pairs in the Map into URL query parameters and appends them to the M3U8 request.
// builder.setUrlExtendParams(authParams);

// 4. Build the playback source and play
StrategySource vidSource = builder.build();
ttVideoEngine.setStrategySource(vidSource);
ttVideoEngine.play();
```



</Tab>
<Tab zoneid="j1aQ1d4ENZ" title="DirectUrl mode">
<TabTitle>DirectUrl mode</TabTitle>

You can directly use `DirectUrlSource` to set the HLS standard encrypted video's M3U8 address. If you have enabled the [HLS encryption rewrite](https://docs.byteplus.com/en/docs/byteplus-vod/docs-standard-encryption#step-3-configuring-hls-encryption-rewrite-recommended) feature, you need to manually append the authentication parameters to the end of the URL and set the URL to the player.

```Java
// 1. Obtain the required playback information from your application server
final String vid = "your_unique_vid_for_hls"; // Provided by your server
final String cacheKey = "md5_of_original_url"; // Provided by your server - calculated based on the original URL

// If "HLS encryption rewrite" is enabled, your application server must append authentication parameters (such as AppAuthToken) and send a complete URL to the client.
// --- URL Example ---
// Original URL: https://www.example.com/encrypted_master.m3u8
// URL sent to the client after enabling "HLS encryption rewrite": https://www.example.com/encrypted_master.m3u8?AppAuthToken=<your_token>
final String finalUrlFromServer = "https://www.example.com/encrypted_master.m3u8?AppAuthToken=<your_token>";

// 2. Construct the DirectUrlSource
StrategySource directUrlSource = new DirectUrlSource.Builder()
        .setVid(vid)
        .addItem(new DirectUrlSource.UrlItem.Builder()
                .setUrl(finalUrlFromServer) // Use the complete URL sent by the server directly
                .setCacheKey(cacheKey)
                .build())
        .build();
        
// 3. Set the playback source and play
ttVideoEngine.setStrategySource(directUrlSource);
ttVideoEngine.play();
```



</Tab>
</Tabs>


<span id="25bfec1b"></span>
## Setting business tags

Business tags (tag) are used to distinguish between different types of audio and video within the same app (appid). They can be categorized according to business needs, based on video scenario and video duration—for example, immersive feed, short video, or long video. Call `setTag` to set the business tag. The example code is shown below.

```java
ttVideoEngine.setTag("tag"); // Set Tag
```


<span id="5660d314"></span>
## Setting business subtags

Business subtags (subtag) are used to further distinguish different audio and video types under the same business tag, such as encrypted video, unencrypted video, and audio. Call `setSubTag` to set the business subtag. The example code is shown below.

```java
ttVideoEngine.setSubTag("subtag"); //Set SubTag
```


<span id="configure-reporting-domain"></span>
## Configure the reporting domain

Player SDK 1.51.300 and later supports configuring the event reporting domain. If you do not configure the reporting domain, the SDK uses its built\-in default reporting domain.


* To use the SDK's built\-in dual\-stack reporting domain, call `setApplogDomainIpv6Enabled(true)`.

* To use a custom IPv4 or IPv6 reporting URL, call `setApplogDomain`. The URL must start with `http://` or `https://`.

* If both settings are configured, the custom reporting URL specified by `setApplogDomain` takes precedence.


The following sample code shows how to configure the reporting domain:

```java
private void initTTSDK(Context context) {
    // 1. Build the Config object.
    Config.Builder configBuilder = new Config.Builder();
    configBuilder.setApplicationContext(context.getApplicationContext());
    // ... Other required configurations, such as AppID, AppName, and License.

    // 2. Configure the event reporting domain. If you do not configure it, the SDK uses its built-in default reporting domain.
    //    - To use the built-in dual-stack reporting domain, enable setApplogDomainIpv6Enabled(true).
    //    - To use a custom IPv4 or IPv6 reporting URL, specify it through setApplogDomain. The URL must start with http:// or https://.
    //    - If both settings are configured, setApplogDomain takes precedence.
    configBuilder.setApplogDomainIpv6Enabled(true);
    configBuilder.setApplogDomain("https://custom-report-url.com");

    // 3. Start the SDK.
    Env.start(configBuilder.build());
}
```


<span id="7660e9cd"></span>
## Keeping the screen on

Call `View#setKeepScreenOn(boolean)` to set the screen to remain illuminated as normal, and `View#getKeepScreenOn` to fetch whether it remains illuminated as normal. The example code is shown below.

```java
textureView.setKeepScreenOn(true); // Keep the screen awake.
boolean isKeepScreenOn = textureView.getKeepScreenOn(); // Whether to keep the screen awake.
```


<span id="9c303658"></span>
## Listening for the playback status

Example code for listening for the playback status is shown below.

```Java
ttVideoEngine.setVideoEngineCallback(new VideoEngineCallback() {
    @Override
    public void onPlaybackStateChanged(TTVideoEngine engine, int playbackState) {
        Log.v("VideoPlay", "onPlaybackStateChanged " + engine + " " + playbackState);
        // Callback for playback state changes.
        switch (playbackState) {
            case TTVideoEngine.PLAYBACK_STATE_PLAYING:
                // Playback has started.
                break;
            case TTVideoEngine.PLAYBACK_STATE_ERROR:
                // An error occurred during playback.
                // Note:
                // 1. This state does not necessarily mean playback has failed. The player might recover after internal retries.
                // 2. If playback ultimately fails, the onError() callback will be triggered.
                break;
            case TTVideoEngine.PLAYBACK_STATE_STOPPED:
                // Playback has stopped.
                break;
            case TTVideoEngine.PLAYBACK_STATE_PAUSED:
                // Playback is paused.
                break;
            default:
                break;
        }
    }

    @Override
    public void onLoadStateChanged(TTVideoEngine engine, int loadState) {
        Log.v("VideoPlay", "onLoadStateChanged " + engine + " " + loadState);
        switch (loadState) {
            case TTVideoEngine.LOAD_STATE_PLAYABLE:
                // Buffering has ended, or rendering has started.
                break;
            case TTVideoEngine.LOAD_STATE_STALLED:
                // Buffering has started.
                break;
            case TTVideoEngine.LOAD_STATE_ERROR:
                // A loading error occurred.
                break;
            default:
                break;
        }
    }

    @Override
    public void onVideoSizeChanged(TTVideoEngine engine, int width, int height) {
        Log.v("VideoPlay", "onVideoSizeChanged " + engine + " " + width + " " + height);
        // Called when the player has parsed the video's width and height.
        // For videos with a pixel aspect ratio other than 1:1, width/height does not represent the final display aspect ratio.
        // The final display aspect ratio should be calculated using the 'num' and 'den' values from the onSARChanged callback.
        // displayAspectRatio = (num/(float)den) * (width/(float)height)
    }

    @Override
    public void onBufferingUpdate(TTVideoEngine engine, int percent) {
        Log.v("VideoPlay", "onBufferingUpdate " + engine + " " + percent);
        // Callback for buffering progress. Can be used to display a secondary progress bar (buffer indicator) on the seek bar.
    }

    @Override
    public void onPrepare(TTVideoEngine engine) {
        Log.v("VideoPlay", "onPrepare " + engine);
        // Called immediately when prepare() is invoked.
    }

    @Override
    public void onPrepared(TTVideoEngine engine) {
        Log.v("VideoPlay", "onPrepared " + engine + " isSystem " + engine.isSystemPlayer());
        // Called when preparation is complete.
    }

    @Override
    public void onRenderStart(TTVideoEngine engine) {
        Log.v("VideoPlay", "onRenderStart " + engine);
        // Called when the first frame is rendered. At this point, the video is visible to the user.
    }

    @Override
    public void onStreamChanged(TTVideoEngine engine, int type) {
        Log.v("VideoPlay", "onStreamChanged " + engine + " " + type);
        // Notification of a change in the audio or video stream.
        // type: TTVideoEngine.VIDEO_STREAM or TTVideoEngine.AUDIO_STREAM
    }

    @Override
    public void onCompletion(TTVideoEngine engine) {
        Log.v("VideoPlay", "onCompletion " + engine);
        // Called when playback is complete.
    }

    @Override
    public void onError(Error error) {
        Log.v("VideoPlay", "onError " + error);
        // Called when a fatal playback error occurs.
        // For error code documentation, see: https://docs.byteplus.com/en/docs/byteplus-vod/docs-error-code
        // After this callback is triggered, the player is automatically released internally.
    }

    /**
     * Called when buffering (stalling) starts.
     *
     * @param code The type of buffering:
     * {@link VideoBufferDetailListener#BUFFERING_TYPE_NET} Network-related buffering.
     * {@link VideoBufferDetailListener##BUFFERING_TYPE_DECODER} Decoder-related buffering.
     *
     * @param afterFirstFrame The timing of the buffering event:
     * {@link VideoBufferDetailListener#BEFORE_FIRST_FRAME} Buffering before the first frame.
     * {@link VideoBufferDetailListener#AFTER_FIRST_FRAME} Buffering after the first frame.
     *
     * @param action The action that caused the buffering:
     * {@link VideoBufferDetailListener#BUFFER_START_ACTION_NONE} Buffering during normal playback.
     * {@link VideoBufferDetailListener#BUFFER_START_ACTION_SEEK} Seeking.
     * {@link VideoBufferDetailListener#BUFFER_START_ACTION_CHANG_RESOLUTION} Changing resolution.
     */
    @Override
    public void onBufferStart(int code, int afterFirstFrame, int action) {
        Log.v("VideoPlay", "onBufferStart " + code + ", " + afterFirstFrame + ", " + action);
        // Buffering started, show a loading indicator.
    }

    /**
     * Callback for video buffering progress percentage.
     * @param percent The buffering progress percentage (0-99).
     */
    public void onBufferPercentUpdate(int percent) {
        // Update the loading progress UI with the 'percent' value.
    }
    
    /**
     * Called when buffering (stalling) ends.
     * @param code The type of buffering:
     * {@link VideoBufferDetailListener#BUFFERING_TYPE_NET} Network-related buffering.
     * {@link VideoBufferDetailListener##BUFFERING_TYPE_DECODER} Decoder-related buffering.
     */
    @Override
    public void onBufferEnd(int code) {
        Log.v("VideoPlay", "onBufferEnd " + code);
        // Buffering ended, hide the loading indicator.
    }

    @Override
    public void onSARChanged(int num, int den) {
        Log.v("VideoPlay", "onSARChanged " + num + ", " + den);
        // Callback for changes in the video's Sample Aspect Ratio (SAR), used to control the display mode.
        float sampleAspectRatio = num / (float) den;
    }
});
```


<span id="af396b3b"></span>
## Displaying the current download speed

The Player SDK supports callback of the video data volume fetched by the current video within a period of time. This can be used to display the current video download speed during video playback, seeking, or stuttering. The implementation steps and example code are shown below.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="warning">This feature is only supported by the Premium and Enterprise editions. Make sure you have purchased a Premium or Enterprise license. For details, see <a href="https://docs.byteplus.com/en/docs/byteplus-vod/docs-license-management">Licenses</a>.</div>



1. Before initializing the SDK, enable global real\-time download speed listening.

   ```java
   // Enable global real-time download speed monitoring, call before initializing the SDK. 
   TTVideoEngine.setIntValue(DATALOADER_KEY_INT_NEED_SPEED_TEST_BY_TIMEINTERNAL, 1);
   
   // Initialize SDK
   Env.start(...)；
   ```
   

2. Set the single instance speed time interval.

   ```java
   // The value is the speed test interval, in MS. The recommended value is 500 MS.
   // Timing of the call: Call after setting the playback source.
   ttVideoEngine.setCustomHeader("X-SpeedTest-TimeInternal", value);
   ```
   

3. Set callback listening.

   ```java
   // Set callback listener.
   TTVideoEngine.setDataLoaderListener(new DataLoaderListener());
   
   interface DataLoaderListener {
       ...
       /**
        * 
        * @param what == DATALOADER_KEY_NOTIFY_SPEEDINFO Used for network speed callback.
        * At this point, code is netReadLen (in bytes), and parameter is netReadTime (in milliseconds).
        */
       public void  onNotify(int  what, long  code, long  parameter, String info) {
           if  (what == DataLoaderHelper.DATALOADER_KEY_NOTIFY_SPEEDINFO) {
               float  dataSize = code / 1024;
               float  time = parameter / 1000;
               float  speed = dataSize / time; // Unit in KB/s
               Log.d(TAG, "download speed = "  + speed);
           }
       }
   }
   ```
   


<span id="disabling-playback-cache-for-the-current-player-instance"></span>
## Disabling playback cache for the current player instance

By default, the player caches video data during playback to speed up subsequent playback. If you do not want specific videos to be written to the local playback cache, disable the data loader module for the current player instance before setting the playback source:

```java
ttVideoEngine.setIntOption(
        TTVideoEngineInterface.PLAYER_OPTION_ENABLE_DATALOADER,
        0);
```


After this option is set, playback data generated by the current player instance is not written to the local cache.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>



* <div data-tips="true" data-tips-type="warning">This setting applies only to the current player instance. Disabling playback cache globally is not supported.</div>


* <div data-tips="true" data-tips-type="warning">This setting does not affect offline download tasks. Downloaded videos are still written to local storage.</div>


* <div data-tips="true" data-tips-type="warning">Preloading and prerendering tasks are independent of player instances. If you have configured these tasks, exclude videos that must not be cached from the preloading or prerendering list. If you have not configured these tasks, no action is required.</div>



<span id="e806f41d"></span>
## Clearing the video cache

Call [clearAllCaches](https://docs.byteplus.com/docs/byteplus-vod/docs-android-player-sdk-api-details#TTVideoEngine-clearallcaches) to clear the video cache:

```Java
TTVideoEngine.clearAllCaches(true); // True to clear all caches; false to use LRU and retain the most recent 10 cache entries.
```


<span id="d681070f"></span>
## Seeking to the last frame

During playback, if the user drags the progress bar to fast\-forward the video to a position within 3 seconds of the total duration of the video, the player will directly call back to indicate that playback is complete. If you need to support seeking to the last frame, you can configure it as follows:

```Java
mVideoEngine.setIntOption(TTVideoEngine.PLAYER_OPTION_ENABLE_SEEK_LASTFRAME,1);
mVideoEngine.setIntOption(TTVideoEngine.PLAYER_OPTION_ENABLE_SEEK_END,1);
```


<span id="df2b09a0"></span>
## Setting the primary and backup domain names

The SDK supports setting URLs for multiple domain names in DirectUrl mode to achieve primary and backup disaster recovery.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="warning">Versions 1.35.1 or above support this function.</div>



1. Before initialization, enable `DATALOADER_KEY_INT_ALLOW_TRY_THE_LAST_URL`.

   ```Java
   TTVideoEngine.setIntValue(DataLoaderHelper.DATALOADER_KEY_INT_ALLOW_TRY_THE_LAST_URL, 1);
   Env.start(/* Omit */);
   ```
   

2. Configure the playback asset:

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The files referenced by the primary and backup addresses must be the same.   </div>
   

   ```Java
   final String vid = "video id"; // The video source and vid must correspond one-to-one.
   final String mainUrl = "http://www.example.com/h264.mp4"; // Main URL
   final String backUpUrl = "http://www.examplebackup.com/h264.mp4"; // Backup URL
   // It is recommended to use the MD5 of a consistent and non-variable part of the URL for the cacheKey, such as the MD5 of the path section.
   final String cacheKey = TTVideoEngine.computeMD5(mainUrl); 
   
   StrategySource directUrlSource = new DirectUrlSource.Builder()
           .setVid(vid)
           .addItem(new DirectUrlSource.UrlItem.Builder()
                   .setUrls(new String[]{mainUrl, backUpUrl})
                   .setCacheKey(cacheKey)
                   .build())
           .build();
   ```
   


<span id="9779c336"></span>
## Setting the maximum number of retries for playback failure

When a playback error occurs, the player attempts to restart playback until it reaches the maximum number of retries. If all retries fail, the `onError` callback is eventually triggered. Starting from version 1.50.200.3, you can call the `setIntOption` method and set a value for `PLAYER_OPTION_MAX_ERROR_COUNT` to configure the maximum number of retries after a playback failure. If you do not configure this setting, the player retries a maximum of 3 times by default.

```Java
// Set the maximum number of retries after a playback failure as 3
ttVideoEngine.setIntOption(TTVideoEngine.PLAYER_OPTION_MAX_ERROR_COUNT, 3);
```


<span id="1d472b50"></span>
## Fetching the device ID

The Player SDK automatically generates a unique device ID by default. You can track the playback records of the device ID on the [Endpoint tracker](https://docs.byteplus.com/docs/byteplus-vod/docs-end-point-tracker). Refer to the following code to fetch the device ID:

```Java
// Get device ID
TTVideoEngine.getDeviceID()
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">If you have your own user system and want to track the play behavior of individual users using the user ID, you can <a href="https://docs.byteplus.com/docs/byteplus-vod/docs-customizing-device-id-android">Android Player SDK: Customizing device ID</a></div>


<span id="116d5715"></span>
## **Setting network timeout** duration

Refer to the following code snippet to set the network timeout duration for the SDK. It is recommended to set it to 10 seconds.

```Java
// 1. Enable network timeout detection
// Set ALGO_OPTION_USE_ENGINE_NETWORK_TIMEOUT to 1
TTVideoEngine.setIntValue(TTVideoEngine.ALGO_OPTION_USE_ENGINE_NETWORK_TIMEOUT, 1);

TTVideoEngine ttVideoEngine = new TTVideoEngine(context, TTVideoEngine.PLAYER_TYPE_OWN);
// 2. Set network timeout duration (in seconds) for the engine instance
// This example sets it to 10 seconds
ttVideoEngine.setIntOption(PLAYER_NETWORK_TIMEOUT, 10);
// 3. Disable connection error retry. When connection fails, no retry will be attempted
ttVideoEngine.setIntOption(PLAYER_OPTION_SET_ORIGINAL_RETRY, 0);
// 4. Disable engine playback failure retry. When playback fails, no retry will be attempted
ttVideoEngine.setIntOption(PLAYER_OPTION_SET_MAX_ACCUMULATED_COUNT, 0);
```
