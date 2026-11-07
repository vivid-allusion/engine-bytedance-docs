---
title: "Android 版 Viewer SDK：基本功能"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/android-ban-viewer-sdk-ji-ben-gong-neng-zh-TW"
---

本主題說明如何整合 Android 版 Viewer SDK 的基本功能，包括如何整合全功能直播間、自訂播放器和預設播放器。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">目前，觀眾一次只能加入一個直播間。</div>


<span id="9e3ed5fc"></span>
## 先決條件

完成 [整合 Android Viewer SDK](https://docs.byteplus.com/docs/byteplus-livesaas/zheng-he-android-viewer-sdk-zh-TW) 中的前 5 個步驟。

<span id="4d05724b"></span>
## 功能

本主題說明如何整合以下功能。


* [全功能直播間](https://docs.byteplus.com/docs/byteplus-livesaas/android-ban-viewer-sdk-ji-ben-gong-neng-zh-TW#d27888d9)

* [自訂播放器](https://docs.byteplus.com/docs/byteplus-livesaas/android-ban-viewer-sdk-ji-ben-gong-neng-zh-TW#380007d1)

* [預設播放器](https://docs.byteplus.com/docs/byteplus-livesaas/android-ban-viewer-sdk-ji-ben-gong-neng-zh-TW#4b8efe3c)


<span id="d27888d9"></span>
## 全功能直播間

全功能直播間包含 BytePlus Live 直播間的所有功能模組，與單獨模組相比，整合更簡單且更方便。除非有特殊需求，建議您整合全功能直播間。

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b5e29c4a28954ea2a00c0139bf42ff86~tplv-goo7wpa0wc-image.image) </span>

如需瞭解全功能直播間支援的功能，請參見 [SaaS 與 aPaaS 的功能比較](https://docs.byteplus.com/docs/byteplus-livesaas/saas-yu-apaas-de-gong-neng-bi-jiao-zh-TW)。

<span id="3e176d1e"></span>
### 進入直播間

呼叫 [joinLiveRoom](https://docs.byteplus.com/docs/byteplus-livesaas/docs-tvuliveroom-zh-TW#b20db0d1) 方法，讓觀眾進入全功能直播間，並在應用程式中顯示全功能直播間頁面。

範例程式碼如下。

```Java
long activityId = ACTIVITY_ID; // Replace ACTIVITY_ID with the activity ID of the live room.
String token = "TOKEN"; // Replace TOKEN with the authorization token required to join the live room.
TVULiveRoom.TVURoomAuthMode roomAuthMode = TVULiveRoom.TVURoomAuthMode.PUBLIC; // The authentication mode of the live room.本範例使用公開模式，允許觀眾在未登入的情況下觀看直播和查看評論。
boolean isPortrait = true;// Whether the live room is in portrait mode.此處以直式模式為例。
// Join the live room.
TVULiveRoom.joinLiveRoom(context, new JoinRoomConfig(activityId,token,roomAuthMode,isPortrait));
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">呼叫<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-createactivityapiv2-zh-TW">CreateActivityAPIV2</a>或<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-TW">ListActivityAPI</a>以獲取直播間的活動 ID。</div>


* <div data-tips="true" data-tips-type="tip">呼叫<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi-zh-TW">GetSDKTokenAPI</a>並將<code>Mode</code> 的值設為<code>1</code>，以獲取公開模式下的授權 token。如需將驗證模式更改為自訂，請參閱<a href="https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-jin-jie-gong-neng-zh-TW#e54b3982">自訂登入</a>。</div>



<span id="6ca81fd6"></span>
### 自訂直播間

在進入直播間前，您可以呼叫 `CustomSettings.Holder.mSettings.set` 方法，自訂直播間的以下顯示效果。


* 字型：使用 TypeFace 設定字型。

* 字型大小：使用整數值設定字型大小。單位：sp。

* 圖片：使用 Drawable 物件設定圖片。支援 PNG 和 JPG 格式的圖片。

* 顏色：使用整數值設定顏色。例如，白色為 `0xFFFFFFFF`。採用 RGB 色彩模型，使用 ARGB 表示法。

* 其他。


使用以下範例程式碼，將關閉直播間的圖示自訂為名為 `tvu_nav_icon_back_melon` 的圖片。

```Java
CustomSettings settings = CustomSettings.Holder.mSettings;
settings.setExitRoomIcon(ContextCompat.getDrawable(this, R.drawable.tvu_nav_icon_back_melon));
```


如需瞭解如何自訂直播間，請參見 [mSettings](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-TW) 類的方法。

<span id="2f10c4ae"></span>
### 離開直播間

當您需要讓觀眾離開直播間時，例如觀眾無權觀看影片時，可以呼叫 [leaveLiveRoom](https://docs.byteplus.com/docs/byteplus-livesaas/docs-tvuliveroom-zh-TW#9fab7a9d) 方法。如需讓觀眾重新進入直播間，可以再次呼叫 [joinLiveRoom](https://docs.byteplus.com/docs/byteplus-livesaas/docs-tvuliveroom-zh-TW#b20db0d1) 方法。

範例程式碼如下。

```Java
TVULiveRoom.leaveLiveRoom(context);
```


<span id="2729cb86"></span>
### 銷毀浮動視窗

浮動視窗亦稱為子母畫面（PiP）視窗。

若已啟用浮動視窗權限，當觀眾退出直播間頁面時，會顯示浮動視窗。若無需顯示浮動視窗，可將其銷毀。銷毀浮動視窗時，對應的浮動視窗播放器也會一併銷毀。

範例程式碼如下。

```Java
TVULiveRoom.destroyFloatWindow();
```


<span id="8e3c6e92"></span>
### 完整範例程式碼

以下範例程式碼以直式模式的直播間為例，activity ID（`activityId`）為 `1721010849258****`，`token` 為 `pg****`，驗證模式（`roomAuthMode`）為公開。您可根據需要修改參數值。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">呼叫<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-createactivityapiv2-zh-TW">CreateActivityAPIV2</a>或<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-TW">ListActivityAPI</a>以獲取直播間的活動 ID。</div>


* <div data-tips="true" data-tips-type="tip">呼叫<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi-zh-TW">GetSDKTokenAPI</a>並將<code>Mode</code> 的值設為<code>1</code>，以獲取公開模式下的授權 token。如需將驗證模式更改為自訂，請參閱<a href="https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-jin-jie-gong-neng-zh-TW#e54b3982">自訂登入</a>。</div>



```Java
long activityId = 1721010849258****;
String token = "pg****";
TVULiveRoom.TVURoomAuthMode roomAuthMode = TVULiveRoom.TVURoomAuthMode.PUBLIC;
boolean isPortrait = true;
// (Optional) Customize the live room.此處以自訂關閉直播間的圖示為例。
CustomSettings settings = CustomSettings.Holder.mSettings;
settings.setExitRoomIcon(ContextCompat.getDrawable(this, R.drawable.tvu_nav_icon_back_melon));
// Join the live room.
TVULiveRoom.joinLiveRoom(context, new JoinRoomConfig(activityId,token,roomAuthMode,isPortrait));
// Leave the live room.
TVULiveRoom.leaveLiveRoom(context);
```


<span id="380007d1"></span>
## 自訂播放器

自訂播放器不包含控制介面，即不具備播放按鈕等互動按鈕。

自訂播放器實例 `TVUSinglePlayerView` 包含兩個元素：`TextureView` 和影片封面圖片。該實例同時提供多個 API 和事件，方便您將自訂播放器嵌入頁面並實現以下功能：


* 在您自己的頁面上，為自訂播放器新增自訂控制介面。

* 在您自己的頁面上顯示多個自訂播放器，每個播放器對應不同的直播間。當觀眾點擊頁面上顯示的自訂播放器時，可以進入對應的全功能直播間。

   當觀眾點擊您自己頁面上的自訂播放器時，必須使用全功能直播間章節[進入直播間](https://docs.byteplus.com/docs/byteplus-livesaas/android-ban-viewer-sdk-ji-ben-gong-neng-zh-TW#3e176d1e)中提供的程式碼。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bd187e4c9e4f406fb192f3ffc6e98ae4~tplv-goo7wpa0wc-image.image) </span>

* 實作您自己的浮動視窗，並在浮動視窗中顯示自訂播放器的內容。這樣可以先顯示浮動視窗，再顯示全功能直播間。例如，觀眾先進入您的商品詳情頁查看商品，然後點擊浮動視窗進入全功能直播間。

   您必須將`videoView`（於[進入直播間](https://docs.byteplus.com/docs/byteplus-livesaas/android-ban-viewer-sdk-ji-ben-gong-neng-zh-TW#fe765d44)的範例程式碼中）新增至浮動視窗，並在觀眾點擊浮動視窗時，使用全功能直播間章節[進入直播間](https://docs.byteplus.com/docs/byteplus-livesaas/android-ban-viewer-sdk-ji-ben-gong-neng-zh-TW#3e176d1e)的範例程式碼。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/42b00e893d0d4c5d9bd233fe960a9c2a~tplv-goo7wpa0wc-image.image) </span>


<span id="fe765d44"></span>
### 進入直播間

使用以下範例程式碼進入直播間並建立自訂播放器。

```Java
// Create the TVULiveRoomServer instance before calling the Activity.setContentView method.此處僅整合自訂播放器作為範例。如需將聊天互動選單、人氣等直播間元件綁定至自訂播放器，請將 SERVER_TYPE_SINGLE 替換為 SERVER_TYPE_LIVEROOM。
TVULiveRoomServer roomServer = new TVULiveRoomServer(this, activityId, token, TVULiveRoomServer.SERVER_TYPE_SINGLE);
// Set the authentication mode of the live room to public, allowing viewers to perform operations such as watching the live stream and viewing comments without logging in.
roomServer.setRoomAuthMode(TVULiveRoom.TVURoomAuthMode.PUBLIC);
// Initialize the TVUSinglePlayerView instance.
InitConfig initConfig = new InitConfig();
TVUSinglePlayerView videoView = findViewById(R.id.video_view);
videoView.init(initConfig);
// Bind the TVUSinglePlayerView instance to the TVULiveRoomServer instance.
roomServer.setPlayerView(videoView.getInnerPlayerView());
// Start the TVULiveRoomServer instance.啟動實例後，播放器會自動播放影片。
roomServer.start();   
```


<span id="53bf8dc4"></span>
### 處理自訂控制介面中的按鈕點擊

在自訂播放器中新增自訂控制介面後，您可以設定按鈕的點擊行為。

以下範例程式碼設定了播放按鈕與暫停按鈕的點擊行為。

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
### 實作自訂播放器控制

啟動`TVULiveRoomServer`實例後，您可以呼叫相關方法以實作自訂播放器控制。如需更多資訊，請參閱[TVUSinglePlayerView](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview-zh-TW)。

以下範例程式碼展示如何在自訂播放器中實作影片暫停與播放。

```Java
// Find the videoView using the findViewById method.
TVUSinglePlayerView videoView = findViewById(R.id.video_view);
videoView.pause();   // Pause the video.
videoView.play();    // Play the video.
```


<span id="6e0a8cd3"></span>
### 監聽自訂播放器事件

您可以監聽自訂播放器事件。如需更多資訊，請參閱[SinglePlayerListener](https://docs.byteplus.com/docs/byteplus-livesaas/android-viewer-sdk-hui-hu-zh-TW#e6e91c48)。

範例程式碼如下。

```Java
// Set the listener for custom player events.
initConfig.singlePlayerListener = new SinglePlayerListener() {
    /*** 當直播間狀態變更時觸發回調。*@paramstatus 當前直播間狀態。*               1: 直播中。*               2: 預覽。*               3: 回放。*               4: 結束。*/
    @Override
    public void liveRoomStatusChanged(int status) {
    }

    /*** 當資源可播放狀態變更時觸發回調。*@paramplayableStatus 當前資源可播放狀態。*                       0: 無可播放資源，因此無法呼叫播放方法。*                       1: 隨選視訊（VOD）影片（預覽和回放）可播放。您可以呼叫播放方法來播放影片。*                       2: 直播流可播放。你可以呼叫 play 方法來播放影片。*/
    @Override
    public void playableStatusChanged(int playableStatus) {
    }

    /*** 播放狀態變更時觸發的回調。*@paramplayStatus 當前播放狀態。*                   0：已暫停。*                   1：播放中。*/
    @Override
    public void playStatusChanged(int playStatus) {

    }

    /*** 當影片尺寸變更時觸發的回調。*@paramwidth 影片寬度。*@paramheight 影片高度。*/
    @Override
    public void sizeChanged(int width, int height) {
    }

    /*** 卡頓狀態變更時觸發的回調。你可以設定是否顯示自訂加載動畫。*@paramisStalling 影片是否卡頓。*                   true：卡頓中。*                   false：未卡頓。*/
    @Override
    public void stallingStatusChanged(boolean isStalling) {
    }

    /*** VOD 錯誤的回調。*@paramerror 錯誤詳情。*/
    @Override
    public void vodErrorOccurred(Error error) {
    }

    /*** 直播錯誤的回調。*@paramerror 錯誤詳情。*/
    @Override
    public void liveErrorOccurred(LiveError error) {
    }

    /*** 播放錯誤的回調，包括 VOD 和直播錯誤。此時影片會暫停。你可以設定重試畫面，引導觀眾點擊重試。*@paramisPlayError 是否發生播放錯誤。*                    true：發生播放錯誤。*                    false：未發生播放錯誤。*/
    @Override
    public void playErrorStatusChanged(boolean isPlayError) {
    }

    /***  VOD 影片準備完成時觸發的回調。你可以呼叫 seekVodTime 方法。*/
    @Override
    public void vodPrepared() {
    }

    /*** VOD 影片開始渲染時觸發的回調。*/
    @Override
    public void vodRenderStarted() {
    }

    /**
     * Callback triggered when a VOD video automatically resumes from its last position.*@paramseekTimeInMills 影片自動恢復後跳轉的位置。單位：毫秒。*/
    @Override
    public void vodAutoSeekPreviousTime(int seekTimeInMills) {
    }


    /*** VOD 影片播放進度變更時觸發的回調。播放進度每秒更新一次。*@paramcurTimeInMills 當前播放進度。單位：毫秒。*/
    @Override
    public void vodCurPlayTimeChanged(int curTimeInMills) {
    }

    /*** VOD 影片總時長變更時觸發的回調。此回調通常在切換影片時觸發。*@paramdurationInMills 影片總時長。單位：毫秒。*/
    @Override
    public void vodDurationChanged(int durationInMills) {
    }

    /*** VOD 影片播放結束時觸發的回調。*/
    @Override
    public void vodCompletion() {
    }

    /*** 直播流準備完成時觸發的回調。*/
    @Override
    public void livePrepared() {
    }

    /*** 直播流開始渲染時觸發的回調。*@paramisFirstFrame 是否為實際渲染的第一幀。由於直播過程中可能重試，此回調可能會多次觸發。*                     true：呼叫 play 方法後的第一幀。*                     false：呼叫 play 方法後非第一幀。*/
    @Override
    public void liveFirstFrameRendered(boolean isFirstFrame) {
    }

    /*** 直播流結束時觸發的回調。*/
    @Override
    public void liveCompletion() {
    }

    /*** 封面顯示狀態變更時觸發的回調。影片播放時封面不可見，未播放時封面可見。*@paramisVisible 封面是否可見。*                  true：可見。*                  false：不可見。*/
    @Override
    public void coverImageVisibleChanged(boolean isVisible) {
    }

    /*** 影片解析度資訊變更時觸發的回調。此回調通常在切換影片時觸發。*@paramresolutions 當前支援的解析度列表。*@paramdefaultResolution 預設選擇的解析度。*/
    @Override
    public void resolutionInfoChanged(String[] resolutions, String defaultResolution) {
    }

    /*** 播放中的 VOD 影片 Vid 變更時的回調，當觀看頁播放的 VOD 影片變更或直播間狀態變更時觸發。*@paramvid 播放中的 VOD 影片 Vid。若未播放任何 VOD 影片，則回傳空字串。*/
    @Override
    public void onCurVodVidChanged(String vid) {
    }

    /*** 直播間回放列表變更的回調，於回放釋出、撤回或直播間狀態變更時觸發。*@paramreplayList 直播間的回放列表。若直播間無回放，則回傳空陣列。*/
    @Override
    public void onCurReplayListChanged(List<Replay> replayList) {
    }

    /*** 當直播源 ID 變更時觸發的回調。*@paramlineId 當前直播源的 ID。若直播間非 Live 狀態，則回傳 0。*/
    @Override
    public void onCurLiveLineIdChanged(long lineId) {
    }

    /*** 當直播源列表變更時觸發的回調。*@paramliveLineList 直播源列表。若直播間非 Live 狀態，則回傳空陣列。*/
    @Override
    public void onCurLiveLineListChanged(List<PullStreamUrl> liveLineList) {
    }
};
```


<span id="d9382c20"></span>
### 離開直播間

在銷毀您自己頁面等場景下，您可以使用以下範例程式碼離開直播間並銷毀自訂播放器。

```Java
roomServer.closeRoom();
```


<span id="d34628bd"></span>
### 完整範例程式碼

以下範例程式碼以直式模式的直播間為例，activity ID（`activityId`）為`1721010849258****`，`token`為`pg****`，驗證模式（`roomAuthMode`）為公開。您可以根據需要修改參數值。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">呼叫 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-createactivityapiv2-zh-TW">CreateActivityAPIV2</a> 或 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-TW">ListActivityAPI</a> 以取得直播間的活動 ID。</div>


* <div data-tips="true" data-tips-type="tip">呼叫 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi-zh-TW">GetSDKTokenAPI</a> 並將 <code>Mode</code> 的值設為 <code>1</code>，以取得公眾模式下的授權憑證。</div>



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
## 預設播放器

如果您有自己的觀看頁面且不需要自訂播放器控制介面，可以選擇僅整合預設播放器。

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d7030048aa90402fb42d3a870f35d327~tplv-goo7wpa0wc-image.image) </span>

<span id="ae62b077"></span>
### 進入直播間

使用以下範例程式碼進入直播間並建立預設播放器。

```Java
// Create the TVULiveRoomServer instance for a live room in portrait mode.若要建立橫式直播間的 TVULiveRoomServer 實例，請將 TVULiveRoomServer.SERVER_TYPE_PORTRAIT_LIVEROOM 替換為 TVULiveRoomServer.SERVER_TYPE_LIVEROOM。
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
//  Start the TVULiveRoomServer instance.啟動實例後，播放器會自動播放影片。
mServer.start();
```


<span id="57cc739a"></span>
### 實作預設播放器控制

啟動`TVULiveRoomServer`實例後，您可以呼叫相關方法以實作預設播放器控制。如需更多資訊，請參閱[PlayerView](https://docs.byteplus.com/docs/byteplus-livesaas/playerview-zh-TW)。

以下範例程式碼展示如何在預設播放器中實作影片暫停與播放。

```Java
// Inflate the PlayerView instance from the player module.
PlayerView playerView = (PlayerView) LayoutInflater.from(this).inflate(com.bytedance.live.sdk.R.layout.tvu_player_layout, null, false);
playerView.pause(); // Pause the video.
playerView.play();  // Play the video.
```


<span id="786492a5"></span>
### 監聽預設播放器事件

您可以監聽預設播放器事件。如需更多資訊，請參閱[ITVULiveRoomServerListener](https://docs.byteplus.com/docs/byteplus-livesaas/android-viewer-sdk-hui-hu-zh-TW#1b64c86a)。

範例程式碼如下。

```Java
// Set the listener for the default player events.
mServer.setListener(new ITVULiveRoomServerListener() {

    /**
     * Callback triggered when the live room information is retrieved successfully.*@paramactivityResult BytePlus Live 伺服器回傳的直播間資料。*/
    @Override
    public void onGetRoomDataSuccess(ActivityResult activityResult) {
    }

    /*** 取得直播間資訊失敗時觸發的回調。**@paramerrCode 錯誤碼。0：解析 BytePlus Live 伺服器回傳資料時發生錯誤。1：直播間不支援行動裝置。*@paramerrMsg 說明失敗原因的錯誤訊息。*/
    @Override
    public void onGetRoomDataFailed(int errCode, String errMsg) {
    }

    /**
     * Callback triggered when the full-screen or exit-full-screen icon is tapped.於此回調中可實作切換播放器方向或顯示/隱藏狀態列的邏輯。*/
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

    /*** 直播間狀態變更時觸發的回調。*@paramvalue 當前直播間狀態。1：直播中。2：預覽中。3：回放中。4：已結束。*/
    @Override
    public void liveRoomStatusChange(int value) {
    }

    /*** 當播放狀態變更時觸發回呼函式。*@paramplayerStatus 當前播放狀態。0: 已暫停。1: 播放中。*/
    @Override
    public void playerStatusChange(int playerStatus) {
    }

    /*** 當點擊播放速度按鈕時觸發回呼函式。*/
    @Override
    public void onSpeedButtonDidTouch() {
    }

    /*** 當點擊重播按鈕時觸發回呼函式。*/
    @Override
    public void onReplayButtonDidTouch() {
    }
});
```


<span id="aeca63f4"></span>
### 離開直播間

當觀眾離開您的觀看頁面時，請使用以下範例程式碼離開直播間並銷毀預設播放器。

```Java
mServer.closeRoom();
```


<span id="1cee0370"></span>
### 完整範例程式碼

以下範例程式碼以直式模式的直播間為例，活動 ID（`activityId`）為`1721010849258****`，`token` 為`pg****`，驗證模式（`roomAuthMode`）為公開。您可以根據需要修改參數值。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">呼叫 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-createactivityapiv2-zh-TW">CreateActivityAPIV2</a> 或 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-TW">ListActivityAPI</a> 以取得直播間的活動 ID。</div>


* <div data-tips="true" data-tips-type="tip">呼叫 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi-zh-TW">GetSDKTokenAPI</a> 並將 <code>Mode</code> 的值設為 <code>1</code>，以取得公開模式下的授權令牌。</div>



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
