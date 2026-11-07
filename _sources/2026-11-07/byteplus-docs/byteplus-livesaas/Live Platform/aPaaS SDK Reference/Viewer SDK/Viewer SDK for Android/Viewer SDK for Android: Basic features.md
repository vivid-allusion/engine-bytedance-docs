---
title: "Viewer SDK for Android: Basic features"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-android-basic-features"
---

This topic describes how to integrate the basic features of the Viewer SDK for Android, including how to integrate a full\-featured live room, a custom player, and a default player.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Currently, viewers can only join one live room at a time.</div>


<span id="9e3ed5fc"></span>
## Prerequisites

Complete the first 5 steps in [Integrating the Viewer SDK for Android](https://docs.byteplus.com/docs/byteplus-livesaas/docs-integrating-the-viewer-sdk-for-android).

<span id="4d05724b"></span>
## Features

This topic describes how to integrate the following features.


* [Full-featured live room](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-basic-features#d27888d9)

* [Custom player](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-basic-features#380007d1)

* [Default player](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-basic-features#4b8efe3c)


<span id="d27888d9"></span>
## Full\-featured live room

A full\-featured live room includes all the functional modules of a BytePlus Live live room, making it easier and more convenient to integrate than modules. Unless you have special requirements, we recommend that you integrate a full\-featured live room.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b5e29c4a28954ea2a00c0139bf42ff86~tplv-goo7wpa0wc-image.image) </span>

For more information on the features supported by a full\-featured live room, see [Feature comparison between SaaS and aPaaS](https://docs.byteplus.com/docs/byteplus-livesaas/docs-feature-comparison-between-saas-and-apaas).

<span id="3e176d1e"></span>
### Joining the live room

Call the [joinLiveRoom](https://docs.byteplus.com/docs/byteplus-livesaas/docs-tvuliveroom#b20db0d1) method to allow viewers to join the full\-featured live room and display the full\-featured live room page in the app.

The sample code is as follows.

```Java
long activityId = ACTIVITY_ID; // Replace ACTIVITY_ID with the activity ID of the live room.
String token = "TOKEN"; // Replace TOKEN with the authorization token required to join the live room. 
TVULiveRoom.TVURoomAuthMode roomAuthMode = TVULiveRoom.TVURoomAuthMode.PUBLIC; // The authentication mode of the live room. Here take the public mode as an example. Viewers can perform operations such as watching the live stream and viewing comments without logging in to the live room.
boolean isPortrait = true;// Whether the live room is in portrait mode. Here take the portrait mode as an example.
// Join the live room.
TVULiveRoom.joinLiveRoom(context, new JoinRoomConfig(activityId,token,roomAuthMode,isPortrait));
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Call <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-createactivityapiv2">CreateActivityAPIV2</a> or <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi">ListActivityAPI</a> to get the activity ID of the live room.</div>


* <div data-tips="true" data-tips-type="tip">Call <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi">GetSDKTokenAPI</a> and set the value of <code>Mode</code> to <code>1</code> to get the authorization token in public mode. To change the authentication mode to custom, see <a href="https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-advanced-features#e54b3982">Custom login</a>.</div>



<span id="6ca81fd6"></span>
### Customizing the live room

Before joining the live room, you can call the `CustomSettings.Holder.mSettings.set` method to customize the following display effects of the live room.


* Font: Use TypeFace to set the font.

* Font size: Use an integer value to set the font size. Unit: sp.

* Image: Use a Drawable object to set an image. Images in PNG and JPG format are supported.

* Color: Use an integer value to set the color. For example, white is `0xFFFFFFFF`. Following the RGB color model, ARGB representation is used.

* Other.


Use the following sample code to customize the icon to close the live room as the image named `tvu_nav_icon_back_melon`.

```Java
CustomSettings settings = CustomSettings.Holder.mSettings;
settings.setExitRoomIcon(ContextCompat.getDrawable(this, R.drawable.tvu_nav_icon_back_melon));
```


For more information on how to customize the live room, see methods of the [mSettings](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings) class.

<span id="2f10c4ae"></span>
### Leaving the live room

When you need viewers to leave the live room, for example, when viewers do not have permission to watch the videos, you can call the [leaveLiveRoom](https://docs.byteplus.com/docs/byteplus-livesaas/docs-tvuliveroom#9fab7a9d) method. To allow viewers to rejoin the live room, you can call the [joinLiveRoom](https://docs.byteplus.com/docs/byteplus-livesaas/docs-tvuliveroom#b20db0d1) method again.

The sample code is as follows.

```Java
TVULiveRoom.leaveLiveRoom(context);
```


<span id="2729cb86"></span>
### Destroying the floating window

The floating window, namely the picture\-in\-picture (PiP) window.

If the floating window permission is enabled, a floating window is displayed when viewers exit the live room page. You can destroy the floating window if you do not need to display it. Destroying the floating window also destroys the corresponding player in the floating window.

The sample code is as follows.

```Java
TVULiveRoom.destroyFloatWindow();
```


<span id="8e3c6e92"></span>
### Complete sample code

The following sample code takes a live room in portrait mode as an example, with the activity ID (`activityId`) as `1721010849258****`, the `token` as `pg****`, and the authentication mode (`roomAuthMode`) as public. You can modify the parameter values as needed.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Call <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-createactivityapiv2">CreateActivityAPIV2</a> or <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi">ListActivityAPI</a> to get the activity ID of the live room.</div>


* <div data-tips="true" data-tips-type="tip">Call <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi">GetSDKTokenAPI</a> and set the value of <code>Mode</code> to <code>1</code> to get the authorization token in public mode. To change the authentication mode to custom, see <a href="https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-advanced-features#e54b3982">Custom login</a>.</div>



```Java
long activityId = 1721010849258****;
String token = "pg****";
TVULiveRoom.TVURoomAuthMode roomAuthMode = TVULiveRoom.TVURoomAuthMode.PUBLIC;
boolean isPortrait = true;
// (Optional) Customize the live room. Here, customize the icon to close the live room as an example.
CustomSettings settings = CustomSettings.Holder.mSettings;
settings.setExitRoomIcon(ContextCompat.getDrawable(this, R.drawable.tvu_nav_icon_back_melon));
// Join the live room.
TVULiveRoom.joinLiveRoom(context, new JoinRoomConfig(activityId,token,roomAuthMode,isPortrait));
// Leave the live room.
TVULiveRoom.leaveLiveRoom(context);
```


<span id="380007d1"></span>
## Custom player

A custom player does not include the control interface, which means it does not have interactive buttons such as the play button.

The custom player instance `TVUSinglePlayerView` contains two elements: `TextureView` and the video cover image. The instance also exposes several APIs for calling and events for listening, making it easy to embed the custom player into your own page and implement the following features:


* Add a custom control interface to the custom player on your own page.

* Display multiple custom players on your own page, each corresponding to a different live room. When viewers tap a custom player displayed on the page, they can join the corresponding full\-featured live room.

   When viewers tap a custom player on your own page, you must use the code provided in [Joining the live room](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-basic-features#3e176d1e) of the full\-featured live room section.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bd187e4c9e4f406fb192f3ffc6e98ae4~tplv-goo7wpa0wc-image.image) </span>

* Implement the floating window on your own and display the content playing in the custom player on the floating window view. This allows you to first display the floating window, then the full\-featured live room. For example, viewers enter your product detail page first to view the product, and then tap the floating window to join the full\-featured live room.

   You must add the `videoView` in the sample code of [Joining the live room](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-basic-features#fe765d44) to the floating window view, and use the sample code of [Joining the live room](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-basic-features#3e176d1e) in the full\-featured live room section when viewers tap the floating window view.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/42b00e893d0d4c5d9bd233fe960a9c2a~tplv-goo7wpa0wc-image.image) </span>


<span id="fe765d44"></span>
### Joining the live room

Use the following sample code to join the live room and create a custom player.

```Java
// Create the TVULiveRoomServer instance before calling the Activity.setContentView method. Here, only the custom player is integrated as an example. To bind live room components, such as chat interaction menu and popularity, to the custom player, replace SERVER_TYPE_SINGLE with SERVER_TYPE_LIVEROOM.
TVULiveRoomServer roomServer = new TVULiveRoomServer(this, activityId, token, TVULiveRoomServer.SERVER_TYPE_SINGLE);
// Set the authentication mode of the live room to public, allowing viewers to perform operations such as watching the live stream and viewing comments without logging in.
roomServer.setRoomAuthMode(TVULiveRoom.TVURoomAuthMode.PUBLIC);
// Initialize the TVUSinglePlayerView instance.  
InitConfig initConfig = new InitConfig();
TVUSinglePlayerView videoView = findViewById(R.id.video_view);
videoView.init(initConfig);
// Bind the TVUSinglePlayerView instance to the TVULiveRoomServer instance.
roomServer.setPlayerView(videoView.getInnerPlayerView());
// Start the TVULiveRoomServer instance. The player automatically plays the video after the instance is started.
roomServer.start();   
```


<span id="53bf8dc4"></span>
### Setting tap behaviors of buttons in a custom control interface

After adding a custom control interface to a custom player, you can set the tap behaviors of buttons.

The following sample code sets the tap behaviors of the play button and the pause button.

```Java
// Find the videoView using the findViewById method.
TVUSinglePlayerView videoView = findViewById(R.id.video_view);
// Find the play button using the findViewById method.
Button btnPlay = findViewById(R.id.btn_play);
// Find the pause button using the findViewById method.
Button btnPause = findViewById(R.id.btn_pause);
// Set the tap behavior of the play button: play the video when the play button is tapped.
btnPlay.setOnClickListener(v -> {
    videoView.play();
});
// Set the tap behavior of the pause button: pause the video when the pause button is tapped.
btnPause.setOnClickListener(v -> {
    videoView.pause();
});
```


<span id="5c92bfa9"></span>
### Implementing custom player control

After the `TVULiveRoomServer` instance is started, you can call related methods to implement custom player control. For more information, see [TVUSinglePlayerView](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview).

The following sample code demonstrates how to implement video pause and play in a custom player.

```Java
// Find the videoView using the findViewById method.
TVUSinglePlayerView videoView = findViewById(R.id.video_view);
videoView.pause();   // Pause the video.
videoView.play();    // Play the video.
```


<span id="6e0a8cd3"></span>
### Listening to custom player events

You can listen to custom player events. For more information, see [SinglePlayerListener](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#e6e91c48).

The sample code is as follows.

```Java
// Set the listener for custom player events.
initConfig.singlePlayerListener = new SinglePlayerListener() {
    /**
     * Callback triggered when the live room status changes.
     * @param status The current live room status.
     *               1: Live.
     *               2: Preview.
     *               3: Playback.
     *               4: Over.
     */
    @Override
    public void liveRoomStatusChanged(int status) {
    }

    /**
     * Callback triggered when the playable status of resources changes.
     * @param playableStatus The current playable status of resources.
     *                       0: No resources are playable, so you cannot call the play method.
     *                       1: Video On Demand (VOD) videos (previews and playbacks) are playable. You can call the play method to play the videos.
     *                       2: A live stream is playable. You can call the play method to play the video.
     */
    @Override
    public void playableStatusChanged(int playableStatus) {
    }

    /**
     * Callback triggered when the play status changes.
     * @param playStatus The current play status.
     *                   0: Paused.
     *                   1: Playing.
     */
    @Override
    public void playStatusChanged(int playStatus) {

    }

    /**
     * Callback triggered when the video size changes.
     * @param width Video width.
     * @param height Video height.
     */
    @Override
    public void sizeChanged(int width, int height) {
    }

    /**
     * Callback triggered when the stuttering status changes. You can configure whether to display the custom loading animation.
     * @param isStalling Whether the video is stuttering.
     *                   true: Stuttering.
     *                   false: Not stuttering.
     */
    @Override
    public void stallingStatusChanged(boolean isStalling) {
    }

    /**
     * Callback for VOD errors.
     * @param error Error details.
     */
    @Override
    public void vodErrorOccurred(Error error) {
    }

    /**
     * Callback for live errors.
     * @param error Error details.
     */
    @Override
    public void liveErrorOccurred(LiveError error) {
    }

    /**
     * Callback for play errors, including VOD and live errors. During this time, the video is paused. You can configure a retry screen to guide viewers to tap retry.
     * @param isPlayError Whether a play error occurs.
     *                    true: A play error occurs.
     *                    false: No play error occurs.
     */
    @Override
    public void playErrorStatusChanged(boolean isPlayError) {
    }

    /**
     *  Callback triggered when the VOD video is ready. You can call the seekVodTime method.
     */
    @Override
    public void vodPrepared() {
    }

    /**
     * Callback triggered when the VOD video rendering starts.
     */
    @Override
    public void vodRenderStarted() {
    }

    /**
     * Callback triggered when a VOD video automatically resumes playing from the point where it stopped.
     * @param seekTimeInMills The position to which the video seeks after automatically resuming from where it stopped. Unit: ms.
     */
    @Override
    public void vodAutoSeekPreviousTime(int seekTimeInMills) {
    }


    /**
     * Callback triggered when the playback progress of the VOD video changes. The playback progress is updated every second.
     * @param curTimeInMills The current playback progress. Unit: ms.
     */
    @Override
    public void vodCurPlayTimeChanged(int curTimeInMills) {
    }

    /**
     * Callback triggered when the total duration of the VOD video changes. This callback is usually triggered when the video switches.
     * @param durationInMills The total duration of the video. Unit: ms.
     */
    @Override
    public void vodDurationChanged(int durationInMills) {
    }

    /**
     * Callback triggered when the VOD video finishes playing.
     */
    @Override
    public void vodCompletion() {
    }

    /**
     * Callback triggered when the live stream is ready.
     */
    @Override
    public void livePrepared() {
    }

    /**
     * Callback triggered when the live stream rendering starts.
     * @param isFirstFrame Whether this is the first frame actually being rendered. This callback may be triggered multiple times due to retries during the live stream.
     *                     true: This is the first frame after calling the play method.
     *                     false: This is not the first frame after calling the play method.
     */
    @Override
    public void liveFirstFrameRendered(boolean isFirstFrame) {
    }

    /**
     * Callback triggered when the live stream ends.
     */
    @Override
    public void liveCompletion() {
    }

    /**
     * Callback triggered when the visibility status of the cover changes. The cover is not visible when the video is playing, and is visible when no video is playing.
     * @param isVisible Whether the cover is visible.
     *                  true: Visible.
     *                  false: Not visible.
     */
    @Override
    public void coverImageVisibleChanged(boolean isVisible) {
    }

    /**
     * Callback triggered when video resolution information changes. This callback is usually triggered when the video switches.
     * @param resolutions List of currently supported resolutions.
     * @param defaultResolution The resolution selected by default.
     */
    @Override
    public void resolutionInfoChanged(String[] resolutions, String defaultResolution) {
    }

    /**
     * Callback for the video ID (Vid) change of the playing VOD video, triggered when the VOD video playing on the viewing page changes or when the live room status changes.
     * @param vid The Vid of the playing VOD video. If no VOD video is playing, an empty string is returned.
     */
    @Override
    public void onCurVodVidChanged(String vid) {
    }

    /**
     * Callback for the playback list change in the live room, triggered when playbacks are released or withdrawn or when the live room status changes.
     * @param replayList The playback list of the live room. If the live room has no playbacks, an empty array is returned.
     */
    @Override
    public void onCurReplayListChanged(List<Replay> replayList) {
    }

    /**
     *  Callback triggered when the live source ID changes.
     * @param lineId The ID of the current live source. If the live room is not in the Live status, 0 is returned.
     */
    @Override
    public void onCurLiveLineIdChanged(long lineId) {
    }

    /**
     * Callback triggered when the live source list changes.
     * @param liveLineList The list of live sources. If the live room is not in the Live status, an empty array is returned.
     */
    @Override
    public void onCurLiveLineListChanged(List<PullStreamUrl> liveLineList) {
    }
};
```


<span id="d9382c20"></span>
### Leaving the live room

In scenarios such as destroying your own page, you can use the following sample code to leave the live room and destroy the custom player.

```Java
roomServer.closeRoom();
```


<span id="d34628bd"></span>
### Complete sample code

The following sample code takes a live room in portrait mode as an example, with the activity ID (`activityId`) as `1721010849258****`, the `token` as `pg****`, and the authentication mode (`roomAuthMode`) as public. You can modify the parameter values as needed.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Call <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-createactivityapiv2">CreateActivityAPIV2</a> or <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi">ListActivityAPI</a> to get the activity ID of the live room.</div>


* <div data-tips="true" data-tips-type="tip">Call <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi">GetSDKTokenAPI</a> and set the value of <code>Mode</code> to <code>1</code> to get the authorization token in public mode.</div>



```Java
long activityId = 1721010849258****;
String token = "pg****";
TVULiveRoomServer roomServer = new TVULiveRoomServer(this, activityId, token, TVULiveRoomServer.SERVER_TYPE_SINGLE);
roomServer.setRoomAuthMode(TVULiveRoom.TVURoomAuthMode.PUBLIC);
InitConfig initConfig = new InitConfig();
TVUSinglePlayerView videoView = findViewById(R.id.video_view);
videoView.init(initConfig);
// Bind the TVUSinglePlayerView instance to the TVULiveRoomServer instance.
roomServer.setPlayerView(videoView.getInnerPlayerView());
// Start the TVULiveRoomServer instance.
roomServer.start();
// Set tap behaviors for your custom play and pause buttons.
Button btnPlay = findViewById(R.id.btn_play);
Button btnPause = findViewById(R.id.btn_pause);
btnPlay.setOnClickListener(v -> {
    videoView.play();
});
btnPause.setOnClickListener(v -> {
    videoView.pause();
});
// Leave the live room and destroy the custom player.
roomServer.closeRoom();
```


<span id="4b8efe3c"></span>
## Default player

If you have your own viewing page and do not need to customize the player control interface, you can choose to integrate only the default player.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d7030048aa90402fb42d3a870f35d327~tplv-goo7wpa0wc-image.image) </span>

<span id="ae62b077"></span>
### Joining the live room

Use the following sample code to join the live room and create a default player.

```Java
// Create the TVULiveRoomServer instance for a live room in portrait mode. To create the TVULiveRoomServer instance for a live room in landscape mode, replace TVULiveRoomServer.SERVER_TYPE_PORTRAIT_LIVEROOM with TVULiveRoomServer.SERVER_TYPE_LIVEROOM.
TVULiveRoomServer mServer = new TVULiveRoomServer(this, activityId, token, TVULiveRoomServer.SERVER_TYPE_PORTRAIT_LIVEROOM);
// Introduce the PlayerView instance of the player module.
PlayerView playerView = (PlayerView) LayoutInflater.from(this).inflate(com.bytedance.live.sdk.R.layout.tvu_player_layout, null, false);
// Set the authentication mode of the live room to public, allowing viewers to perform operations such as watching the live stream and viewing comments without logging in.
mServer.setRoomAuthMode(TVULiveRoom.TVURoomAuthMode.PUBLIC);
// Bind the PlayerView instance to the TVULiveRoomServer instance.
mServer.setPlayerView(playerView);
// Introduce your player container.
FrameLayout playerViewContainer = findViewById(R.id.player_view_container);
// Place the PlayerView instance into the container.
playerViewContainer.addView(playerView, new FrameLayout.LayoutParams(ViewGroup.LayoutParams.MATCH_PARENT, ViewGroup.LayoutParams.MATCH_PARENT));
//  Start the TVULiveRoomServer instance. The player automatically plays the video after the instance is started.
mServer.start();
```


<span id="57cc739a"></span>
### Implementing default player control

After the `TVULiveRoomServer` instance is started, you can call related methods to implement default player control. For more information, see [PlayerView](https://docs.byteplus.com/docs/byteplus-livesaas/playerview).

The following sample code demonstrates how to implement video pause and play in a default player.

```Java
// Introduce the PlayerView instance of the player module.
PlayerView playerView = (PlayerView) LayoutInflater.from(this).inflate(com.bytedance.live.sdk.R.layout.tvu_player_layout, null, false);
playerView.pause(); // Pause the video.
playerView.play();  // Play the video.
```


<span id="786492a5"></span>
### Listening to default player events

You can listen to default player events. For more information, see [ITVULiveRoomServerListener](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#1b64c86a).

The sample code is as follows.

```Java
// Set the listener for the default player events.
mServer.setListener(new ITVULiveRoomServerListener() {

    /**
     * Callback triggered when getting the live room information successfully.
     * @param activityResult Live room data returned from the BytePlus Live server.
     */
    @Override
    public void onGetRoomDataSuccess(ActivityResult activityResult) {
    }

    /**
     * Callback triggered when failing to get the live room information.
     *
     * @param errCode The error code. 0: An error occurred when parsing data returned from the BytePlus Live server. 1: The live room is not available on mobile devices.
     * @param errMsg The error message explaining the reason for failure.
     */
    @Override
    public void onGetRoomDataFailed(int errCode, String errMsg) {
    }

    /**
     * Callback triggered when the full-screen or exit-full-screen icon is tapped. You can change the player's orientation, show or hide the status bar, and more in this callback.
     */
    @Override
    public void onFullScreenChange() {
        // If the current player's orientation is portrait, switch to landscape.
        if (ActivityInfo.SCREEN_ORIENTATION_PORTRAIT == getRequestedOrientation()) {
            setRequestedOrientation(ActivityInfo.SCREEN_ORIENTATION_LANDSCAPE);
            Toast.makeText(getBaseContext(), "Tap the full-screen icon to watch videos in landscape orientation", Toast.LENGTH_LONG).show();
            BarUtils.setStatusBarVisibility(ModularizationActivity.this, false); // Enter full-screen mode, and hide the status bar.
            ViewHelper.removeViewParent(playerView);
            playerView.setIsLandScape(true);
            landPlayerViewContainer.setVisibility(View.VISIBLE);
            landPlayerViewContainer.addView(playerView, 0, new FrameLayout.LayoutParams(ViewGroup.LayoutParams.MATCH_PARENT,
                    ViewGroup.LayoutParams.MATCH_PARENT));
        } else {
            setRequestedOrientation(ActivityInfo.SCREEN_ORIENTATION_PORTRAIT); // If the current player's orientation is landscape, switch to portrait.
            BarUtils.setStatusBarVisibility(ModularizationActivity.this, true); // Exit full-screen mode, and show the status bar.
            ViewHelper.removeViewParent(playerView);
            playerView.setIsLandScape(false);
            landPlayerViewContainer.setVisibility(View.GONE);
            playerViewContainer.addView(playerView, new FrameLayout.LayoutParams(ViewGroup.LayoutParams.MATCH_PARENT,
                    ViewGroup.LayoutParams.MATCH_PARENT));
        }
    }

    /**
     * Callback triggered when the live room status changes.
     * @param value The current live room status. 1: Live. 2: Preview. 3: Playback. 4: Over.
     */
    @Override
    public void liveRoomStatusChange(int value) {
    }

    /**
     * Callback triggered when the play status changes.
     * @param playerStatus The current play status. 0: Paused. 1: Playing.
     */
    @Override
    public void playerStatusChange(int playerStatus) {
    }

    /**
     * Callback triggered when the playback speed button is tapped.
     */
    @Override
    public void onSpeedButtonDidTouch() {
    }

    /**
     * Callback triggered when the replay button is tapped.
     */
    @Override
    public void onReplayButtonDidTouch() {
    }
});
```


<span id="aeca63f4"></span>
### Leaving the live room

Use the following sample code to leave the live room and destroy the default player when viewers exit your viewing page.

```Java
mServer.closeRoom();
```


<span id="1cee0370"></span>
### Complete sample code

The following sample code takes a live room in portrait mode as an example, with the activity ID (`activityId`) as `1721010849258****`, the `token` as `pg****`, and the authentication mode (`roomAuthMode`) as public. You can modify the parameter values as needed.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Call <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-createactivityapiv2">CreateActivityAPIV2</a> or <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi">ListActivityAPI</a> to get the activity ID of the live room.</div>


* <div data-tips="true" data-tips-type="tip">Call <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi">GetSDKTokenAPI</a> and set the value of <code>Mode</code> to <code>1</code> to get the authorization token in public mode.</div>



```Java
long activityId = 1721010849258****;
String token = "pg****";

TVULiveRoomServer mServer = new TVULiveRoomServer(this, activityId, token, TVULiveRoomServer.SERVER_TYPE_PORTRAIT_LIVEROOM);
PlayerView playerView = (PlayerView) LayoutInflater.from(this).inflate(com.bytedance.live.sdk.R.layout.tvu_player_layout, null, false);
mServer.setRoomAuthMode(TVULiveRoom.TVURoomAuthMode.PUBLIC);
mServer.setPlayerView(playerView);
FrameLayout playerViewContainer = findViewById(R.id.player_view_container);
playerViewContainer.addView(playerView, new FrameLayout.LayoutParams(ViewGroup.LayoutParams.MATCH_PARENT, ViewGroup.LayoutParams.MATCH_PARENT));
// Start the TVULiveRoomServer instance.
mServer.start();
// Leave the live room and destroy the default player.
mServer.closeRoom();
```
