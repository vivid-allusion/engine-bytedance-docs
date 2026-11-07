---
title: "iOS Player SDK：基本功能"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-implementing-basic-features-3-zh-TW"
---

本主題介紹如何實作 iOS Player SDK 的基本功能。

## 前提條件

你已依照[整合 iOS Player SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-ios) 和[初始化 iOS Player SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-initializing-for-ios) 中的指示，整合並初始化 Player SDK。

## 注意事項

Player SDK 會使用多種 iOS 音訊和視訊 API。這些 API 在模擬器上可能無法正常運作。建議使用實體裝置進行偵錯。

## 建立播放器

iOS Player SDK 中的播放器類別是 `TVLManager`。以下範例程式碼會建立播放器。

```objectivec
TVLManager *livePlayer = [[TVLManager alloc] init];
```

> **說明**

* > 請依播放器類型選擇初始化方法：

   * > `VeLivePlayerTypeOwn`：SDK 的內建播放器。呼叫 [init](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#init) 會建立此類型的播放器。你也可以呼叫 [initWithType:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#initwithtype) 並傳入 `VeLivePlayerTypeOwn`。只有此類型支援[子母畫面](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#picture-in-picture)。

   * > `VeLivePlayerTypeSystem`：系統播放器。若要建立此類型的播放器，請呼叫 [initWithType:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#initwithtype) 並傳入 `VeLivePlayerTypeSystem`。使用此類型播放 DRM 加密串流。如需詳細資訊，請參閱[播放 DRM 加密串流](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-implementing-advanced-features-3#playing-a-drm-encrypted-stream)。此類型僅支援 M3U8 拉流位址，且不支援以下功能：

      * > 主備串流切換

      * > 自適應位元率（ABR）拉流

      * > 擷取快照

      * > 視訊鏡像

      * > 自訂音訊和視訊算繪

      * > 超解析度

      * > 補充增強資訊（SEI）

* > 為確保最佳播放效果，建議每次播放工作階段建立新的播放器執行個體，而不是重複使用現有執行個體。

## 設定播放器

使用 [VeLivePlayerConfiguration](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#veliveplayerconfiguration) 設定播放器的初始設定，並呼叫 [setConfig:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#setconfig) 套用設定。請在呼叫 [play](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#play) 前完成設定。下表說明 `VeLivePlayerConfiguration` 中的參數。

|參數 |類型 |說明 |
|---|---|---|
|enableSei |BOOL |是否啟用字串 SEI 訊息解析。預設值為 `NO`。 |
|enableBinarySei |BOOL |是否啟用二進位 SEI 訊息解析。預設值為 `NO`。啟用後，播放器會接收二進位 SEI 訊息，且不再觸發字串 SEI 訊息回呼。 |
|enableHardwareDecode |BOOL |是否啟用硬體解碼。預設值為 `YES`。啟用後，如果硬體解碼啟動失敗或在播放期間失敗，播放器會自動切換至軟體解碼。 |
|networkTimeoutMs |NSInteger |網路逾時時間，單位為毫秒。預設值為 `5000`。送出網路請求後，若在此期間內未收到伺服器回應，播放器會判定請求失敗。 |
|retryIntervalTimeMs |NSInteger |重試間隔，單位為毫秒。預設值為 `5000`。如果網路錯誤或類似問題中斷直播播放，播放器會依此間隔重試播放。 |
|retryMaxCount |NSInteger |網路連線錯誤後的最大重試次數。預設值為 `5`。值為 `0` 時會停用播放器內部重試。 |
|stallRetryTimeout |NSInteger |因卡頓而停止重試的逾時閾值，單位為毫秒。預設值為 `10000`（10 秒）。當卡頓持續時間超過此閾值時，播放器會停止重試。 |
|enableLiveDNS |BOOL |是否啟用本機 DNS 預先擷取。預設值為 `YES`。啟用本機 DNS 預先擷取可縮短啟動播放所需時間。<br><br>> **警告**<br><br><br>> 本機 DNS 預先擷取期間發生錯誤可能影響播放器正常運作。<br> |
|enableStatisticsCallback |BOOL |是否啟用播放資訊的週期性回呼。預設值為 `NO`。 |
|statisticsCallbackInterval |NSInteger |提供播放資訊的週期性回呼時間間隔，單位為秒。預設值為 `5`。 |

以下範例程式碼顯示如何設定播放器的初始設定。

```objectivec
// 建立 VeLivePlayerConfiguration 執行個體。
VeLivePlayerConfiguration *config = [[VeLivePlayerConfiguration alloc] init];
// 啟用提供播放資訊的週期性回呼。
config.enableStatisticsCallback = YES;
// 啟用本機 DNS 預先擷取。
config.enableLiveDNS = YES;
// 設定播放器的初始設定。
[self.livePlayer setConfig:config];
```

## 設定播放器觀察者

呼叫 [setObserver:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#setobserver) 設定播放器觀察者，並使用 [VeLivePlayerObserver](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver) 協定監聽播放器狀態更新、錯誤、第一個音訊和視訊影格事件，以及週期性播放統計資料。請在呼叫 [play](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#play) 前設定觀察者。範例程式碼如下。

1. 設定播放器觀察者。

   ```objectivec
   @interface VeLivePullViewController () <VeLivePlayerObserver>
   @end
   
   // 設定播放器觀察者。
   [self.livePlayer setObserver:self];
   ```

2. 處理播放器事件。

   ```objectivec
   - (void)onError:(TVLManager *)player error:(VeLivePlayerError *)error {
       // 播放器發生錯誤時觸發。
   }
   
   - (void)onInfo:(TVLManager *)player info:(VeLivePlayerError *)info {
       // 播放器遇到內部錯誤時觸發。
   }
   
   - (void)onFirstVideoFrameRender:(TVLManager *)player isFirstFrame:(BOOL)isFirstFrame {
       // 第一個視訊影格完成算繪時觸發。
   }
   
   - (void)onFirstAudioFrameRender:(TVLManager *)player isFirstFrame:(BOOL)isFirstFrame {
       // 第一個音訊影格完成算繪時觸發。
   }
   
   - (void)onStallStart:(TVLManager *)player {
       // 播放卡頓開始時觸發。
   }
   
   - (void)onStallEnd:(TVLManager *)player {
       // 播放卡頓停止時觸發。
   }
   
   - (void)onVideoRenderStall:(TVLManager *)player stallTime:(int64_t)stallTime  {
       // 視訊算繪卡頓時觸發。
   }
   
   - (void)onAudioRenderStall:(TVLManager *)player stallTime:(int64_t)stallTime  {
       // 音訊算繪卡頓時觸發。
   }
   
   - (void)onResolutionSwitch:(TVLManager *)player resolution:(VeLivePlayerResolution)resolution error:(VeLivePlayerError *)error reason:(VeLivePlayerResolutionSwitchReason)reason  {
       // 播放器切換至不同畫質層級時觸發。
   }
   
   - (void)onVideoSizeChanged:(TVLManager *)player width:(int)width height:(int)height  {
       // 視訊尺寸變更時觸發。
   }
   
   - (void)onReceiveSeiMessage:(TVLManager *)player message:(NSString *)message  {
       // 播放器收到字串 SEI 訊息時觸發。
   }
   
   - (void)onReceiveBinarySeiMessage:(TVLManager *)player message:(NSData *)message  {
       // 播放器收到二進位 SEI 訊息時觸發。啟用 enableBinarySei 以接收此回呼。啟用後，不再觸發字串 SEI 訊息回呼。
   }
   
   - (void)onMainBackupSwitch:(TVLManager *)player streamType:(VeLivePlayerStreamType)streamType error:(VeLivePlayerError *)error  {
       // 播放器在主串流與備用串流之間切換時觸發。
   }
   
   - (void)onStreamFormatSwitch:(TVLManager *)player fromStreamFormat:(VeLivePlayerFormat)fromStreamType toStreamFormat:(VeLivePlayerFormat)toStreamType error:(VeLivePlayerError *)error extraInfo:(NSDictionary *)extraInfo {
       // 播放器切換串流格式時觸發。
   }
   
   - (void)onPlayerStatusUpdate:(TVLManager *)player status:(VeLivePlayerStatus)status  {
       // 播放器狀態變更時觸發。
   }
   
   - (void)onPlayerStatusUpdate:(TVLManager *)player status:(VeLivePlayerStatus)status extraInfo:(NSDictionary *)extraInfo  {
       // 播放器狀態變更時觸發。extraInfo 參數提供目前播放串流的補充資訊。
   }
   
   - (void)onStatistics:(TVLManager *)player statistics:(VeLivePlayerStatistics *)statistics {
       // 定期觸發以回報播放統計資料。
   }
   
   - (void)onSnapshotComplete:(TVLManager *)player image:(UIImage *)image  {
       // 擷取螢幕擷圖時觸發。
   }
   
   - (void)onRenderVideoFrame:(TVLManager *)player videoFrame:(VeLivePlayerVideoFrame *)videoFrame  {
       // 播放器解碼視訊影格時觸發。
   }
   
   - (void)onRenderAudioFrame:(TVLManager *)player audioFrame:(VeLivePlayerAudioFrame *)audioFrame  {
       // 播放器解碼音訊影格時觸發。
   }
   
   - (void)onStreamFailedOpenSuperResolution:(TVLManager *)player error:(VeLivePlayerError *)error {
       // SDK 無法啟用超解析度時觸發。
   }
   ```

## 設定播放器檢視

將 [playerView](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#playerview) 新增至自訂檢視以算繪視訊。

```objectivec
// 使用 Metal 進行算繪。
self.livePlayer.playerViewRenderType = TVLPlayerViewRenderTypeMetal;

// 設定 playerView 的大小。
self.livePlayer.playerView.frame = UIScreen.mainScreen.bounds;

// 將 playerView 作為子檢視新增至自訂檢視。
[self.view addSubview:self.livePlayer.playerView];
```

## 設定播放 URL

呼叫 [setPlayUrl:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#setplayurl) 設定單一播放 URL。此方法支援 RTMP、FLV 和 HLS 等直播串流協定。請將範例程式碼中的 URL 取代為你的實際直播播放 URL。請在呼叫 [play](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#play) 前呼叫此方法。範例程式碼如下。

```objectivec
NSString *playUrl = @"http://pull.example.com/live/stream.flv";
[self.livePlayer setPlayUrl:playUrl]; // 設定播放 URL。
```

> **說明**

> 若要設定多個播放 URL，請呼叫 [setPlayStreamData:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#setplaystreamdata)。此方法支援 RTM 拉流、QUIC 拉流、主備串流切換、多個畫質層級和自適應位元率（ABR）等功能。請在呼叫 [play](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#play) 前呼叫此方法。如需詳細資訊，請參閱 [iOS Player SDK：進階功能](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3)。

## 調整播放畫面

你可以設定填滿模式、鏡像和旋轉，以取得更好的播放體驗。

### 設定填滿模式

呼叫 [setRenderFillMode:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#setrenderfillmode) 設定播放畫面的填滿模式。播放器支援以下填滿模式。

|填滿模式 |說明 |
|---|---|
|VeLivePlayerFillModeAspectFit |顯示完整的視訊影格。視訊影格會按比例縮放，直到整個影格符合畫布。如果視訊影格的寬高比與畫布不同，未填滿區域會顯示為黑色。 |
|VeLivePlayerFillModeFullFill |讓視訊影格適應畫布。視訊影格會非等比例縮放，直到填滿畫布。在此過程中，視訊影格的寬高比可能會改變。 |
|VeLivePlayerFillModeAspectFill |使用視訊填滿畫布。視訊影格會按比例縮放，直到填滿畫布。超出畫面的視訊影格部分會被裁切。因此，視訊影格的部分內容可能不可見。 |

```objectivec
// 將填滿模式設為 aspect fill。
[self.livePlayer setRenderFillMode:VeLivePlayerFillModeAspectFill];
```

### 設定鏡像

呼叫 [setRenderMirror:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setrendermirror) 設定播放畫面的鏡像。播放器支援以下鏡像模式。

|鏡像模式 |說明 |
|---|---|
|VeLivePlayerMirrorNone |無鏡像。 |
|VeLivePlayerMirrorHorizontal |水平鏡像。 |
|VeLivePlayerMirrorVertical |垂直鏡像。 |

```objectivec
// 設定水平鏡像。
[self.livePlayer setRenderMirror:VeLivePlayerMirrorHorizontal];
```

### 設定旋轉角度

呼叫 [setRenderRotation:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#setrenderrotation) 設定播放畫面的旋轉角度。播放器支援以下旋轉角度。

|旋轉角度 |說明 |
|---|---|
|`VeLivePlayerRotation0` |不旋轉。 |
|`VeLivePlayerRotation90` |將視訊順時針旋轉 90 度。 |
|`VeLivePlayerRotation180` |將視訊順時針旋轉 180 度。 |
|`VeLivePlayerRotation270` |將視訊順時針旋轉 270 度。 |

```objectivec
// 將視訊順時針旋轉 90 度。
[self.livePlayer setRenderRotation:VeLivePlayerRotation90];
```

## 開始播放

呼叫 [play](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#play) 開始播放。

```objectivec
[self.livePlayer play]; // 開始播放。
```

你可以呼叫 [isPlaying](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#isplaying) 取得目前播放狀態。

```objectivec
BOOL isPlaying = [self.livePlayer isPlaying]; // 取得播放狀態。
```

## 停止播放

呼叫 [stop](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#stop) 停止播放。呼叫 `stop` 不會銷毀播放器。

```objectivec
[self.livePlayer stop]; // 停止播放。
```

## 銷毀播放器

停止播放後，如果不再需要播放器，請呼叫 [destroy](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#destroy) 銷毀播放器並釋放其相關記憶體。

```objectivec
[self.livePlayer destroy]; // 銷毀播放器並釋放其相關記憶體。
```

## 處理應用程式前景與背景轉換

預設情況下，應用程式進入背景後，播放器會繼續播放音訊。若要防止音訊在背景繼續播放，請在應用程式進入背景時停止播放，並在應用程式返回前景時繼續播放，如以下程式碼所示：

```objectivec
// 新增觀察者以監聽應用程式切換至前景時的通知。
[NSNotificationCenter.defaultCenter addObserver:self
            selector:@selector(applicationDidBecomeActive:)
            name:UIApplicationDidBecomeActiveNotification
            object:nil];
// 新增觀察者以監聽應用程式切換至背景時的通知。
[NSNotificationCenter.defaultCenter addObserver:self
            selector:@selector(applicationWillResignActive:)
            name:UIApplicationWillResignActiveNotification
            object:nil];

- (void)applicationDidBecomeActive:(NSNotification *)notification {
    [self.livePlayer play]; // 應用程式切換至前景時繼續播放。
}

- (void)applicationWillResignActive:(NSNotification *)notification {
    [self.livePlayer stop]; // 應用程式切換至背景時停止播放。
}
```

## 將播放靜音

呼叫 [setMute:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#setmute) 將音訊靜音或取消靜音。

```objectivec
[self.livePlayer setMute:YES]; // 將播放靜音。
```

你可以呼叫 [isMute](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#ismute) 查詢音訊是否已靜音。

```objectivec
BOOL isMute = [self.livePlayer isMute]; // 取得靜音狀態。
```

## 設定播放器音量

使用 [volume](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#volume) 屬性設定播放器音量。此屬性指定音量層級。預設值為 `1.0`。有效範圍為 `[0.0, 1.0]`。

```objectivec
[self.livePlayer setVolume:0.5];
```

## 設定日誌層級

呼叫 [setLogLevel:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#setloglevel) 設定輸出至主控台的日誌層級。

```objectivec
// 將日誌層級設為 INFO。將輸出 INFO、WARNING 和 ERROR 層級的日誌。
[TVLManager setLogLevel:VeLivePlayerLogLevelInfo];
```

## 疑難排解

錯誤：Cannot remove an observer <TTAVPlayerItem 0x2806577a0\> for the key path "status" from <TVLOwnPlayer 0x2817e9290\> because it is not registered as an observer

如果從不同執行緒呼叫直播播放器的方法，可能會發生此錯誤。若要避免此錯誤，請確保從主執行緒呼叫直播播放器的方法。
