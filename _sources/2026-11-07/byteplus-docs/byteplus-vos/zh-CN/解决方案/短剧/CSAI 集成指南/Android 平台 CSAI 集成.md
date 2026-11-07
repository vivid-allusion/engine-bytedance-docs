---
title: "Android 平台 CSAI 集成"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/csai-integration-for-android-zh-CN"
---

本指南介绍如何将 BytePlus MediaAds SDK 和 Google IMA SDK 集成到基于 VideoOne 的短剧 Android 应用中。

<span id="10c2b5c1"></span>
## 前置条件

在开始之前，请确保您已具备以下条件：


1. **已有集成**：您已集成 VideoOne 短剧解决方案（详见[短剧视频 - Android 集成](https://docs.byteplus.com/docs/byteplus-vos/short-drama-videos-android-integration-zh-CN)）。

2. **Google Play 服务**：您的应用必须包含 Google Play 服务，以支持 Google IMA SDK。

3. **广告标签 URL**：您需要一个有效的 VAST/VMAP 广告标签 URL。

   * 测试时：您可以使用 [Google 的 VAST 标签示例](https://developers.google.com/interactive-media-ads/docs/sdks/html5/client-side/tags)。

   * 生产环境：请从您的广告服务器（如 Google Ad Manager）获取广告标签 URL。

4. **最低 SDK 要求**：

   * `minSdkVersion`：24 或更高（Google IMA 必需）。

   * `Android Gradle 插件（AGP）`：8.13.0 或更高（Google IMA 必需）。


<span id="64f0e2a3"></span>
## SDK 集成

请按照以下步骤将 MediaAds SDK 集成到您的 Android 项目中。


1. **配置应用属性**：将您的应用渠道、ID 和名称添加到项目根目录下的 `gradle.properties` 文件中。这些属性将被 SDK 用于初始化和分析。

   ```Bash
   VOD_APP_CHANNEL=overseas
   VOD_APP_ID=522211
   VOD_APP_NAME=VideoOne
   
   # others ...
   ```
   

2. **添加依赖版本**：打开 `libs.versions.toml` 文件（版本库），并定义 MediaAds SDK 和 Google IMA SDK 的版本。

   ```Bash
   interactivemedia = "3.38.0"
   mediaads = "2.0.0"
   
   # others ...
   
   google-interactivemedia = { module = "com.google.ads.interactivemedia.v3:interactivemedia", version.ref = "interactivemedia" }
   byteplus-mediaads = { module = "com.byteplus.mediaplus:mediaads", version.ref = "mediaads" }
   
   # others ...
   ```
   

3. **配置库模块**：在库级 `build.gradle` 文件中，导入 SDK 依赖，并将应用属性注入到 `BuildConfig` 类中。这样您的代码即可在运行时访问这些值。

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
   

4. **启用 Java 8 解糖**：Google IMA SDK 需要 Java 8 语言特性。在应用级 `build.gradle` 文件中启用核心库解糖，以确保兼容不同 Android 版本。

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
## 快速开始

<span id="e2989d44"></span>
### 通用指南

MediaAds SDK 设计为播放器无关。但若未提供播放器，则默认使用内置 `TTVideoEngine`。为适配任意播放器，提供了 `AdPlaybackSession` 实体，用于包装内容播放器和广告播放器，并协调主内容中的广告插入。

请按照以下步骤创建 `AdSchedule` 并构建 `AdPlaybackSession`。


1. 创建 `AdAppInfo`：使用 `AdAppInfo.Builder` 创建 `AdAppInfo` 对象，该对象包含日志记录和身份识别所需的应用元数据。

   ```Java
   AdAppInfo.Builder appInfoBuilder = new AdAppInfo.Builder();
   appInfoBuilder.setAppId(BuildConfig.VOD_APP_ID);      // Set the application ID
   appInfoBuilder.setAppName(BuildConfig.VOD_APP_NAME);  // Set the application name
   appInfoBuilder.setAppChannel(BuildConfig.VOD_APP_CHANNEL); // Set the application channel
   AdAppInfo appInfo = appInfoBuilder.build();
   ```
   

2. 创建 `AdConfig`：使用 `AdConfig.Builder` 创建 `AdConfig` 对象，启用预加载和预渲染等功能以优化广告播放性能。

   ```Java
   AdConfig.Builder adConfigBuilder = new AdConfig.Builder();
   adConfigBuilder.setAppInfo(appInfo);                  // Associate the app info
   adConfigBuilder.setEnablePreloadVast(true);           // Enable VAST preloading for faster ad response
   adConfigBuilder.setEnablePreloadAdMediaFile(true);    // Enable ad media file preloading to reduce buffering
   adConfigBuilder.setEnablePreRenderAdPlayer(true);     // Enable ad player pre-rendering for smoother transitions
   AdConfig adConfig = adConfigBuilder.build();
   ```
   

3. 创建多 VAST `AdBreakItem` 列表：定义内容的广告插播点。在本示例中，我们通过 VAST 标签 URL 配置前贴片、中插和后贴片广告。

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
   

4. 创建 `AdSchedule`：将 `AdConfig` 和 `AdBreakItem` 列表合并为 `AdSchedule` 对象。该计划定义了会话的完整广告播放行为。

   ```Java
   AdSchedule.Builder adScheduleBuilder = new AdSchedule.Builder();
   adScheduleBuilder.setAdConfig(adConfig);
   adScheduleBuilder.setAdBreaks(adBreaks);
   AdSchedule adSchedule = adScheduleBuilder.build();
   ```
   

5. 创建 `AdPlaybackSession`：最后，创建 `AdPlaybackSession`，使用 `MediaAds` 单例。绑定到您的视图、内容播放器和计划，以开始管理播放。

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
### 与 VideoOne 集成

<span id="9d143f84"></span>
#### 修改 `PlaybackController`

`PlaybackController` 类负责管理内容播放器状态和 UI 绑定。为支持广告并保留 VideoOne 现有播放列表逻辑（如自动播放下一集），我们需要拦截播放事件。

建议创建子类 `AdsPlaybackController`，而非直接修改复杂的 `PlaybackController`。为实现继承，需先重构 `PlaybackController`，以暴露关键控制点。

重构目标：


* **允许方法重写**：将 `bindPlayer` 和 `unbindPlayer` 的可见性更改为 `protected`。

* **拦截播放控制**：拆分 `startPlayback` 和 `pausePlayback`，以暴露 `startPlayer` 和 `pausePlayer` 钩子。这样可以使子类将这些命令路由到 `AdPlaybackSession`，而不是直接路由到播放器。

* **为事件劫持做准备**：添加 `stopPlayer` 钩子。这对于正确处理“完成”状态至关重要——我们必须确保应用在内容和后贴片广告都播放完毕之前，不会认为剧集已经结束。


请对您的 `PlaybackController` 类应用以下调整：

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
#### 实现 `AdsPlaybackController`

创建继承自 `PlaybackController` 的 `AdsPlaybackController` 类。该类重写播放器控制方法，将其重定向到 `AdPlaybackSession`。

该类的主要职责：


1. **拦截播放器事件**：用自定义的 `AdsPlayerListener` 替换原有的 `PlayerListener`，以管理内容与广告之间的交互。

2. **延迟完成**：确保仅在整个会话（内容+广告）完成时才分发 `PlayerEvent.State.COMPLETED` 事件，而不仅仅是内容完成时。

3. **管理会话生命周期**：创建、启动、暂停和停止 `AdPlaybackSession`。

4. **计算中插广告时间戳**：会话创建延迟到视频准备好且已知时长后进行，因为 Android 当前要求中插广告使用绝对时间戳。


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
#### 实现 `VideoContentPlayer`

MediaAds SDK 中的 `ContentPlayer` 接口使 `AdPlaybackSession` 能够控制任何底层播放器。您需要实现一个适配器类 `VideoContentPlayer`，它包装您的具体播放器（如 `TTVideoEngine`），并实现 `ContentPlayer` 接口。

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
