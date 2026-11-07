---
title: "Android 观播 SDK：基础功能"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-basic-for-viewer-sdk-for-android-zh-CN"
---

本主题介绍如何集成 Android 观播 SDK 的基础功能，包括如何集成完整直播间、独立播放器和完整播放器。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">目前，观众一次只能加入一个直播间。</div>


<span id="9e3ed5fc"></span>
## 前提条件

完成 [集成 Android 观播 SDK](https://docs.byteplus.com/docs/byteplus-livesaas/docs-integrating-the-viewer-sdk-for-android-zh-CN) 的前 5 步。

<span id="4d05724b"></span>
## 功能

本主题介绍如何集成以下功能。


* [完整直播间](https://docs.byteplus.com/docs/byteplus-livesaas/docs-basic-for-viewer-sdk-for-android-zh-CN#d27888d9)

* [独立播放器](https://docs.byteplus.com/docs/byteplus-livesaas/docs-basic-for-viewer-sdk-for-android-zh-CN#380007d1)

* [完整播放器](https://docs.byteplus.com/docs/byteplus-livesaas/docs-basic-for-viewer-sdk-for-android-zh-CN#4b8efe3c)


<span id="d27888d9"></span>
## 完整直播间

完整直播间包含 BytePlus Live 直播间的所有功能模块，相较于单独集成模块，集成更简单、便捷。除非有特殊需求，建议集成完整直播间。

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b5e29c4a28954ea2a00c0139bf42ff86~tplv-goo7wpa0wc-image.image) </span>

关于完整直播间支持的功能详情，请参见 [SaaS 与 aPaaS 功能对比](https://docs.byteplus.com/docs/byteplus-livesaas/docs-feature-comparison-between-saas-and-apaas-zh-CN)。

<span id="3e176d1e"></span>
### 进入直播间

调用 [joinLiveRoom](https://docs.byteplus.com/docs/byteplus-livesaas/docs-tvuliveroom-zh-CN#b20db0d1) 方法，允许观众进入完整直播间，并在应用中展示完整直播间页面。

示例代码如下。

```Java
long activityId = ACTIVITY_ID; // Replace ACTIVITY_ID with the activity ID of the live room.
String token = "TOKEN"; // Replace TOKEN with the authorization token required to join the live room.
TVULiveRoom.TVURoomAuthMode roomAuthMode = TVULiveRoom.TVURoomAuthMode.PUBLIC; // The authentication mode of the live room.本示例使用公开模式，观众无需登录即可观看直播流和查看评论。
boolean isPortrait = true;// Whether the live room is in portrait mode.此处以竖屏模式为例。
// Join the live room.
TVULiveRoom.joinLiveRoom(context, new JoinRoomConfig(activityId,token,roomAuthMode,isPortrait));
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">调用<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-createactivityapiv2-zh-CN">CreateActivityAPIV2</a>或<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-CN">ListActivityAPI</a>获取直播间的活动 ID。</div>


* <div data-tips="true" data-tips-type="tip">调用<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi-zh-CN">GetSDKTokenAPI</a>并将<code>Mode</code>的值设置为<code>1</code>，以公开模式获取授权 token。如需将认证模式更改为自定义，请参见<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-advanced-for-the-viewer-sdk-for-android-zh-CN#e54b3982">自定义登录</a>。</div>



<span id="6ca81fd6"></span>
### 自定义直播间

在进入直播间前，可调用 `CustomSettings.Holder.mSettings.set` 方法自定义直播间的以下显示效果。


* 字体：使用 TypeFace 设置字体。

* 字体大小：使用整数值设置字体大小。单位：sp。

* 图片：使用 Drawable 对象设置图片。支持 PNG 和 JPG 格式的图片。

* 颜色：使用整数值设置颜色。例如，白色为 `0xFFFFFFFF`。采用 RGB 色彩模型，使用 ARGB 表示方式。

* 其他。


使用以下示例代码，将关闭直播间的图标自定义为名为 `tvu_nav_icon_back_melon` 的图片。

```Java
CustomSettings settings = CustomSettings.Holder.mSettings;
settings.setExitRoomIcon(ContextCompat.getDrawable(this, R.drawable.tvu_nav_icon_back_melon));
```


关于直播间自定义的更多信息，请参见 [mSettings](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-CN) 类的方法。

<span id="2f10c4ae"></span>
### 离开直播间

当需要观众离开直播间，例如观众无权限观看视频时，可调用 [leaveLiveRoom](https://docs.byteplus.com/docs/byteplus-livesaas/docs-tvuliveroom-zh-CN#9fab7a9d) 方法。如需允许观众重新进入直播间，可再次调用 [joinLiveRoom](https://docs.byteplus.com/docs/byteplus-livesaas/docs-tvuliveroom-zh-CN#b20db0d1) 方法。

示例代码如下。

```Java
TVULiveRoom.leaveLiveRoom(context);
```


<span id="2729cb86"></span>
### 销毁悬浮窗

悬浮窗，也称为画中画（PiP）窗口。

若已开启悬浮窗权限，观众退出直播间页面时会显示悬浮窗。如无需显示悬浮窗，可进行销毁操作。销毁悬浮窗时，悬浮窗中的对应播放器也会被销毁。

示例代码如下。

```Java
TVULiveRoom.destroyFloatWindow();
```


<span id="8e3c6e92"></span>
### 完整示例代码

以下示例代码以竖屏模式的直播间为例，活动 ID（`activityId`）为 `1721010849258****`，`token` 为 `pg****`，认证模式（`roomAuthMode`）为 public。可根据需要修改参数值。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">调用<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-createactivityapiv2-zh-CN">CreateActivityAPIV2</a>或<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-CN">ListActivityAPI</a>获取直播间的活动 ID。</div>


* <div data-tips="true" data-tips-type="tip">调用<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi-zh-CN">GetSDKTokenAPI</a>并将<code>Mode</code>的值设置为<code>1</code>，以公开模式获取授权 token。如需将认证模式更改为自定义，请参见<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-advanced-for-the-viewer-sdk-for-android-zh-CN#e54b3982">自定义登录</a>。</div>



```Java
long activityId = 1721010849258****;
String token = "pg****";
TVULiveRoom.TVURoomAuthMode roomAuthMode = TVULiveRoom.TVURoomAuthMode.PUBLIC;
boolean isPortrait = true;
// (Optional) Customize the live room.此处以自定义关闭直播间图标为例。
CustomSettings settings = CustomSettings.Holder.mSettings;
settings.setExitRoomIcon(ContextCompat.getDrawable(this, R.drawable.tvu_nav_icon_back_melon));
// Join the live room.
TVULiveRoom.joinLiveRoom(context, new JoinRoomConfig(activityId,token,roomAuthMode,isPortrait));
// Leave the live room.
TVULiveRoom.leaveLiveRoom(context);
```


<span id="380007d1"></span>
## 独立播放器

独立播放器不包含控制界面，即没有播放按钮等交互按钮。

独立播放器实例 `TVUSinglePlayerView` 包含两个元素：`TextureView` 和视频封面图。该实例还开放了多个 API 和事件，便于将独立播放器嵌入页面并实现以下功能：


* 在你的页面上的独立播放器中添加自定义控制界面。

* 在你的页面上展示多个独立播放器，每个播放器对应不同的直播间。当观众点击页面上展示的独立播放器时，可以进入对应的完整直播间。

   当观众点击你页面上的独立播放器时，必须使用完整直播间章节[进入直播间](https://docs.byteplus.com/docs/byteplus-livesaas/docs-basic-for-viewer-sdk-for-android-zh-CN#3e176d1e)中提供的代码。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bd187e4c9e4f406fb192f3ffc6e98ae4~tplv-goo7wpa0wc-image.image) </span>

* 实现你自己的悬浮窗，并在悬浮窗视图中展示独立播放器的内容。这样可以先展示悬浮窗，再展示完整直播间。例如，观众首先进入你的商品详情页查看商品，然后点击悬浮窗进入完整直播间。

   你必须将`videoView`（在[进入直播间](https://docs.byteplus.com/docs/byteplus-livesaas/docs-basic-for-viewer-sdk-for-android-zh-CN#fe765d44)的示例代码中）添加到悬浮窗视图，并在观众点击悬浮窗视图时，使用完整直播间章节[进入直播间](https://docs.byteplus.com/docs/byteplus-livesaas/docs-basic-for-viewer-sdk-for-android-zh-CN#3e176d1e)的示例代码。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/42b00e893d0d4c5d9bd233fe960a9c2a~tplv-goo7wpa0wc-image.image) </span>


<span id="fe765d44"></span>
### 进入直播间

使用以下示例代码进入直播间并创建独立播放器。

```Java
// Create the TVULiveRoomServer instance before calling the Activity.setContentView method.此处仅集成独立播放器作为示例。如需将聊天互动菜单、人气等直播间组件绑定到独立播放器，请将 SERVER_TYPE_SINGLE 替换为 SERVER_TYPE_LIVEROOM。
TVULiveRoomServer roomServer = new TVULiveRoomServer(this, activityId, token, TVULiveRoomServer.SERVER_TYPE_SINGLE);
// Set the authentication mode of the live room to public, allowing viewers to perform operations such as watching the live stream and viewing comments without logging in.
roomServer.setRoomAuthMode(TVULiveRoom.TVURoomAuthMode.PUBLIC);
// Initialize the TVUSinglePlayerView instance.
InitConfig initConfig = new InitConfig();
TVUSinglePlayerView videoView = findViewById(R.id.video_view);
videoView.init(initConfig);
// Bind the TVUSinglePlayerView instance to the TVULiveRoomServer instance.
roomServer.setPlayerView(videoView.getInnerPlayerView());
// Start the TVULiveRoomServer instance.实例启动后，播放器会自动播放视频。
roomServer.start();   
```


<span id="53bf8dc4"></span>
### 处理自定义控制界面中的按钮点击

在独立播放器中添加自定义控制界面后，可以设置按钮的点击行为。

以下示例代码设置了播放按钮和暂停按钮的点击行为。

```Java
// Find the videoView using the findViewById method.
TVUSinglePlayerView videoView = findViewById(R.id.video_view);
// Find the play button using the findViewById method.
Button btnPlay = findViewById(R.id.btn_play);
// Find the pause button using the findViewById method.
Button btnPause = findViewById(R.id.btn_pause);
// Set the play button's tap behavior to play the video.
btnPlay.setOnClickListener(v -> {
    videoView.play();
});
// Set the tap behavior of the pause button: pause the video when the pause button is tapped.
btnPause.setOnClickListener(v -> {
    videoView.pause();
});
```


<span id="5c92bfa9"></span>
### 实现独立播放器控制

启动`TVULiveRoomServer`实例后，可以调用相关方法实现独立播放器控制。更多信息，请参见[TVUSinglePlayerView](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview-zh-CN)。

以下示例代码演示如何在独立播放器中实现视频暂停和播放。

```Java
// Find the videoView using the findViewById method.
TVUSinglePlayerView videoView = findViewById(R.id.video_view);
videoView.pause();   // Pause the video.
videoView.play();    // Play the video.
```


<span id="6e0a8cd3"></span>
### 监听独立播放器事件

你可以监听独立播放器事件。更多信息，请参见[SinglePlayerListener](https://docs.byteplus.com/docs/byteplus-livesaas/docs-callback-the-viewer-sdk-for-android-zh-CN#e6e91c48)。

示例代码如下。

```Java
// Set the listener for custom player events.
initConfig.singlePlayerListener = new SinglePlayerListener() {
    /*** 当直播间状态发生变化时触发回调。*@paramstatus 当前直播间状态。*               1: 直播。*               2: 预告。*               3: 回放。*               4: 结束。*/
    @Override
    public void liveRoomStatusChanged(int status) {
    }

    /*** 当资源可播放状态发生变化时触发回调。*@paramplayableStatus 当前资源可播放状态。*                       0: 无可播放资源，无法调用 play 方法。*                       1: 点播视频（预告和回放）可播放。你可以调用 play 方法播放视频。*                       2: 直播流可播放。你可以调用 play 方法来播放视频。*/
    @Override
    public void playableStatusChanged(int playableStatus) {
    }

    /*** 播放状态发生变化时触发的回调。*@paramplayStatus 当前播放状态。*                   0: 已暂停。*                   1: 播放中。*/
    @Override
    public void playStatusChanged(int playStatus) {

    }

    /*** 视频尺寸发生变化时触发的回调。*@paramwidth 视频宽度。*@paramheight 视频高度。*/
    @Override
    public void sizeChanged(int width, int height) {
    }

    /*** 卡顿状态发生变化时触发的回调。你可以配置是否显示自定义加载动画。*@paramisStalling 视频是否卡顿。*                   true: 卡顿。*                   false: 未卡顿。*/
    @Override
    public void stallingStatusChanged(boolean isStalling) {
    }

    /*** VOD 错误回调。*@paramerror 错误详情。*/
    @Override
    public void vodErrorOccurred(Error error) {
    }

    /*** 直播错误回调。*@paramerror 错误详情。*/
    @Override
    public void liveErrorOccurred(LiveError error) {
    }

    /*** 播放错误回调，包括 VOD 和直播错误。此时视频处于暂停状态。你可以配置重试界面，引导观众点击重试。*@paramisPlayError 是否发生播放错误。*                    true: 发生播放错误。*                    false: 未发生播放错误。*/
    @Override
    public void playErrorStatusChanged(boolean isPlayError) {
    }

    /*** VOD 视频准备就绪时触发的回调。你可以调用 seekVodTime 方法。*/
    @Override
    public void vodPrepared() {
    }

    /*** VOD 视频渲染开始时触发的回调。*/
    @Override
    public void vodRenderStarted() {
    }

    /**
     * Callback triggered when a VOD video automatically resumes from its last position.*@paramseekTimeInMills 视频自动恢复后跳转到的位置。单位：ms。*/
    @Override
    public void vodAutoSeekPreviousTime(int seekTimeInMills) {
    }


    /*** VOD 视频播放进度变化时触发的回调。播放进度每秒更新一次。*@paramcurTimeInMills 当前播放进度。单位：ms。*/
    @Override
    public void vodCurPlayTimeChanged(int curTimeInMills) {
    }

    /*** VOD 视频总时长变化时触发的回调。该回调通常在视频切换时触发。*@paramdurationInMills 视频总时长。单位：ms。*/
    @Override
    public void vodDurationChanged(int durationInMills) {
    }

    /*** VOD 视频播放结束时触发的回调。*/
    @Override
    public void vodCompletion() {
    }

    /*** 直播流准备就绪时触发的回调。*/
    @Override
    public void livePrepared() {
    }

    /*** 直播流渲染开始时触发的回调。*@paramisFirstFrame 是否为实际渲染的首帧。该回调可能因直播流重试多次触发。*                     true: 调用 play 方法后为首帧。*                     false: 调用 play 方法后不是首帧。*/
    @Override
    public void liveFirstFrameRendered(boolean isFirstFrame) {
    }

    /*** 直播流结束时触发的回调。*/
    @Override
    public void liveCompletion() {
    }

    /*** 封面可见状态变化时触发的回调。视频播放时封面不可见，无视频播放时封面可见。*@paramisVisible 封面是否可见。*                  true: 可见。*                  false: 不可见。*/
    @Override
    public void coverImageVisibleChanged(boolean isVisible) {
    }

    /*** 视频分辨率信息变化时触发的回调。该回调通常在视频切换时触发。*@paramresolutions 当前支持的分辨率列表。*@paramdefaultResolution 默认选中的分辨率。*/
    @Override
    public void resolutionInfoChanged(String[] resolutions, String defaultResolution) {
    }

    /*** 播放中的 VOD 视频 Vid 变化回调，在观看页播放的 VOD 视频变化或直播间状态变化时触发。*@paramvid 播放中的 VOD 视频的 Vid。如果没有正在播放的点播视频，则返回空字符串。*/
    @Override
    public void onCurVodVidChanged(String vid) {
    }

    /*** 直播间回放列表变更的回调，在回放发布、撤回或直播间状态变更时触发。*@paramreplayList 直播间的回放列表。如果直播间没有回放，则返回空数组。*/
    @Override
    public void onCurReplayListChanged(List<Replay> replayList) {
    }

    /*** 当直播源 ID 变更时触发的回调。*@paramlineId 当前直播源的 ID。如果直播间不处于直播状态，则返回 0。*/
    @Override
    public void onCurLiveLineIdChanged(long lineId) {
    }

    /*** 直播源列表变更时触发的回调。*@paramliveLineList 直播源列表。如果直播间不处于直播状态，则返回空数组。*/
    @Override
    public void onCurLiveLineListChanged(List<PullStreamUrl> liveLineList) {
    }
};
```


<span id="d9382c20"></span>
### 退出直播间

在销毁你的页面等场景下，可以使用以下示例代码退出直播间并销毁独立播放器。

```Java
roomServer.closeRoom();
```


<span id="d34628bd"></span>
### 完整示例代码

以下示例代码以竖屏模式的直播间为例，活动 ID（`activityId`）为`1721010849258****`，`token`为`pg****`，认证模式（`roomAuthMode`）为公开。你可以根据需要修改参数值。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">调用<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-createactivityapiv2-zh-CN">CreateActivityAPIV2</a>或<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-CN">ListActivityAPI</a>获取直播间的活动 ID。</div>


* <div data-tips="true" data-tips-type="tip">调用<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi-zh-CN">GetSDKTokenAPI</a>并将<code>Mode</code>的值设置为<code>1</code>，以获取公有模式下的授权 token。</div>



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
## 完整播放器

如果你有自己的观看页且无需自定义播放器控制界面，可以选择只集成完整播放器。

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d7030048aa90402fb42d3a870f35d327~tplv-goo7wpa0wc-image.image) </span>

<span id="ae62b077"></span>
### 进入直播间

使用以下示例代码进入直播间并创建完整播放器。

```Java
// Create the TVULiveRoomServer instance for a live room in portrait mode.如需为横屏模式的直播间创建 TVULiveRoomServer 实例，请将 TVULiveRoomServer.SERVER_TYPE_PORTRAIT_LIVEROOM 替换为 TVULiveRoomServer.SERVER_TYPE_LIVEROOM。
TVULiveRoomServer mServer = new TVULiveRoomServer(this, activityId, token, TVULiveRoomServer.SERVER_TYPE_PORTRAIT_LIVEROOM);
// Inflate the PlayerView instance from the player module.
PlayerView playerView = (PlayerView) LayoutInflater.from(this).inflate(com.bytedance.live.sdk.R.layout.tvu_player_layout, null, false);
// Set the authentication mode of the live room to public, allowing viewers to perform operations such as watching the live stream and viewing comments without logging in.
mServer.setRoomAuthMode(TVULiveRoom.TVURoomAuthMode.PUBLIC);
// Bind the PlayerView instance to the TVULiveRoomServer instance.
mServer.setPlayerView(playerView);
// Introduce your player container.
FrameLayout playerViewContainer = findViewById(R.id.player_view_container);
// Place the PlayerView instance into the container.
playerViewContainer.addView(playerView, new FrameLayout.LayoutParams(ViewGroup.LayoutParams.MATCH_PARENT, ViewGroup.LayoutParams.MATCH_PARENT));
//  Start the TVULiveRoomServer instance.实例启动后，播放器会自动播放视频。
mServer.start();
```


<span id="57cc739a"></span>
### 实现完整播放器控制

启动`TVULiveRoomServer`实例后，可以调用相关方法实现完整播放器控制。更多信息，请参见[PlayerView](https://docs.byteplus.com/docs/byteplus-livesaas/playerview-zh-CN)。

以下示例代码演示如何在完整播放器中实现视频暂停和播放。

```Java
// Inflate the PlayerView instance from the player module.
PlayerView playerView = (PlayerView) LayoutInflater.from(this).inflate(com.bytedance.live.sdk.R.layout.tvu_player_layout, null, false);
playerView.pause(); // Pause the video.
playerView.play();  // Play the video.
```


<span id="786492a5"></span>
### 监听完整播放器事件

你可以监听完整播放器事件。更多信息，请参见[ITVULiveRoomServerListener](https://docs.byteplus.com/docs/byteplus-livesaas/docs-callback-the-viewer-sdk-for-android-zh-CN#1b64c86a)。

示例代码如下。

```Java
// Set the listener for the default player events.
mServer.setListener(new ITVULiveRoomServerListener() {

    /**
     * Callback triggered when the live room information is retrieved successfully.*@paramactivityResult BytePlus Live 服务端返回的直播间数据。*/
    @Override
    public void onGetRoomDataSuccess(ActivityResult activityResult) {
    }

    /*** 获取直播间信息失败时触发的回调。**@paramerrCode 错误码。0：解析 BytePlus Live 服务端返回数据时发生错误。1：直播间不支持移动端访问。*@paramerrMsg 说明失败原因的错误信息。*/
    @Override
    public void onGetRoomDataFailed(int errCode, String errMsg) {
    }

    /**
     * Callback triggered when the full-screen or exit-full-screen icon is tapped.在该回调中，可实现切换播放器方向或切换状态栏显示/隐藏的逻辑。*/
    @Override
    public void onFullScreenChange() {
        // If the current player's orientation is portrait, switch to landscape.
        if (ActivityInfo.SCREEN_ORIENTATION_PORTRAIT == getRequestedOrientation()) {
            setRequestedOrientation(ActivityInfo.SCREEN_ORIENTATION_LANDSCAPE);
            Toast.makeText(getBaseContext(), "Tap the full-screen icon to watch videos in landscape orientation", Toast.LENGTH_LONG).show();
            BarUtils.setStatusBarVisibility(ModularizationActivity.this, false); // Enter full-screen mode and hide the status bar.
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

    /*** 直播间状态变更时触发的回调。*@paramvalue 当前直播间状态。1：直播。2：预告。3：回放。4：结束。*/
    @Override
    public void liveRoomStatusChange(int value) {
    }

    /*** 当播放状态发生变化时触发回调。*@paramplayerStatus 当前播放状态。0: 已暂停。1: 播放中。*/
    @Override
    public void playerStatusChange(int playerStatus) {
    }

    /*** 当点击回放速度按钮时触发回调。*/
    @Override
    public void onSpeedButtonDidTouch() {
    }

    /*** 当点击重播按钮时触发回调。*/
    @Override
    public void onReplayButtonDidTouch() {
    }
});
```


<span id="aeca63f4"></span>
### 退出直播间

当观众退出你的观看页时，使用以下示例代码退出直播间并销毁完整播放器。

```Java
mServer.closeRoom();
```


<span id="1cee0370"></span>
### 完整示例代码

以下示例代码以竖屏模式的直播间为例，活动 ID（`activityId`）为`1721010849258****`，`token`为`pg****`，认证模式（`roomAuthMode`）为公开。你可以根据需要修改参数值。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">调用 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-createactivityapiv2-zh-CN">CreateActivityAPIV2</a> 或 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-CN">ListActivityAPI</a> 获取直播间的活动 ID。</div>


* <div data-tips="true" data-tips-type="tip">调用 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi-zh-CN">GetSDKTokenAPI</a> 并将 <code>Mode</code> 的值设置为 <code>1</code>，以获取公共模式下的授权令牌。</div>



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
