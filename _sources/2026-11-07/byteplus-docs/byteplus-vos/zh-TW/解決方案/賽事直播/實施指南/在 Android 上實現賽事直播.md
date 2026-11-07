---
title: "在 Android 上實現賽事直播"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/docs-implementing-live-sport-streaming-for-android-zh-TW"
---

本指南介紹如何使用 BytePlus MediaLive SDK 在 Android 上實現賽事直播觀看體驗。您將學習如何初始化直播播放器、透過低延遲協議拉流、切換機位和畫質，以及在播放之上疊加互動功能。

<span id="lsa-env"></span>
## 環境要求


* Android Studio Arctic Fox 或更高版本。我們建議使用最新版本的 Android Studio 以獲得最佳效能。

* 一台執行 Android 6.0 或更高版本的真機行動裝置。

* 確保您使用的 CPU 架構為 armv7 或 arm64。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">暫不支援模擬器。</div>


<span id="lsa-prereq"></span>
## 前提條件


* 一個已啟用 [BytePlus MediaLive](https://console.byteplus.com/live) 的有效 [BytePlus 帳戶](http://console.byteplus.com/)。

* 完成 [直播的基礎設定](https://docs.byteplus.com/en/byteplus-media-live/docs/getting-started)：

   * 取得 BytePlus MediaLive SDK 授權。

      * 有關如何取得授權的詳細說明，請參見 [存取您的 SDK 授權](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management#accessing-your-sdk-license)。

      * 要瞭解更多如何根據您的需求選擇合適的授權類型，請參考 [SDK 簡介](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-introduction)。


<span id="lsa-version"></span>
## 版本要求


* 要使用 **直播拉流** 功能，您必須使用 BytePlus MediaLive SDK。請記得在 [用戶端 SDK 元件](https://docs.byteplus.com/en/docs/byteplus-vos/docs-version-combination) 頁面選擇正確的 SDK。


<span id="lsa-integrate"></span>
## 整合 SDK

<span id="lsa-maven"></span>
### 步驟 1: 新增 maven 倉庫

開啟位於專案根目錄下的專案 `build.gradle` 檔案，在 `repositories` 程式碼區塊中新增倉庫地址，如下所示：

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
```


<span id="lsa-dep"></span>
### 步驟 2: 整合 SDK

要整合 SDK，請將以下相依項新增到模組的 `build.gradle` 檔案中：

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">要取得最新的版本號，請參見 <a href="https://docs.byteplus.com/en/docs/byteplus-vos/docs-version-combination">用戶端 SDK 元件</a>。</div>


```Groovy
dependencies {
    def ttsdkVersion = "1.50.300.1"
    // BytePlus MediaLive SDK dependencies
    implementation "com.bytedanceapi:ttsdk-ttlivepull_premium:$ttsdkVersion"
    implementation 'commons-net:commons-net:3.9.0'
    implementation 'com.bytedance.applog:RangersAppLog-Lite-global:6.14.3'
}
```


<span id="lsa-perm"></span>
### 步驟 3: 宣告應用權限

在 `AndroidManifest.xml` 中宣告 SDK 所需的權限。

```XML
<uses-permission android:name="android.permission.INTERNET" /> 
```


<span id="lsa-impl"></span>
## 實現

本節介紹 Android Demo 如何實現賽事直播體驗。Demo 程式碼組織在以下模組中：

```text
solutions/media-live/live-sport
```


該模組包含三個面向使用者的體驗：


* **Live Watch**：播放賽事直播流，支援機位切換、播放設定、評論、禮物、點讚和全螢幕控制。

* **Live Comparison**：並排對比延遲、影像增強以及 H.265/H.264 降本流。

* **Custom Stream URL**：允許觀眾輸入 FLV、RTM、HLS 或 RTMP 拉流 URL 並預覽播放。


<span id="lsa-enter"></span>
### 步驟 1: 進入賽事直播場景

賽事直播入口註冊在 VideoOne 首頁場景列表中。當觀眾開啟賽事直播卡片時，應用會初始化直播 SDK 環境並啟動賽事直播首頁。

關鍵程式碼：


* `app/src/main/kotlin/com/videoone/app/protocol/SceneEntry.kt`

* `solutions/media-live/live-sport/src/main/kotlin/com/videoone/app/protocol/LiveSportEntry.kt`

* `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/entry/LiveSportHomeActivity.kt`


<span id="lsa-init"></span>
### 步驟 2: 初始化 TTSDK 和授權

在播放開始前，初始化 TTSDK 並載入有效的授權。Demo 將此邏輯集中在 `SportLiveEnv.ensureInitialized()` 中，該方法可安全地多次呼叫。

關鍵程式碼：


* `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/player/SportLiveEnv.kt`

* `solutions/media-live/live-sport/gradle.properties`


```Kotlin
Env.init(
    Config.Builder()
        .setApplicationContext(appContext)
        .setAppID(BuildConfig.LIVE_TTSDK_APP_ID)
        .setAppName(BuildConfig.LIVE_TTSDK_APP_NAME)
        .setAppChannel(BuildConfig.LIVE_TTSDK_APP_CHANNEL)
        .setLicenseUri(BuildConfig.LIVE_TTSDK_LICENSE_URI)
        .setLicenseCallback(SportLicenseCallback())
        .build()
)
```


<span id="lsa-channel"></span>
### 步驟 3: 準備頻道資料

預設的賽事頻道是資料驅動的。每個頻道都可以宣告機位 ID、拉流協議策略、FLV 流檔位、位元速率資訊、低延遲 FLV 偏好以及 ABR 偏好。

關鍵程式碼：


* `solutions/media-live/live-sport/src/main/assets/live_sport_channels.json`

* `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/data/SportChannelRepo.kt`

* `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/data/SportChannel.kt`

* `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/player/SportPlayerModels.kt`


`SportChannelRepo` 載入 JSON 頻道列表，`SportChannel.toPlayerConfig()` 將選定的頻道轉換為播放器層使用的 `SportPlayerConfig`。

```Kotlin
val config = channel.toPlayerConfig(
    protocol = protocolOption,
    abrAuto = abrOn,
    pinnedResolution = pinnedResolution,
    enableSR = srEnabled,
    enableSharpen = sharpenEnabled,
)
```


<span id="lsa-player"></span>
### 步驟 4: 建立直播播放器

觀看頁面使用 `SportLivePlayer` 作為 `VeLivePlayer` 的封裝。該封裝處理播放器生命週期、`TextureView` 繫結、流資料設定、低延遲 FLV、ABR、超解析度、銳化、播放事件以及播放統計。

關鍵程式碼：


* `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/watch/LiveWatchActivity.kt`

* `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/player/SportLivePlayer.kt`


```Kotlin
player = SportLivePlayer(this).apply {
    setListener(playerListener)
    bindTextureView(playerTexture)
}
```


當播放開始時，該封裝會建立一個 `VideoLiveManager`，套用 `VeLivePlayerConfiguration`，設定流資料，附加渲染表面，並呼叫 `play()`。

對於預設的賽事頻道，Demo 使用 `setPlayStreamData()`，使一個頻道可以承載多個 FLV 檔位，用於畫質選擇和 ABR。

對於使用者輸入的自訂流 URL，Demo 使用 `setPlayUrl()`，並讓 SDK 從 URL 中偵測協議。

<span id="lsa-start"></span>
### 步驟 5: 開始播放

`LiveWatchActivity` 在頁面設定期間準備初始頻道，並在頁面進入前台時開始播放。

關鍵程式碼：


* `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/watch/LiveWatchActivity.kt`


<span id="lsa-switch"></span>
### 步驟 6: 切換機位、協議和畫質

機位切換由觀看頁面處理。當觀眾選擇另一個機位時，頁面會準備一個新的頻道設定，並以選定的頻道重新開始播放。

關鍵程式碼：


* `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/watch/LiveWatchActivity.kt`

* `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/watch/camera/CameraListAdapter.kt`


播放設定在設定面板中暫存。協議或 ABR 的變更會使用新的 `SportPlayerConfig` 重建播放。超解析度和銳化是執行時開關，無需重建播放器。

關鍵程式碼：


* `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/watch/panel/PlayerSettingsPanel.kt`

* `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/watch/LiveWatchActivity.kt`

* `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/player/SportLivePlayer.kt`


畫質選擇基於選定頻道宣告的 FLV 檔位。啟用 ABR 時，播放器可以在可用檔位之間自適應。停用 ABR 時，在重建播放前會將選定的解析度固定在 `SportPlayerConfig` 中。

<span id="lsa-interact"></span>
### 步驟 7: 新增全螢幕和互動功能

互動功能作為疊加在直播播放之上的 UI 層實現。

關鍵程式碼：


* 評論：`solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/watch/comment`

* 禮物：`solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/watch/gift`

* 點讚：`solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/watch/like`

* 全螢幕控制：`solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/fullscreen`

* 觀看頁面編排：`solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/watch/LiveWatchActivity.kt`


在全螢幕模式下，`LandscapeController` 會將現有的 `TextureView` 移入橫螢幕浮層。這樣可以保持同一個播放器實例，並避免在進入或退出全螢幕時重新開始播放。

<span id="lsa-compare"></span>
### 步驟 8: 新增對比和自訂流體驗

對比頁面使用獨立的播放器插槽，以並排對比多種播放體驗。只有處於啟用狀態的對比標籤頁會保持其播放器執行。

關鍵程式碼：


* `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/compare/LiveCompareActivity.kt`

* `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/compare/CompareSlot.kt`

* `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/compare/CompareConfig.kt`

* `solutions/media-live/live-sport/src/main/assets/live_sport_compare.json`


自訂流頁面會校驗觀眾輸入的 URL，並以自訂流模式開啟觀看頁面。

關鍵程式碼：


* `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/stream/LiveStreamAddressActivity.kt`

* `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/stream/CustomStreamUrlParser.kt`

* `solutions/media-live/live-sport/src/main/kotlin/com/byteplus/live/sport/stream/CustomStreamSettingsBinder.kt`


<span id="lsa-code"></span>
## 範例程式碼

請參考 Demo 原始碼，將此功能整合到您的應用中。


* Android：[live-sport](https://github.com/byteplus-sdk/VideoOneSolutions/tree/main/Client/Android/solutions/media-live/live-sport)
