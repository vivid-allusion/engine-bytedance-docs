---
title: "Flutter 播放器 SDK：進階功能"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/player-sdk-for-flutter-advanced-features-zh-TW"
---

為提升應用程式中的觀看體驗，本主題詳細介紹如何實現 Flutter 播放器 SDK 的進階功能。您可根據實際業務需求，按需實現複雜功能。

<span id="dd785362"></span>
## 前置條件


* 您已整合基本功能。如需更多資訊，請參閱[Flutter 用 Player SDK：基本功能](https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-basic-features-zh-TW)。

* 若需使用 H.265 硬體與軟體解碼功能，請確保您使用的是高級或試用授權。

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">試用授權僅供專案測試使用，無法續期。試用授權過期將導致驗證失敗，服務將中斷。在專案正式上線前，請升級為正式授權。如需更多資訊，請參閱<a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management-zh-TW#777c7de7">將試用授權升級為基礎版或高級版授權</a>。   </div>
   

<span id="c955251c"></span>
## 多路串流配置

若需使用主備串流及自適應碼率（ABR）功能，必須呼叫此方法為播放器配置多路串流。

```Dart
Future<void> setPlayStreamData(VeLivePlayerStreamData streamData);
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">如需型別定義，請參閱<a href="https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-type-definitions-zh-TW#dfb9d282">VeLivePlayerStreamData</a>。</div>


<span id="97511097"></span>
## 主備串流使用

主備串流功能為直播提供災難恢復能力。透過配置主串流與備串流，播放器可在其中一條串流故障時自動切換。例如，若主串流故障，播放器將切換至備串流。您可使用來自同一或不同服務提供商的串流地址。

<span id="fc2a7ac7"></span>
### 整合準備

取得主串流與備串流地址。若使用 BytePlus MediaLive 服務，可於 BytePlus MediaLive 控制台透過[地址生成器](https://docs.byteplus.com/en/byteplus-media-live/docs/address-generator)產生主串流與備串流地址。

<span id="83e07645"></span>
### 整合步驟


1. 配置主串流與備串流地址以進行播放。範例程式碼如下。

   ```Java
   // Set the primary stream address.
   VeLivePlayerStream mainStream = VeLivePlayerStream(url: 'https://pull.example.com/live/主.flv');
   mainStream.format = VeLivePlayerFormat.flv;
   mainStream.resolution = VeLivePlayerResolution.origin;
   mainStream.type = VeLivePlayerStreamType.main;
   
   // Set the backup stream address.
   VeLivePlayerStream backupStream = VeLivePlayerStream(url: 'https://pull.example.com/live/备.flv');
   backupStream.format = VeLivePlayerFormat.flv;
   backupStream.resolution = VeLivePlayerResolution.origin;
   backupStream.type = VeLivePlayerStreamType.backup;
   
   // Create the playback source.
   VeLivePlayerStreamData streamData = VeLivePlayerStreamData();
   
   // Enable primary and backup stream switching.
   streamData.enableMainBackupSwitch = true;
   
   // Add the primary stream.
   streamData.mainStream = [mainStream];
   // Add the backup stream.
   streamData.backupStream = [backupStream];
   
   // Configure the playback source.
   manager.setPlayStreamData(streamData);
   
   // Start playback.
   manager.play();
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">如需型別定義，請參閱<a href="https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-type-definitions-zh-TW#dfb9d282">VeLivePlayerStreamData</a>與<a href="https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-type-definitions-zh-TW#6c9e31fd">VeLivePlayerStream</a>。   </div>
   

2. `onMainBackupSwitch` 回呼來自 `VeLivePlayerObserver`，可通知您播放器在主備串流間切換時的狀態。範例程式碼如下。

   ```Dart
   // 當主串流與備用串流切換時會觸發此回調。
   VeLivePlayerObserver observer = VeLivePlayerObserver(onMainBackupSwitch: (VeLivePlayerStreamType streamType, VeLivePlayerError? error) {
         _addItem('onMainBackupSwitch: $streamType, error:$error');
       });
   manager.setObserver(observer);
   ```
   


<span id="ae69d1e9"></span>
## ABR 串流拉取

ABR 是一種串流技術，透過演算法根據網路狀況自動切換不同解析度的串流。此過程可最大程度減少播放卡頓並提升觀看體驗。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">ABR 功能僅適用於 FLV 串流。</div>


<span id="c07520a7"></span>
### 整合準備

取得各解析度的原始串流與轉碼串流地址。若使用 BytePlus MediaLive 服務，請先登入控制台並完成[轉碼配置](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-configuring-transcoding)。接著可按以下方式取得拉流地址：


* **除錯用**：可使用[地址生成器](https://docs.byteplus.com/en/byteplus-media-live/docs/address-generator)取得拉流地址。

* **正式環境**：可透過呼叫 API [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) 或使用[伺服器 SDK](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-server-sdk)取得拉流地址。


本主題整合步驟以以下拉流地址為範例。


|解析度 |拉流地址 |位元率（kbps） |
|---|---|---|
|來源串流（Origin） |`https://pull.example.com/live/123456.flv` |2500 |
|超高畫質（UHD） |`https://pull.example.com/live/123456_uhd.flv` |2500 |
|高畫質（HD） |`https://pull.example.com/live/123456_hd.flv` |1000 |
|標準畫質（SD） |`https://pull.example.com/live/123456_sd.flv` |800 |
|低畫質（LD） |`https://pull.example.com/live/123456_ld.flv` |500 |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">請確保各解析度的位元率設定與<a href="https://docs.byteplus.com/en/docs/byteplus-media-live/docs-configuring-transcoding">轉碼配置</a>中設定的位元率一致。</div>


<span id="097e0679"></span>
### 整合步驟


1. 配置不同解析度的串流地址以進行播放。範例程式碼如下。

   ```Dart
   // 設定不同解析度的串流地址。
   VeLivePlayerStream playStreamOrigin = VeLivePlayerStream(url: 'https://pull.example.com/live/123456.flv');
   playStreamOrigin.format = VeLivePlayerFormat.flv;
   playStreamOrigin.resolution = VeLivePlayerResolution.origin; // 原始串流解析度。
   playStreamOrigin.type = VeLivePlayerStreamType.main; 
   playStreamOrigin.bitrate = 2500;
   
   VeLivePlayerStream playStreamUHD = VeLivePlayerStream(url: 'https://pull.example.com/live/123456_uhd.flv');
   playStreamOrigin.format = VeLivePlayerFormat.flv;
   playStreamOrigin.resolution = VeLivePlayerResolution.uhd; // UHD 解析度。
   playStreamOrigin.type = VeLivePlayerStreamType.main;
   playStreamOrigin.bitrate = 2500;
   
   VeLivePlayerStream playStreamHD = VeLivePlayerStream(url: 'https://pull.example.com/live/123456_hd.flv');
   playStreamOrigin.format = VeLivePlayerFormat.flv;
   playStreamOrigin.resolution = VeLivePlayerResolution.hd; // HD 解析度。
   playStreamOrigin.type = VeLivePlayerStreamType.main;
   playStreamOrigin.bitrate = 1000;
   
   VeLivePlayerStream playStreamSD = VeLivePlayerStream(url: 'https://pull.example.com/live/123456_sd.flv');
   playStreamOrigin.format = VeLivePlayerFormat.flv;
   playStreamOrigin.resolution = VeLivePlayerResolution.sd; // SD 解析度。
   playStreamOrigin.type = VeLivePlayerStreamType.main;
   playStreamOrigin.bitrate = 800;
   
   VeLivePlayerStream playStreamLD = VeLivePlayerStream(url: 'https://pull.example.com/live/123456_ld.flv');
   playStreamOrigin.format = VeLivePlayerFormat.flv;
   playStreamOrigin.resolution = VeLivePlayerResolution.ld; // LD 解析度。
   playStreamOrigin.type = VeLivePlayerStreamType.main;
   playStreamOrigin.bitrate = 500;
   
   // 建立播放來源。
   VeLivePlayerStreamData streamData = VeLivePlayerStreamData();
   
   // 新增不同解析度的串流。
   List<VeLivePlayerStream> streamList = [];
   streamList.add(playStreamOrigin);
   streamList.add(playStreamUHD);
   streamList.add(playStreamHD);
   streamList.add(playStreamSD);
   streamList.add(playStreamLD);
   streamData.mainStream = streamList;
   
   // 設定播放啟動時使用的預設解析度。以下範例將預設解析度設定為原始串流解析度。
   streamData.defaultResolution = VeLivePlayerResolution.origin;
   
   // 啟用 ABR 功能。
   streamData.enableABR = true;
   
   // 設定播放來源。
   manager.setPlayStreamData(streamData);
   
   // 開始播放。
   manager.play();
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">如需型別定義，請參閱<a href="https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-type-definitions-zh-TW#dfb9d282">VeLivePlayerStreamData</a>與<a href="https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-type-definitions-zh-TW#6c9e31fd">VeLivePlayerStream</a>。   </div>
   

2. `onResolutionSwitch` 回呼來自 `VeLivePlayerObserver`，可通知您解析度自動切換時的狀態。範例程式碼如下。

   ```Dart
   VeLivePlayerObserver observer = VeLivePlayerObserver(onResolutionSwitch:
           (VeLivePlayerResolution resolution, VeLivePlayerError? error,
               VeLivePlayerResolutionSwitchReason reason) {
         print('onResolutionSwitch: $resolution');
       });
   manager.setObserver(observer);
   ```
   


<span id="a83ecddb"></span>
## 畫中畫

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">僅 Flutter 1.47.400 及以上版本支援畫中畫功能。</div>


<span id="2d3df60a"></span>
### 整合準備


* 請確保設備符合以下系統要求：

   * iOS 15.0 及以上版本的實機

   * Android 6.0（minSdkVersion：23）及以上版本的實機

* iOS 端需完成以下配置：

   * 於 Xcode 的 App Target 下，開啟畫中畫權限：

      1. 點擊 **Signing & Capabilities** 分頁下的  **+ Capability**，並雙擊新增 **Background Modes**。

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f8ccac9b131740cab54e2d294a73885f~tplv-goo7wpa0wc-image.image) </span>

      2. 於 **Background Modes** 區域，勾選 **Audio, AirPlay, and Picture in Picture**。

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d3247172cc324cbab1603e4705c42601~tplv-goo7wpa0wc-image.image) </span>

   * 請確保觀眾設備的**設定** \> **一般** \> **畫中畫**頁面中，已開啟**自動啟用畫中畫**開關，允許觀眾在 App 進入背景時透過畫中畫繼續觀看直播。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/96a5bc1446e14b548cdb3095a58c12af~tplv-goo7wpa0wc-image.image) </span>

* Android 端需於 `app` 目錄下的 `AndroidManifest.xml` 檔案中聲明以下 SDK 所需權限：

   ```XML
   <uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />
   <uses-permission android:name="android.permission.SYSTEM_OVERLAY_WINDOW" />
   ```
   


<span id="3b42a18d"></span>
### 整合步驟


1. 啟用畫中畫功能。

   ```Dart
   import 'package:byteplus_live/velive_flutter_sdk.dart';
   
   // 开启画中画功能。
   VeLivePlayer.enablePictureInPicture();
   ```
   

2. 取得 Android 設備的畫中畫權限。

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">此步驟僅適用於 Android。iOS 請直接進行下一步。   </div>
   

   ```Dart
   VeLivePlayer.requestOverlayPermission();
   ```
   

3. 建立播放器，初始化播放器配置，設定播放地址並開始播放。詳情請參閱[Flutter 用 Player SDK：基本功能](https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-basic-features-zh-TW)。

   ```Dart
   // 创建播放器。
   VeLivePlayer manager = await VeLivePlayer.createManager();
   // 初始化播放器配置。
   VeLivePlayerConfiguration configuration = VeLivePlayerConfiguration(
   ...
   );
   manager.setConfig(configuration);
   // 通过 URL 进行播放。支援 RTM、FLV、HLS 直播協議地址。
   String playUrl = "http://pull.example.com/live/stream.flv"
   // 配置播放地址。
   manager.setPlayUrl(playUrl)
   // 开始播放。
   manager.play();
   ```
   

4. 為確保畫中畫功能正常運作，建議先呼叫以下方法判斷目前設備是否支援畫中畫。若不支援，可提供相應提示。

   ```Dart
   VeLivePlayer.isPictureInPictureSupported()
   ```
   

5. 按需監聽畫中畫相關回呼。監聽到相關回呼後，可執行自訂邏輯以滿足業務需求。例如，監聽到畫中畫視窗還原按鈕點擊回呼後，可從畫中畫模式切換至全螢幕模式。

   ```Dart
   VeLivePlayerObserver observer = VeLivePlayerObserver(
       // 畫中畫模式進入回調。
       onStartPictureInPicture: () async {
           bool? isActive = await VeLivePlayer.isPictureInPictureActive();
           print('onStartPictureInPicture' + '(小窗状态:$isActive)'); 
       }, 
       // 畫中畫模式退出回調。
       onStopPictureInPicture: () async {
           bool? isActive = await VeLivePlayer.isPictureInPictureActive();
           print('onStopPictureInPicture' + '(小窗状态:$isActive)'); 
       }, 
       // 畫中畫視窗點擊回調。
       onClickPictureInPicture: () {
           print('onClickPictureInPicture'); 
       }, 
       // 畫中畫模式錯誤回調，可返回錯誤碼與額外資訊。
       onPictureInPictureError: (int code, Map? extraData) {
           print('onPictureInPictureError: $code, $extraData');
       }, 
       // 畫中畫視窗關閉按鈕點擊回調。
       onClickPictureInPictureCloseBtn: () {
           print('onClickPictureInPictureCloseBtn'); 
           Navigator.of(context).pop();
       // 画中画窗口还原按钮点击回调。
       }, onClickPictureInPictureRestoreBtn: () {
           print('onClickPictureInPictureRestoreBtn'); 
       }
   );
   // 设置回调监听器。
   manager.setObserver(observer);
   ```
   

6. 按需呼叫相關方法。

   * App 切換至背景時會自動進入畫中畫模式，無需呼叫 `startPictureInPicture()` 方法。

      ```Dart
      manager.enableAutoPipOnBackground()
      ```
      

   * 進入畫中畫模式。可於觀眾主動觸發進入畫中畫模式或業務邏輯需切換至畫中畫模式時呼叫。

      ```Dart
      manager.startPictureInPicture();
      ```
      

   * 退出畫中畫模式。可於觀眾關閉畫中畫模式或業務邏輯需恢復全螢幕播放時呼叫。

      ```Dart
      manager.stopPictureInPicture();
      ```
      

   * 判斷目前是否處於畫中畫模式。您可根據回傳值，按需決定是否顯示相關 UI 或觸發相應操作。

      ```Dart
      VeLivePlayer.isPictureInPictureActive();
      ```
      


&nbsp;
