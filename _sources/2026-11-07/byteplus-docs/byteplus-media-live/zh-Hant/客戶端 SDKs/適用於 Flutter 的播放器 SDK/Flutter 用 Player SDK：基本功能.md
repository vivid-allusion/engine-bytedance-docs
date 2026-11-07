---
title: "Flutter 用 Player SDK：基本功能"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/player-sdk-for-flutter-basic-features-zh-TW"
---

本主題介紹如何實現 Flutter 用 Player SDK 的基本功能。

<span id="b3349bc1"></span>
## 先決條件

你已整合並初始化 Flutter 用 Player SDK。如需更多資訊，請參閱 [整合 Player SDK 至 Flutter](https://docs.byteplus.com/docs/byteplus-media-live/integrating-the-player-sdk-for-flutter-zh-TW) 和 [初始化 Flutter 的 Player SDK](https://docs.byteplus.com/docs/byteplus-media-live/initializing-the-player-sdk-for-flutter-zh-TW)。

<span id="cd2e09da"></span>
## 建立播放器並配置渲染視圖

要使用 Flutter 用 Player SDK，必須先建立播放器。要在播放器中顯示影片，必須配置渲染視圖。

```Dart
// 建立 一個 播放器。以下範例 建立一個寬度等於螢幕寬度，高度等於螢幕高度 9/16 的播放器。
VeLivePlayer manager = await VeLivePlayer.createManager();

@override
Widget build(BuildContext context) {
  return Scaffold(
    body: Container(
      height: MediaQuery.of(context).size.height * 9 / 16,
      width: MediaQuery.of(context).size.width,
      // 配置 一個 渲染 視圖。
      child: VeliveFlutterPlayerView(manager: manager),
    ),
  );
}
```


<span id="72224c5b"></span>
## 初始化播放器設定

建立播放器後，可使用 `VeLivePlayerConfiguration` 初始化其設定。下表列出詳細參數。


|參數 |型別 |說明 |
|---|---|---|
|enableSei |boolean |是否啟用解析補充增強資訊（SEI）訊息。預設值為 `false`。有效值：<br><br><br>* `true`：啟用。<br><br>* `false`：停用。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">SEI 訊息是一種與視訊畫面同步的資料通道，常用於在特定時間點顯示互動內容，例如問題、彈幕及虛擬道具，為觀眾帶來更豐富的互動體驗。</div><br> |
|enableHardwareDecode |boolean |是否啟用硬體解碼。預設值為 `true`。有效值：<br><br><br>* `true`：啟用。若硬體解碼失敗，播放器會自動切換為軟體解碼。<br><br>* `false`：停用。 |
|enableLiveDNS |boolean |是否啟用本地 DNS 預解析。預設值為 `false`。有效值：<br><br><br>* `true`：啟用。啟用本地 DNS 預解析可減少播放啟動時間。<br><br>* `false`：停用。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">預解析過程中出現問題可能影響播放器的正常運作。</div><br> |
|enableStatisticsCallback |boolean |是否啟用播放資訊的定期回調。預設值為 `false`。有效值：<br><br><br>* `true`：啟用。<br><br>* `false`：停用。 |
|statisticsCallbackInterval |int |播放資訊定期回調的時間間隔。單位為秒。預設值為 `5`。 |
|networkTimeoutMs |int |網路逾時時間。單位為毫秒。預設值為 `5000`。<br><br>若網路請求在逾時期間未收到伺服器回應，則視為請求失敗。 |
|retryIntervalTimeMs |int |重試間隔。單位為毫秒。預設值為 `5000`。<br><br>直播過程中，若因網路錯誤或類似問題導致中斷，播放器會立即嘗試重試。當重試嘗試失敗後，播放器會在每個重試間隔進行重試。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">此參數僅在沒有備用串流時生效。若有備用串流，播放器將在發生網路錯誤或類似問題時直接切換至備用串流並繼續播放。</div><br> |
|retryMaxCount |int |當網路連線錯誤時，播放器的最大重試次數。預設值為`5`。設定值`0`將停用播放器的內部重試機制。 |


```Dart
// 初始化播放器設定。在以下範例中，啟用 SEI 訊息解析與硬體解碼。
VeLivePlayerConfiguration configuration = await VeLivePlayerConfiguration(
      enableSei: true
      enableHardwareDecode: true
    );
await manager.setConfig(configuration);    
```


<span id="9b96cdda"></span>
## 配置播放 URL

配置支援 RTM、FLV 和 HLS 串流協議的播放 URL。

```Dart
// Play via URL.
String playUrl = "http://pull.example.com/live/stream.flv"
// Configure the playback URL.
manager.setPlayUrl(playUrl)
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">要設定不同的播放 URL 以便播放器在播放期間切換，請使用<code>setPlayStreamData</code>方法。此方法支援主流與備流，以及自適應碼率（ABR）功能。如需更多資訊，請參閱<a href="https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-advanced-features-zh-TW">Flutter 播放器 SDK：進階功能</a>。</div>


<span id="180ccac5"></span>
## 開始播放

```Dart
Future<void> play();
```


<span id="23a7e6fe"></span>
## 檢查播放器是否正在播放

```Dart
Future<bool?> isPlaying();
```


<span id="865bd15c"></span>
## 暫停播放

```Dart
Future<void> pause();
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">在直播期間，暫停與停止播放的效果相同。若在暫停播放後再次呼叫<code>play</code>方法，播放器將重新拉流。</div>


<span id="e5800925"></span>
## 停止播放

```Dart
Future<void> stop();
```


<span id="e46d574a"></span>
## 銷毀播放器

播放停止後，請呼叫此方法以銷毀播放器並釋放其相關記憶體。

```Dart
Future<void> destroy();
```


<span id="19b4ddf5"></span>
## 設定影片縮放模式

可使用播放器的 `setRenderFillMode` 方法設定影片縮放模式。播放器支援以下影片縮放模式。


|影片縮放模式 |說明 |
|---|---|
|aspectfill |保持影片的原始寬高比並填滿播放器。若影片的寬高比與播放器不同，超出播放器邊界的影片區域將被裁切，可能導致畫面不完整。 |
|aspectfit |保持影片的原始寬高比，直到影片完整顯示於播放器內。若影片的寬高比與播放器不同，未被影片填滿的區域將顯示為黑色。 |
|fullfill |影片會完全填滿播放器，但影片的寬高比可能會改變。 |


以下範例程式碼設定影片縮放模式。

```Dart
Future<void> setRenderFillMode(VeLivePlayerFillMode fillMode);
```


<span id="343a19dc"></span>
## 靜音與取消靜音播放

設定播放是否靜音。預設播放為非靜音。

```Dart
Future<void> setMute(bool mute);
```


<span id="348f6dda"></span>
## 取得播放是否靜音

```Dart
Future<bool?> isMute();
```


<span id="83ca7099"></span>
## 設定影片旋轉角度

```Dart
enum VeLivePlayerRotation {
  // Disable rotation.
  rotation0,
  // Rotate 90 degrees clockwise.
  rotation90,
  // Rotate 180 degrees clockwise.
  rotation180,
  // Rotate 270 degrees clockwise.
  rotation270,
}

Future<void> setRenderRotation(VeLivePlayerRotation rotation);
```


<span id="18faede6"></span>
## 配置事件監聽器

透過配置事件監聽器，可接收播放器內部狀態資訊，包括播放狀態、錯誤資訊、音視頻首幀回調，以及定期統計數據。範例程式碼如下。


1. 配置播放器回調。

   ```Dart
   Future<void> setObserver(VeLivePlayerObserver observer);
   ```
   

2. 處理播放器回調。

   ```Dart
     // 當播放器遇到錯誤時會觸發此回呼。
     void Function(VeLivePlayerError error)? onError;
     
     // 當第一個影片畫面成功渲染時，會觸發此回呼。這也適用於成功重試後渲染的第一個影片畫面。
     void Function(bool isFirstFrame)? onFirstVideoFrameRender;
     
     // 當第一個音訊畫面成功渲染時，會觸發此回呼。這也適用於成功重試後渲染的第一個音訊畫面。
     void Function(bool isFirstFrame)? onFirstAudioFrameRender;
     
     // 當解析度變更時會觸發此回呼。
     void Function(VeLivePlayerResolution resolution, VeLivePlayerError? error, VeLivePlayerResolutionSwitchReason reason)? onResolutionSwitch;
     
     // 當播放卡頓開始時會觸發此回呼。
     void Function()? onStallStart;
     
     // 播放卡頓結束回呼。當音訊緩衝區符合播放條件並開始播放時會觸發此回呼。
     void Function()? onStallEnd;
     
     // 當影片寬度或高度變更時會觸發此回呼。
     void Function(int width, int height)? onVideoSizeChanged;
     
     // 當影片渲染卡頓發生時會觸發此回呼。
     void Function(int stallTime)? onVideoRenderStall;
     
     // 當音訊渲染卡頓發生時會觸發此回呼。
     void Function(int stallTime)? onAudioRenderStall;
     
     // 當播放狀態變更時會觸發此回呼。
     void Function(VeLivePlayerStatus status)? onPlayerStatusUpdate;
     
     // A periodic callback that provides playback statistics, such as the current playback URL, bitrate, and frame rate.
     void Function(VeLivePlayerStatistics statistics)? onStatistics;
     
     // 當 SDK 接收到 SEI 訊息時會觸發此回呼。
     void Function(String message)? onReceiveSeiMessage;
     
     // 當主流與備流切換時會觸發此回呼。
     void Function(VeLivePlayerStreamType streamType, VeLivePlayerError? error)? onMainBackupSwitch;
   ```
   


<span id="26f4730d"></span>
## 取得 SDK 版本

```Dart
static Future<String?> getVersion();
```


<span id="a65c2aaa"></span>
## 設定日誌等級

設定輸出至主控台的日誌等級。

```Dart
enum VeLivePlayerLogLevel {
  // Output logs at VERBOSE, DEBUG, INFO, WARNING, and ERROR levels.
  verbose,
  // Output logs at DEBUG, INFO, WARNING, and ERROR levels.
  debug,
  // Output logs at INFO, WARNING, and ERROR levels.
  info,
  // Output logs at WARNING and ERROR levels.
  warn,
  // Output logs at ERROR level.
  error,
  // Disable log output.
  none,
}

static Future<void> setLogLevel(VeLivePlayerLogLevel level);
```
