---
title: "Android 平臺 CSAI 整合"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/csai-integration-for-android-zh-TW"
---

本指南介紹如何將 BytePlus MediaAds SDK 和 Google IMA SDK 整合到基於 VideoOne 的短劇 Android 應用中。

<span id="10c2b5c1"></span>
## 前置條件

在開始之前，請確保您已具備以下條件：


1. **已有整合**：您已整合 VideoOne 短劇解決方案（詳見[短劇影片 - Android 整合](https://docs.byteplus.com/docs/byteplus-vos/short-drama-videos-android-integration-zh-TW)）。

2. **Google Play 服務**：您的應用必須包含 Google Play 服務，以支援 Google IMA SDK。

3. **廣告標籤 URL**：您需要一個有效的 VAST/VMAP 廣告標籤 URL。

   * 測試時：您可以使用 [Google 的 VAST 標籤示例](https://developers.google.com/interactive-media-ads/docs/sdks/html5/client-side/tags)。

   * 生產環境：請從您的廣告伺服器（如 Google Ad Manager）獲取廣告標籤 URL。

4. **最低 SDK 要求**：

   * `minSdkVersion`：24 或更高（Google IMA 必需）。

   * `Android Gradle 外掛（AGP）`：8.13.0 或更高（Google IMA 必需）。


<span id="64f0e2a3"></span>
## SDK 整合

請按照以下步驟將 MediaAds SDK 整合到您的 Android 專案中。


1. **配置應用屬性**：將您的應用渠道、ID 和名稱新增到專案根目錄下的 `gradle.properties` 檔案中。這些屬性將被 SDK 用於初始化和分析。

   ```Bash
   VOD_APP_CHANNEL=overseas
   VOD_APP_ID=522211
   VOD_APP_NAME=VideoOne
   
   # others ...
   ```
   

2. **新增依賴版本**：開啟 `libs.versions.toml` 檔案（版本庫），並定義 MediaAds SDK 和 Google IMA SDK 的版本。

   ```Bash
   interactivemedia = "3.38.0"
   mediaads = "2.0.0"
   
   # others ...
   
   google-interactivemedia = { module = "com.google.ads.interactivemedia.v3:interactivemedia", version.ref = "interactivemedia" }
   byteplus-mediaads = { module = "com.byteplus.mediaplus:mediaads", version.ref = "mediaads" }
   
   # others ...
   ```
   

3. **配置庫模組**：在庫級 `build.gradle` 檔案中，匯入 SDK 依賴，並將應用屬性注入到 `BuildConfig` 類中。這樣您的程式碼即可在執行時訪問這些值。

   ```Kotlin
   android {
       defaultConfig {
           // Read properties from the root project
           def VOD_APP_ID = project(':solutions:vod:vod-common').VOD_APP_ID
           def VOD_APP_NAME = project(':solutions:vod:vod-common').VOD_APP_NAME
           def VOD_APP_CHANNEL = project(':solutions:vod:vod-common').VOD_APP_CHANNEL
       
           // Inject properties into BuildConfig
           buildConfigField('String', 'VOD_APP_ID', "\"$VOD_APP_ID\"")
           buildConfigField('String', 'VOD_APP_NAME', "\"$VOD_APP_NAME\"")
           buildConfigField('String', 'VOD_APP_CHANNEL', "\"$VOD_APP_CHANNEL\"")
           
           // others ...
       }
       
       buildFeatures {
           buildConfig true
       }
   
       // others ...
   }
   
   dependencies {
       // BytePlus MediaAds SDK
       implementation libs.byteplus.mediaads
       
       // Google IMA SDK
       implementation libs.google.interactivemedia
   
       // others ...
   }
   ```
   

4. **啟用 Java 8 解糖**：Google IMA SDK 需要 Java 8 語言特性。在應用級 `build.gradle` 檔案中啟用核心庫解糖，以確保相容不同 Android 版本。

   ```Java
   android {
       compileOptions {
           isCoreLibraryDesugaringEnabled = true
       }
       
       // others ...
   }
   
   dependencies {
       coreLibraryDesugaring "com.android.tools:desugar_jdk_libs:2.1.5"
       
       // others ...
   }
   ```
   


<span id="d7bff433"></span>
## 快速開始

<span id="e2989d44"></span>
### 通用指南

MediaAds SDK 設計為播放器無關。但若未提供播放器，則預設使用內建 `TTVideoEngine`。為適配任意播放器，提供了 `AdPlaybackSession` 實體，用於包裝內容播放器和廣告播放器，並協調主內容中的廣告插入。

請按照以下步驟建立 `AdSchedule` 並構建 `AdPlaybackSession`。


1. 建立 `AdAppInfo`：使用 `AdAppInfo.Builder` 建立 `AdAppInfo` 物件，該物件包含日誌記錄和身份識別所需的應用後設資料。

   ```Java
   AdAppInfo.Builder appInfoBuilder = new AdAppInfo.Builder();
   appInfoBuilder.setAppId(BuildConfig.VOD_APP_ID);      // Set the application ID
   appInfoBuilder.setAppName(BuildConfig.VOD_APP_NAME);  // Set the application name
   appInfoBuilder.setAppChannel(BuildConfig.VOD_APP_CHANNEL); // Set the application channel
   AdAppInfo appInfo = appInfoBuilder.build();
   ```
   

2. 建立 `AdConfig`：使用 `AdConfig.Builder` 建立 `AdConfig` 物件，啟用預載入和預渲染等功能以最佳化廣告播放效能。

   ```Java
   AdConfig.Builder adConfigBuilder = new AdConfig.Builder();
   adConfigBuilder.setAppInfo(appInfo);                  // Associate the app info
   adConfigBuilder.setEnablePreloadVast(true);           // Enable VAST preloading for faster ad response
   adConfigBuilder.setEnablePreloadAdMediaFile(true);    // Enable ad media file preloading to reduce buffering
   adConfigBuilder.setEnablePreRenderAdPlayer(true);     // Enable ad player pre-rendering for smoother transitions
   AdConfig adConfig = adConfigBuilder.build();
   ```
   

3. 建立多 VAST `AdBreakItem` 列表：定義內容的廣告插播點。在本示例中，我們透過 VAST 標籤 URL 配置前貼片、中插和後貼片廣告。

   ```Java
   List<AdBreakItem> adBreaks = new ArrayList<AdBreakItem>();
   
   // Pre-roll ad
   AdBreakItem.Builder preBrBuilder = new AdBreakItem.Builder();
   preBrBuilder.setVastAdTagUrl(AdSources.prerollUrl);   // Set the VAST ad tag URL
   preBrBuilder.setTimeOffset(AdBreakItem.TIME_OFFSET_START); // Set the offset to start
   adBreaks.add(preBrBuilder.build());
   
   // Mid-roll ad
   AdBreakItem.Builder mid1BrBuilder = new AdBreakItem.Builder();
   mid1BrBuilder.setVastAdTagUrl(AdSources.midrollUrl);
   mid1BrBuilder.setTimeOffset("00:00:10.500");          // Set the offset to 10.5 seconds
   adBreaks.add(mid1BrBuilder.build());
   
   // Post-roll ad
   AdBreakItem.Builder postBrBuilder = new AdBreakItem.Builder();
   postBrBuilder.setVastAdTagUrl(AdSources.postrollUrl);
   postBrBuilder.setTimeOffset(AdBreakItem.TIME_OFFSET_END); // Set the offset to end
   adBreaks.add(postBrBuilder.build());
   ```
   

4. 建立 `AdSchedule`：將 `AdConfig` 和 `AdBreakItem` 列表合併為 `AdSchedule` 物件。該計劃定義了會話的完整廣告播放行為。

   ```Java
   AdSchedule.Builder adScheduleBuilder = new AdSchedule.Builder();
   adScheduleBuilder.setAdConfig(adConfig);
   adScheduleBuilder.setAdBreaks(adBreaks);
   AdSchedule adSchedule = adScheduleBuilder.build();
   ```
   

5. 建立 `AdPlaybackSession`：最後，建立 `AdPlaybackSession`，使用 `MediaAds` 單例。繫結到您的檢視、內容播放器和計劃，以開始管理播放。

   ```Java
   // Create a session instance
   AdPlaybackSession adPlaybackSession = MediaAds.instance().createAdSession(view.getContext());
   // Bind the ad container view where ads will be rendered
   adPlaybackSession.setAdViewContainer(view);
   // Set the ad schedule
   adPlaybackSession.setSchedule(adSchedule);
   // Bind the content player (e.g., videoEngine) to allow the SDK to control content playback
   adPlaybackSession.setContentPlayer(videoEngine);
   
   // Tip: You can programmatically skip the current ad using adPlaybackSession.skipAd()
   // if the ad is skippable (check with adPlaybackSession.isSkippable()).
   ```
   


<span id="84f33c81"></span>
### 與 VideoOne 整合

<span id="9d143f84"></span>
#### 修改 `PlaybackController`

`PlaybackController` 類負責管理內容播放器狀態和 UI 繫結。為支援廣告並保留 VideoOne 現有播放列表邏輯（如自動播放下一集），我們需要攔截播放事件。

建議建立子類 `AdsPlaybackController`，而非直接修改複雜的 `PlaybackController`。為實現繼承，需先重構 `PlaybackController`，以暴露關鍵控制點。

重構目標：


* **允許方法重寫**：將 `bindPlayer` 和 `unbindPlayer` 的可見性更改為 `protected`。

* **攔截播放控制**：拆分 `startPlayback` 和 `pausePlayback`，以暴露 `startPlayer` 和 `pausePlayer` 鉤子。這樣可以使子類將這些命令路由到 `AdPlaybackSession`，而不是直接路由到播放器。

* **為事件劫持做準備**：新增 `stopPlayer` 鉤子。這對於正確處理“完成”狀態至關重要——我們必須確保應用在內容和後貼片廣告都播放完畢之前，不會認為劇集已經結束。


請對您的 `PlaybackController` 類應用以下調整：

```Java
public class PlaybackController {
// Methods...

    // Swap private visibility with protected to enable overriding through inheritance
    protected private void bindPlayer(Player newPlayer) {
        // ...
    }

    // Swap private visibility with protected to enable overriding through inheritance
    protected private void unbindPlayer(boolean recycle) {
        // ...
    }

    // Split the player state switch statement from startPlayback to enable overriding
    // through inheritance
    private void startPlayback(boolean startWhenPrepared, @NonNull Player player, @NonNull VideoView videoView) {
        // Bind surface...
        
        startPlayer(startWhenPrepared, player, viewSource);
    }

    protected void startPlayer(boolean startWhenPrepared, @NonNull Player player, @NonNull MediaSource viewSource) {
        @Player.PlayerState final int playerState = player.getState();

        switch (playerState) {
            // Cases...
        }
    }
    
    // Split the player pause statement from pausePlayback to enable overriding
    // through inheritance
    public void pausePlayback() {
        Asserts.checkMainThread();

        final Player player = mPlayer;
        if (player != null) {
            L.d(this, "pausePlayback");

            if (player.isInPlaybackState()) {
                player.pause();
                pausePlayer();
            } else if (player.isPreparing()) {
                player.setStartWhenPrepared(false);
            }
        }
    }

    protected void pausePlayer() {
        mPlayer.pause();
    }

    // Add an empty stopPlayer method to enable overriding through inheritance
    public void stopPlayback() {
        Asserts.checkMainThread();

        final VideoView attachedView = mVideoView;
        final Player attachedPlayer = mPlayer;
        final MediaSource attachedSource = attachedSource(attachedView, attachedPlayer);

        if (attachedView != null) {
            attachedView.setReuseSurface(false);
        }

        if (mStartOnReadyCommand != null // startPlayback but surface not ready
                || attachedPlayer != null
        ) {
            L.d(this, "stopPlayback");

            mDispatcher.obtain(ActionStopPlayback.class, this).dispatch();

            stopPlayer();
            mStartOnReadyCommand = null;
            unbindPlayer(true);

            L.d(this, "stopPlayback", "end");
        }
    }

    protected void stopPlayer() {
    }
    
// Methods...
}
```


<span id="8f1b30ba"></span>
#### 實現 `AdsPlaybackController`

建立繼承自 `PlaybackController` 的 `AdsPlaybackController` 類。該類重寫播放器控制方法，將其重定向到 `AdPlaybackSession`。

該類的主要職責：


1. **攔截播放器事件**：用自定義的 `AdsPlayerListener` 替換原有的 `PlayerListener`，以管理內容與廣告之間的互動。

2. **延遲完成**：確保僅在整個會話（內容+廣告）完成時才分發 `PlayerEvent.State.COMPLETED` 事件，而不僅僅是內容完成時。

3. **管理會話生命週期**：建立、啟動、暫停和停止 `AdPlaybackSession`。

4. **計算中插廣告時間戳**：會話建立延遲到影片準備好且已知時長後進行，因為 Android 當前要求中插廣告使用絕對時間戳。


```Java
public class AdsPlaybackController extends PlaybackController {
    // AdsPlaybackController must at least hold an AdsPlayerListener and
    // an AdPlaybackSession
    private final AdsPlayerListener mAdsPlayerListener = new AdsPlayerListener(this);
    private AdPlaybackSession mSession = null;

    // Methods...

    // Call the original bindPlayer and then immediately replace the original event
    // listener with the AdsPlayerListener
    protected void bindPlayer(Player newPlayer) {
        super.bindPlayer(newPlayer);
        if (super.player() != null && newPlayer != null && !newPlayer.isReleased()) {
            super.player().addPlayerListener(mAdsPlayerListener);
            super.player().removePlayerListener(super.mPlayerListener); // Remove base listener to take over events
        }
    }

    // Remove the AdsPlayerListener and delete the current AdPlaybackSession
    protected void unbindPlayer(boolean recycle) {
        if (super.player() != null) {
            super.player().removePlayerListener(mAdsPlayerListener);
        }
        super.unbindPlayer(recycle);
        mSession = null;
    }

    // Prepare the player or start the AdPlaybackSession if it already exists
    protected void startPlayer(boolean startWhenPrepared, @NonNull Player player, @NonNull MediaSource viewSource) {
        player.setStartWhenPrepared(false); // Disable auto-play, let SDK schedule it

        if (mSession == null) {
            player.prepare(viewSource); // Prepare player first if session not ready
        } else {
            mSession.play(); // Start session (plays ad or content)
        }
    }

    // Pause the AdPlaybackSession
    protected void pausePlayer() {
        if (mSession != null) {
            mSession.pause();
        }
    }

    // Stop the AdPlaybackSession
    protected void stopPlayer() {
        if (mSession != null) {
            mSession.stop();
        }
    }
    
    // Methods...
    
    private AdPlaybackSession createAdPlaybackSession(VideoView view, long duration) {
        // Create AdPlaybackSession logic here (omitted for brevity)...
        // ...
        
        session.addListener( (@NonNull AdPlaybackSession s, @NonNull AdPlayEvent e) -> {
                // Other logic...

                // Dispatch the original PlayerEvent.State.COMPLETED event only when the
                // AdPlaybackSession has completed (content + all ads)
                if (e.type == AdPlayEvent.Type.PLAY_COMPLETED) {
                    mDispatcher.obtain(StateCompleted.class, super.player()).dispatch();
                }
            });

        return session;
    }
    
    private static final class AdsPlayerListener implements EventListener {

        private final WeakReference<AdsPlaybackController> controllerRef;

        AdsPlayerListener(AdsPlaybackController controller) {
            controllerRef = new WeakReference<>(controller);
        }

        public void onEvent(Event event) {
            final AdsPlaybackController controller = controllerRef.get();

            // Create the AdPlaybackSession once the player is prepared
            if (controller != null) {
                if (event.code() == PlayerEvent.State.PREPARED) {
                    // Create session when content duration is known (for mid-rolls)
                    if (controller.mSession == null) {
                        long duration = controller.player().getDuration();
                        controller.mSession = controller.createAdPlaybackSession(controller.videoView(), duration);

                        VideoContentPlayer.Factory f = new VideoContentPlayer.Factory();
                        ContentPlayer cp = f.create(controller.player());
                        controller.mSession.setContentPlayer(cp);
                        controller.mSession.setSchedule(controller.creatAdSchedule(duration));
                    }
                    controller.mSession.play();
                }

                // Dispatch all events except for PlayerEvent.State.COMPLETED
                // COMPLETED is handled by the session listener above
                final Dispatcher dispatcher = controller.mDispatcher;
                if (dispatcher != null && event.code() != PlayerEvent.State.COMPLETED) {
                    dispatcher.dispatchEvent(event);
                }
            }
        }
    }
}
```


<span id="d4bf3c62"></span>
#### 實現 `VideoContentPlayer`

MediaAds SDK 中的 `ContentPlayer` 介面使 `AdPlaybackSession` 能夠控制任何底層播放器。您需要實現一個介面卡類 `VideoContentPlayer`，它包裝您的具體播放器（如 `TTVideoEngine`），並實現 `ContentPlayer` 介面。

```Java
public class VideoContentPlayer implements ContentPlayer {
    // Member variables and other methods...

    public static class Factory implements ContentPlayer.Factory {

        @Override
        public ContentPlayer create(Object player) {
            // Create and return VideoContentPlayer...
        }
    }

    private static final class PlayerListener implements EventListener {
        @Override
        public void onEvent(Event event) {
            // Event callback logic...
        }
    }

    public VideoContentPlayer(Player player) {
        // Constructor...
    }

    @Override
    public void setListener(Listener listener) {
        // Set player event listener...
    }

    @Override
    public void play() {
        // Start player...
        // e.g., mRealPlayer.play();
    }

    @Override
    public void pause() {
        // Pause player...
        // e.g., mRealPlayer.pause();
    }

    @Override
    public void release() {
        // Release player...
    }

    @Override
    public long getCurrentPosition() {
        // Return current player position...
    }

    @Override
    public long getDuration() {
        // Return content duration...
    }

    @Override
    public boolean isCompleted() {
        // Return whether the player has finished...
    }

    @Override
    public boolean isLooping() {
        // Return whether the player is looping...
    }

    @Override
    public void recordLog(String log) {
        // Record logs...
    }
}
```
