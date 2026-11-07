---
title: "在 Android 上實現媒體上下滑動"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/Implementing-media-up-and-down-swiping-for-Android-zh-TW"
---

為了在您的 Android 應用中建立流暢可滑動的影片內容流，本指南將介紹如何實現影片點播（VOD）和直播流播放。您將學習關鍵最佳化策略，例如針對 VOD 的預載入和預渲染，以及針對直播內容的預流，以確保使用者體驗的無縫流暢。

<span id="a3521dd9"></span>
# 環境要求


* Android Studio Arctic Fox 或更高版本。我們建議使用最新版本的 Android Studio，以獲得最佳效能。

* 一臺執行 Android 5.0 或更高版本的實體移動裝置。

* 請確保您使用的 CPU 架構為 armv7 或 arm64。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">暫不支援模擬器。</div>


<span id="76cb7082"></span>
# 前置條件


* 一個有效的[BytePlus 賬號](http://console.byteplus.com/)，並已啟用[BytePlus VOD](https://console.byteplus.com/vodpaas)和[BytePlus MediaLive](https://console.byteplus.com/live)。

* 在[SDK 管理](https://console.byteplus.com/vodpaas/sdk/)頁面的[BytePlus VOD 控制檯](https://docs.byteplus.com/en/byteplus-vod/docs/sdk-management)中完成以下操作：

   * 建立應用並獲取其應用 ID 和名稱。

   * 為應用註冊，併購買及下載用於 Player 的許可證。

   * 您需要高階版 SDK 和許可證，以支援預載入與預渲染。

      * [Player SDK 功能](https://docs.byteplus.com/docs/byteplus-vod/docs-player-features)

      * [Android Player SDK：自定義預載入](https://docs.byteplus.com/docs/byteplus-vod/docs-custom-preloading-android)

* 完成[直播流基礎設定](https://docs.byteplus.com/en/byteplus-media-live/docs/getting-started)。

* 獲取 BytePlus MediaLive SDK 許可證。

   * 有關獲取許可證的詳細說明，請參見[訪問您的 SDK 許可證](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management#accessing-your-sdk-license)。

   * 如需瞭解如何選擇適合您需求的許可證型別，請參考[SDK 介紹](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-introduction)。


<span id="1c99b955"></span>
# 版本要求


* 要訪問**影片播放**和直播流**功能**，必須使用 BytePlus VOD 和 BytePlus MediaLive SDK。請記得在[客戶端 SDK 元件](https://docs.byteplus.com/docs/byteplus-vos/docs-version-combination-zh-TW)頁面選擇正確的 SDK。


<span id="f86cb645"></span>
# 整合 SDK

<span id="f5922109"></span>
## 步驟 1：新增 maven 倉庫

開啟專案根目錄下的 `build.gradle` 檔案，並在 `repositories` 程式碼塊中新增倉庫地址，如下所示：

```Groovy
allprojects { 
    repositories { 
        google() 
        mavenCentral() 
        // BytePlus SDK maven repository
        maven { url 'https://artifact.byteplus.com/repository/public/' }
        maven { url 'https://artifact.bytedance.com/repository/Volcengine/' }
    } 
} 
 
// BytePlus VOD SDK maven repository
apply from: 'https://ve-vos.volccdn.com/script/vevos-repo-base.gradle'
```


<span id="4448e58f"></span>
## 步驟 2：整合 SDK

要整合 SDK，請將以下依賴項新增到您的模組 `build.gradle` 檔案中：

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">要獲取最新版本號，請參見<a href="https://docs.byteplus.com/docs/byteplus-vos/docs-version-combination-zh-TW">客戶端 SDK 元件</a>。</div>


```Groovy
dependencies {
    def ttsdkVersion = "1.43.300.3"
    // BytePlus VOD SDK dependencies
    implementation "com.bytedanceapi:ttsdk-player_premium:$ttsdkVersion"
    
    // BytePlus MediaLive SDK dependencies
    implementation "com.bytedanceapi:ttsdk-ttlivepull_rtc:$ttsdkVersion"
    implementation 'commons-net:commons-net:3.9.0'
    
    implementation 'com.bytedance.applog:RangersAppLog-Lite-global:6.14.3'
}
```


<span id="38b05b45"></span>
## 步驟 3：宣告應用許可權

在 `AndroidManifest.xml` 中宣告 SDK 所需的許可權。

```XML
<uses-permission android:name="android.permission.INTERNET" /> 
```


<span id="06ca11af"></span>
# 實現

<span id="1690b16f"></span>
## 短影片最佳化策略

<span id="9a37c9aa"></span>
### 步驟 1：實現影片播放

如需瞭解如何使用 BytePlus VOD 播放器進行影片播放，請參見[在 Android 上實現影片播放](https://docs.byteplus.com/docs/byteplus-vos/docs-implementing-video-playback-edit-for-android-zh-TW)。

<span id="c8e4d2c6"></span>
### 步驟 2：啟用 BytePlus VOD 播放器的預載入與預渲染策略

呼叫[TTVideoEngine.enableEngineStrategy(int, int)](https://docs.byteplus.com/en/docs/byteplus-vod/docs-android-player-sdk-api-details#enableenginestrategy)以啟用預載入和預渲染策略

```Java
public static void setSceneStrategyEnabled(){
        TTVideoEngine.enableEngineStrategy(
                StrategyManager.STRATEGY_TYPE_PRELOAD,
                StrategyManager.STRATEGY_SCENE_SMALL_VIDEO
        );
        TTVideoEngine.enableEngineStrategy(
                StrategyManager.STRATEGY_TYPE_PRE_RENDER,
                StrategyManager.STRATEGY_SCENE_SMALL_VIDEO
        );
}
```


<span id="fe5ebf44"></span>
### 步驟 3：設定預載入源

在合適的時機（如獲取到影片播放列表後），將播放列表設定為預載入源。


1. 首次載入播放源資料或重新整理頁面獲取新資料時，呼叫[TTVideoEngine.setStrategySources(List](https://docs.byteplus.com/en/docs/byteplus-vod/docs-android-player-sdk-api-details#TTVideoEngine-setstrategysources)。

2. 在載入更多資料的場景下，呼叫[TTVideoEngine.addStrategySources(List)](https://docs.byteplus.com/en/docs/byteplus-vod/docs-android-player-sdk-api-details#TTVideoEngine-addStrategySources)。

> 在該場景下，播放列表包含 VOD 和直播流媒體，因此設定預載入源時，務必排除直播流媒體。否則可能導致意外問題。


根據所提供的播放列表，BytePlus VOD SDK 會根據當前播放狀態自動管理預載入的時機和配置，例如併發預載入數量和資料大小。

```Java
// Set preload sources
if (page == 0) {
    TTVideoEngine.setStrategySources(items.filterMediaSource());
    // ... more codes here
} else { // append items
    TTVideoEngine.addStrategySources(items.filterMediaSource());
    // ... more codes here
}
```


<span id="dacb2db7"></span>
### 步驟 4：封面顯示與預渲染

啟用預渲染後，SDK 會根據您提供的播放列表提前建立播放器，並在播放當前影片時，對播放列表中的下一個影片進行解碼和渲染。

在滾動影片流場景下，當下一個影片即將可見時，我們會載入該影片的封面圖片。如果此時影片已被預渲染，我們將不再載入封面圖片，而是直接使用影片的第一幀作為封面。

```Java
// using the prerendered player.
final TTVideoEngine player = TTVideoEngine.getPreRenderEngine(mediaSource.getMediaId());

if (player != null && player != StrategyManager.instance().getPlayEngine()) {
    // call forceDraw to prerender
    player.setSurface(surface);
    player.forceDraw();
} else {
    // prerender not ready, using image cover
    showVideoCover();
}
```


<span id="8978e0b9"></span>
### 步驟 5：播放影片

播放下一個影片時，如果預渲染已完成且有可用的預渲染播放器，則使用該播放器。否則，建立一個新的播放器。

```Java
TTVideoEngine player = TTVideoEngine.getPreRenderEngine(mediaSource.getMediaId());
if (player == null) {
    player = create(mContext, mediaSource);
}
```


<span id="d6d50092"></span>
## 直播流最佳化策略

<span id="e32ad1e1"></span>
### 步驟 1：初始化 SDK

使用以下程式碼初始化 SDK：

```Java
// Initialize the environment.
   Env.init(new Config.Builder()
   .setApplicationContext(sApplicationContext)
   .setAppID("Your App ID")
   .setAppName("Your application name")
   .setAppVersion(BuildConfig.VERSION_NAME) // A valid version number should contain two or more separators, such as "1.3.2".
   .setAppChannel("Your app channel")
   .setLicenseUri("Your license URI")
   .setLicenseCallback(mLicenseCallback) // Set the license callbacks.
   .build());

// Enable logcat. It is recommended to enable logcat during development and disable logcat when compiling the release APK.
// LicenseManager.turnOnLogcat(true);

// License callbacks.
LicenseManager.Callback mLicenseCallback =new LicenseManager.Callback() {
        @Override
        public void onLicenseLoadSuccess(@NonNull String licenseUri, @NonNull String licenseId) {
            licenseID = licenseId; // License ID, through which you can get the license information.
        }

        @Override
        public void onLicenseLoadError(@NonNull String licenseUri, @NonNull Exception e, boolean retryAble) {
           
        }

        @Override
        public void onLicenseLoadRetry(@NonNull String licenseUri) {
           
        }

        @Override
        public void onLicenseUpdateSuccess(@NonNull String licenseUri, @NonNull String licenseId) {
          licenseID = licenseId;
        }

        @Override
        public void onLicenseUpdateError(@NonNull String licenseUri, @NonNull Exception e, boolean retryAble) {
           
        }

        @Override
        public void onLicenseUpdateRetry(@NonNull String licenseUri) {
          
        }
    };
    
// Get the license information.
License license = LicenseManager.getInstance().getLicense(licenseID); // You can get the license ID through mLicenseCallback.
if (license != null) {
    StringBuilder builder = new StringBuilder();
    builder.append("License id:" + license.getId()).append("\n")
           .append("License package:" + license.getPackageName()).append("\n")
           .append("License test:" + license.getType()).append("\n")
           .append("License version:" + license.getVersion()).append("\n");

    if (license.getModules() != null) {
        String names = "";
        for (License.Module module : license.getModules()) {
            names = "module name:" + module.getName() + ", start time:" +
            TimeUtil.format(module.getStartTime(), Times.YYYY_MM_DD_KK_MM_SS)
                    + ", expire time:" + TimeUtil.format(module.getExpireTime(), Times.YYYY_MM_DD_KK_MM_SS) + "\n";
            builder.append("License modules:" + names);
        }
    }
 }
```


<span id="ff105711"></span>
### 步驟 2：初始化播放器

```Java
// Create a player
VeLivePlayer player = new VideoLiveManager(Env.getApplicationContext());

// Set the player observer
player.setObserver(mLivePlayerObserver)；

// Configure the player
VeLivePlayerConfiguration config = new VeLivePlayerConfiguration();
config.enableStatisticsCallback = true;
config.enableLiveDNS = true;
player.setConfig(config);
```


<span id="e8b8a7da"></span>
### 步驟 3：預載入流

當使用者開始滑動時，將流靜音，滑動完成後取消靜音。

```Java
@Override
public void onPositionVisibilityChanged(int oldPosition, int newPosition) {
    super.onPositionVisibilityChanged(oldPosition, newPosition);

    LiveFeedHolder holder = getHolder(newPosition);
    LiveFeedItem item = (LiveFeedItem) getItem(newPosition);

    VideoLiveManager player = holder.getPlayer();
    if (player == null) {
        player = createLivePlayer(context, item.getRoomId());
        holder.bindPlayer(player);
    }

    player.setPlayUrl(item.getLiveUrl());
    player.setMute(true);
    player.play();
}
```


<span id="32c6f252"></span>
### 步驟 4：取消靜音

當前檢視顯示時，取消流的靜音狀態。

```Java
@Override
public void onPageSelected(int position) {
    super.onPageSelected(position);

    LiveFeedHolder holder = getHolder(position);
    LiveFeedItem item = (LiveFeedItem) getItem(position);

    VideoLiveManager player = holder.getPlayer();
    if (player == null) {
        player = createLivePlayer(context, item.getRoomId());
        holder.bindPlayer(player);
    }

    player.setPlayUrl(item.getLiveUrl());
    player.setMute(false);
    player.play();
}
```


<span id="262dad51"></span>
### 步驟 5：重置播放器狀態

噹噹前影片滑出檢視時，重置播放狀態並停止流。

```Java
@Override
public void onPageSelected(int position) {
    super.onPageSelected(position);
    
    if (lastHolder != null) {
        VideoLiveManager player = lastHolder.getPlayer();
        if (player != null) {
            player.stop();
        }
    }

    // more codes here
}
```
