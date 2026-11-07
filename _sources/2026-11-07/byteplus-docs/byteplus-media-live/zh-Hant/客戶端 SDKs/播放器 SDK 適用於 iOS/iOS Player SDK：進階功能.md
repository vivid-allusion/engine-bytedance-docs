---
title: "iOS Player SDK：進階功能"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-implementing-advanced-features-3-zh-TW"
---

為提升 iOS 應用程式中的觀看體驗，本主題詳細說明如何實作 iOS Player SDK 的進階功能。你可以依據實際業務需求，按需實作複雜功能。

## 前提條件

* 你已依照 [iOS Player SDK：基本功能](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-basic-features-3) 中提供的說明，實作 Player SDK 的基本功能。

* 若要使用下列功能，請確保你使用進階版或試用版 License。

   * [播放 RTM 串流](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#d2fff36e)

   * [QUIC 拉流](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#78c4f3ae)

   * [播放低延遲 FLV 串流](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#3d66c491)

   * [主備流切換](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#49b17368)

   * [ABR 拉流](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#f4206aae)

   * [SEI](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#aceb1766)

   * [超解析度](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#4ea2c546)

   * [H.265 硬體解碼與軟體解碼](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#953988b6)

   * [影片銳化](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#e3976737)

   * [播放 DRM 加密串流](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#e1834266)

   > **警告**

   > 試用版 License 僅供專案測試，且無法續期。試用版 License 過期會導致鑑權失敗，進而中斷服務。請在專案上線前升級至正式 License。如需詳細資訊，請參閱[將試用版 License 升級至基礎版或進階版 License](https://docs.byteplus.com/docs/byteplus-media-live/managing_sdk_licenses#777c7de7)。

## 注意事項

由於 Player SDK 使用多種 iOS 音訊與視訊 API，這些 API 在模擬器上可能無法正常運作，因此建議你使用實體裝置進行測試。

## 流備援策略與主備流切換

如果只配置一個拉流位址，當該位址因網路問題或其他例外而無法使用時，播放可能會卡頓甚至失敗。為降低單一位址發生例外造成播放失敗的風險，你可以為一次播放工作階段配置多個拉流位址，並依需要選擇下列其中一種配置方式：

* **流備援策略**：當你希望播放器依優先順序自動嘗試多個拉流位址時使用。你可以為每個位址配置優先順序與最大重試次數。播放器會先嘗試高優先順序位址。如果某個位址在所有重試嘗試用盡後仍不可用，播放器會切換至下一優先順序的位址。

* **主備流切換**：當你的應用程式維護獨立的主流與備流清單時使用。播放器會先依據流備援策略嘗試主流清單中的串流。只有當主流清單中的所有位址都失敗後，播放器才會自動切換至備流清單並繼續嘗試。

> **說明**

> 只有進階版和試用版 License 支援主備流切換。所有 License 類型都可使用流備援策略。

* 流備援策略

   主流或備流清單中的播放順序如下：

   1. **播放最高優先順序的串流**：根據你設定的 `priority`，播放器會在目前清單中從最高優先順序到最低優先順序嘗試播放串流。

   2. **失敗時重試**：如果目前串流播放失敗，播放器會根據該串流的 `retryMaxCount` 重試。

   3. **切換至備援串流**：如果所有重試嘗試用盡後仍播放失敗，播放器會放棄目前串流，並嘗試目前清單中次高優先順序的串流。

* 主備流切換

   啟用主備流切換後，播放器會依下列順序嘗試串流：

   1. **播放主流**：播放器會先嘗試播放主流清單中的串流。

   2. **切換至備流**：如果主流清單中的所有串流都播放失敗，播放器會嘗試播放備流清單中的串流。

   3. **播放失敗**：如果備流清單中的所有串流也都播放失敗，播放失敗。

在此過程中，SDK 會使用下列回呼通知你目前狀態：

* [onInfo:info:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-oninfo-info)：當某個串流播放失敗但仍存在其他可用串流時觸發。你可以使用此回呼取得詳細錯誤資訊以便偵錯。

* [onStreamFormatSwitch:fromStreamFormat:toStreamFormat:error:extraInfo:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onstreamformatswitch-fromstreamformat-tostreamformat-error-extrainfo)：當播放器切換串流格式時觸發，例如從 RTM 切換至 FLV。

* [onMainBackupSwitch:streamType:error:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onmainbackupswitch-streamtype-error)：當主流清單中的所有串流播放失敗，且播放器成功切換至備流清單時觸發。

* [onError:error:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onerror-error)：當主流與備流清單中的所有串流都播放失敗，且播放最終結束時觸發。

### 前提條件

透過下列其中一種方式，取得 RTM 和 FLV 等協定的拉流位址。同一清單內的備援順序由每個拉流位址的優先順序決定。

* **偵錯用**：使用[位址產生器](https://console.byteplus.com/live/main/locationGenerate)產生拉流位址。

* **生產用**：呼叫 [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023)，或使用[服務端 SDK](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-server-sdk) 動態產生拉流位址。

### 操作步驟

#### 步驟 1：配置備援策略

你可以透過配置 `VeLivePlayerStream` 的 [priority](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStream-priority) 和 [retryMaxCount](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStream-retrymaxcount)，自訂備援策略。

* `priority`：串流的優先順序。值必須是 `0`（預設值）或正整數。**值越大表示優先順序越高**。播放器會優先嘗試播放較高優先順序的串流。

   > **說明**

   > 主流清單與備流清單的優先順序會獨立計算，彼此不互相影響。

* `retryMaxCount`：串流的最大播放嘗試次數，包含首次嘗試。例如，如果值為 `3`，播放器會在首次播放失敗後最多再重試 2 次。有效值：

   * `-1`（預設值）：使用 `VeLivePlayerConfiguration` 中 [retryMaxCount](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerConfiguration-retrymaxcount) 的值。

   * `0`：不嘗試播放此串流。

   * `>0`：最大播放嘗試次數。

**流備援策略**

下列程式碼範例示範基本的流備援情境，播放順序如下：

1. 首先，播放器嘗試播放 RTM 串流（優先順序 5），最多嘗試 3 次。

2. 如果失敗，播放器會備援至 FLV 串流（優先順序 4），最多嘗試 2 次。

3. 如果也失敗，播放結束。

```objectivec
// 建立 VeLivePlayerStreamData 執行個體。
VeLivePlayerStreamData *streamData = [[VeLivePlayerStreamData alloc] init];
NSMutableArray *mainStreams = [NSMutableArray new];

// 新增 RTM 主流（最高優先順序）。
VeLivePlayerStream *rtmStream = [[VeLivePlayerStream alloc] init];
rtmStream.url = @"https://xxx.sdp"; // 替換為你的實際 RTM 拉流位址。
rtmStream.format = VeLivePlayerFormatRTM;
rtmStream.type = VeLivePlayerStreamTypeMain;
rtmStream.protocol = VeLivePlayerProtocolTLS;
rtmStream.retryMaxCount = 3;
rtmStream.priority = 5;
[mainStreams addObject:rtmStream];

// 新增 FLV 主流作為備援串流。
VeLivePlayerStream *flvStream = [[VeLivePlayerStream alloc] init];
flvStream.url = @"https://xxx.flv"; // 替換為你的實際 FLV 拉流位址。
flvStream.format = VeLivePlayerFormatFLV;
flvStream.type = VeLivePlayerStreamTypeMain;
flvStream.protocol = VeLivePlayerProtocolTLS;
flvStream.retryMaxCount = 2;
flvStream.priority = 4;
[mainStreams addObject:flvStream];

streamData.mainStream = mainStreams;

// 配置播放來源。
[self.livePlayer setPlayStreamData:streamData];

// 開始播放。
[self.livePlayer play];
```

**流備援策略 + 主備流切換**

下列程式碼範例示範結合流備援策略與主備流切換的情境，播放順序如下：

1. 首先，播放器嘗試播放主流清單中的 RTM 串流（優先順序 5），最多嘗試 3 次。

2. 如果失敗，播放器會備援至主流清單中的 FLV 串流（優先順序 4），最多嘗試 2 次。

3. 如果仍然失敗，播放器會切換至備流清單，並嘗試播放 RTM 串流（優先順序 5），最多嘗試 3 次。

4. 如果失敗，播放器會備援至備流清單中的 FLV 串流（優先順序 4），最多嘗試 3 次。

5. 如果所有嘗試都失敗，播放結束。

```objectivec
// 建立 VeLivePlayerStreamData 執行個體。
VeLivePlayerStreamData *streamData = [[VeLivePlayerStreamData alloc] init];
// 配置主流清單。
NSMutableArray *mainStreams = [NSMutableArray new];

// 新增 RTM 主流（最高優先順序）。
VeLivePlayerStream *rtmStream = [[VeLivePlayerStream alloc] init];
rtmStream.url = @"https://xxx.sdp"; // 替換為你的實際 RTM 拉流位址。
rtmStream.format = VeLivePlayerFormatRTM;
rtmStream.type = VeLivePlayerStreamTypeMain;
rtmStream.protocol = VeLivePlayerProtocolTLS;
rtmStream.retryMaxCount = 3;
rtmStream.priority = 5;
[mainStreams addObject:rtmStream];

// 新增 FLV 主流作為備援串流。
VeLivePlayerStream *flvStream = [[VeLivePlayerStream alloc] init];
flvStream.url = @"https://xxx.flv"; // 替換為你的實際 FLV 拉流位址。
flvStream.format = VeLivePlayerFormatFLV;
flvStream.type = VeLivePlayerStreamTypeMain;
flvStream.protocol = VeLivePlayerProtocolTLS;
flvStream.retryMaxCount = 2;
flvStream.priority = 4;
[mainStreams addObject:flvStream];

streamData.mainStream = mainStreams;

// 配置備流清單。
NSMutableArray *backupStreams = [NSMutableArray new];
// 新增 RTM 備流。
VeLivePlayerStream *rtmBackupStream = [[VeLivePlayerStream alloc] init];
rtmBackupStream.url = @"https://xxx.sdp"; // 替換為你的實際 RTM 拉流位址。
rtmBackupStream.format = VeLivePlayerFormatRTM;
rtmBackupStream.type = VeLivePlayerStreamTypeBackup;
rtmBackupStream.protocol = VeLivePlayerProtocolTLS;
rtmBackupStream.retryMaxCount = 3;
rtmBackupStream.priority = 5; // 備流清單中的最高優先順序。
[backupStreams addObject:rtmBackupStream];

// 新增 FLV 備流作為備援串流。
VeLivePlayerStream *flvBackupStream = [[VeLivePlayerStream alloc] init];
flvBackupStream.url = @"https://xxx.flv"; // 替換為你的實際 FLV 拉流位址。
flvBackupStream.format = VeLivePlayerFormatFLV;
flvBackupStream.type = VeLivePlayerStreamTypeBackup;
flvBackupStream.protocol = VeLivePlayerProtocolTLS;
flvBackupStream.retryMaxCount = 3;
flvBackupStream.priority = 4;
[backupStreams addObject:flvBackupStream];
streamData.backupStream = backupStreams;

// 啟用主備流切換。
streamData.enableMainBackupSwitch = YES;

// 配置播放來源。
[self.livePlayer setPlayStreamData:streamData];

// 開始播放。
[self.livePlayer play];
```

**多畫質流備援策略**

流備援策略支援為[解析度切換](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#660adfe3)、[ABR 拉流](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#f4206aae)（僅 FLV 串流）和[平滑畫質等級切換](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#37bcd52d)所使用的多畫質串流配置，配置備援串流。配置時，為同一多畫質串流群組中的串流設定相同的 `priority` 值。播放器會先從最高 `priority` 到最低 `priority` 選擇串流群組。如果高優先順序的多畫質串流播放失敗，播放器會備援至較低優先順序的串流。

在下列範例中，播放器會先播放 `priority` 為 `5` 的 ABR 多畫質串流。如果 ABR 多畫質串流播放失敗，播放器會備援至 `priority` 為 `4` 的一般 FLV 串流。

```objectivec
// 建立 VeLivePlayerStreamData 執行個體。
VeLivePlayerStreamData *streamData = [[VeLivePlayerStreamData alloc] init];
NSMutableArray *mainStreams = [NSMutableArray new];

// 新增 ABR 多畫質串流的原畫質等級。優先順序為 5。
VeLivePlayerStream *flvOriginStream = [[VeLivePlayerStream alloc] init];
flvOriginStream.url = @"https://xxx_origin.flv"; // 替換為原畫質等級的實際 FLV 拉流位址。
flvOriginStream.format = VeLivePlayerFormatFLV;
flvOriginStream.type = VeLivePlayerStreamTypeMain;
flvOriginStream.protocol = VeLivePlayerProtocolTLS;
flvOriginStream.resolution = VeLivePlayerResolutionOrigin; // 畫質等級識別碼。
flvOriginStream.bitrate = 2000;
flvOriginStream.retryMaxCount = 3;
flvOriginStream.priority = 5;
[mainStreams addObject:flvOriginStream];

// 新增 ABR 多畫質串流的 UHD 畫質等級。優先順序為 5。
VeLivePlayerStream *flvUHDStream = [[VeLivePlayerStream alloc] init];
flvUHDStream.url = @"https://xxx_uhd.flv"; // 替換為 UHD 畫質等級的實際 FLV 拉流位址。
flvUHDStream.format = VeLivePlayerFormatFLV;
flvUHDStream.type = VeLivePlayerStreamTypeMain;
flvUHDStream.protocol = VeLivePlayerProtocolTLS;
flvUHDStream.resolution = VeLivePlayerResolutionUHD; // 畫質等級識別碼。
flvUHDStream.bitrate = 1800;
flvUHDStream.retryMaxCount = 3;
flvUHDStream.priority = 5;
[mainStreams addObject:flvUHDStream];

// 新增 ABR 多畫質串流的 HD 畫質等級。優先順序為 5。
VeLivePlayerStream *flvHDStream = [[VeLivePlayerStream alloc] init];
flvHDStream.url = @"https://xxx_hd.flv"; // 替換為 HD 畫質等級的實際 FLV 拉流位址。
flvHDStream.format = VeLivePlayerFormatFLV;
flvHDStream.type = VeLivePlayerStreamTypeMain;
flvHDStream.protocol = VeLivePlayerProtocolTLS;
flvHDStream.resolution = VeLivePlayerResolutionHD; // 畫質等級識別碼。
flvHDStream.bitrate = 1500;
flvHDStream.retryMaxCount = 3;
flvHDStream.priority = 5;
[mainStreams addObject:flvHDStream];

// 新增一般 FLV 串流作為備援串流。優先順序為 4。
VeLivePlayerStream *flvStream = [[VeLivePlayerStream alloc] init];
flvStream.url = @"https://xxx.flv"; // 替換為你的實際 FLV 拉流位址。
flvStream.format = VeLivePlayerFormatFLV;
flvStream.type = VeLivePlayerStreamTypeMain;
flvStream.protocol = VeLivePlayerProtocolTLS;
flvStream.retryMaxCount = 2;
flvStream.priority = 4;
[mainStreams addObject:flvStream];

streamData.mainStream = mainStreams;

// 配置預設啟動畫質等級。
streamData.defaultResolution = VeLivePlayerResolutionOrigin;

// 啟用 ABR。
streamData.enableABR = YES;

// 配置播放來源。
[self.livePlayer setPlayStreamData:streamData];

// 開始播放。
[self.livePlayer play];
```

#### 步驟 2：新增回呼

依需要新增下列回呼，以監聽備援過程中的事件。

* 監聽串流格式切換，例如從 RTM 切換至 FLV。

   ```objectivec
   - (void)onStreamFormatSwitch:(TVLManager *_Nonnull)player fromStreamFormat:(VeLivePlayerFormat)fromStreamType toStreamFormat:(VeLivePlayerFormat)toStreamType error:(VeLivePlayerError *)error extraInfo:(NSDictionary *)extraInfo;
   ```

* 監聽播放期間遇到的可復原問題。當某個串流播放失敗，但 SDK 即將執行復原動作，例如切換至備援串流時，會觸發此回呼。這表示播放仍在繼續，你不需要中斷播放流程。偵錯時，你可以使用傳回的錯誤資訊了解串流播放失敗的具體原因。

   ```objectivec
   - (void)onInfo:(TVLManager *_Nonnull)player info:(VeLivePlayerError *_Nonnull)info;
   ```

* 監聽從主流切換至備流。

   ```objectivec
   - (void)onMainBackupSwitch:(TVLManager *_Nonnull)player streamType:(VeLivePlayerStreamType)streamType error:(VeLivePlayerError *)error;
   ```

* 監聽播放最終結束，也就是所有串流都播放失敗。

   ```objectivec
   - (void)onError:(TVLManager *_Nonnull)player error:(VeLivePlayerError *_Nonnull)error;
   ```

## 播放 RTM 串流

播放 RTM 串流可將直播延遲降低至 1\-2 秒，為觀眾提供高品質直播觀看體驗。

不過，RTM 的超低延遲功能也對網路環境提出更高要求。在不穩定的網路條件下，可能會發生播放延遲、卡頓或失敗。如果你希望在 RTM 拉流位址不可用時，自動嘗試 FLV 等其他協定的拉流位址，請將此功能與流備援策略或主備流切換搭配使用。如需詳細資訊，請參閱[流備援策略與主備流切換](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#49b17368)。

> **說明**

> 只有進階版和試用版 License 支援播放 RTM 串流。

### 前提條件

* 確保你已整合 Player SDK 1.50.100 或更新版本，並新增 `LivePull-RTS` 依賴項。如需詳細資訊，請參閱[整合 iOS 版 Player SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-ios)。

* 透過下列其中一種方式，取得 RTM 和 FLV 等協定的拉流位址。

   * **偵錯用**：使用[位址產生器](https://console.byteplus.com/live/main/locationGenerate)產生拉流位址。

   * **生產用**：呼叫 [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023)，或使用[服務端 SDK](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-server-sdk) 動態產生拉流位址。

### 操作步驟

本主題提供下列兩個程式碼範例，對應從簡單到複雜的情境：

* **基本情境**：示範當主流清單中的高優先順序 RTM 串流播放失敗時，如何自動備援至 FLV 等其他協定的串流。

* **進階情境**：在基本情境上新增主備流切換機制。當主流清單中的所有串流，包括 RTM 串流和備援串流，都不可用時，播放器會自動切換至備流清單重試。

建議你從基本情境開始。

**基本情境**

下列程式碼範例示範基本的流備援情境，播放順序如下：

1. 首先，播放器嘗試播放 RTM 串流（優先順序 5），最多嘗試 3 次。

2. 如果失敗，播放器會備援至 FLV 串流（優先順序 4），最多嘗試 2 次。

3. 如果也失敗，播放結束。

```objectivec
// 建立 VeLivePlayerStreamData 執行個體。
VeLivePlayerStreamData *streamData = [[VeLivePlayerStreamData alloc] init];
NSMutableArray *mainStreams = [NSMutableArray new];

// 新增 RTM 主流（最高優先順序）。
VeLivePlayerStream *rtmStream = [[VeLivePlayerStream alloc] init];
rtmStream.url = @"https://xxx.sdp"; // 替換為你的實際 RTM 拉流位址。
rtmStream.format = VeLivePlayerFormatRTM;
rtmStream.type = VeLivePlayerStreamTypeMain;
rtmStream.protocol = VeLivePlayerProtocolTLS;
rtmStream.retryMaxCount = 3;
rtmStream.priority = 5;
[mainStreams addObject:rtmStream];

// 新增 FLV 主流作為備援串流。
VeLivePlayerStream *flvStream = [[VeLivePlayerStream alloc] init];
flvStream.url = @"https://xxx.flv"; // 替換為你的實際 FLV 拉流位址。
flvStream.format = VeLivePlayerFormatFLV;
flvStream.type = VeLivePlayerStreamTypeMain;
flvStream.protocol = VeLivePlayerProtocolTLS;
flvStream.retryMaxCount = 2;
flvStream.priority = 4;
[mainStreams addObject:flvStream];

streamData.mainStream = mainStreams;

// 配置播放來源。
[self.livePlayer setPlayStreamData:streamData];

// 開始播放。
[self.livePlayer play];
```

**進階情境**

下列程式碼範例示範結合流備援策略與主備流切換的情境，播放順序如下：

1. 首先，播放器嘗試播放主流清單中的 RTM 串流（優先順序 5），最多嘗試 3 次。

2. 如果失敗，播放器會備援至主流清單中的 FLV 串流（優先順序 4），最多嘗試 2 次。

3. 如果仍然失敗，播放器會切換至備流清單，並嘗試播放 RTM 串流（優先順序 5），最多嘗試 3 次。

4. 如果失敗，播放器會備援至備流清單中的 FLV 串流（優先順序 4），最多嘗試 3 次。

5. 如果所有嘗試都失敗，播放結束。

```objectivec
// 建立 VeLivePlayerStreamData 執行個體。
VeLivePlayerStreamData *streamData = [[VeLivePlayerStreamData alloc] init];
// 配置主流清單。
NSMutableArray *mainStreams = [NSMutableArray new];

// 新增 RTM 主流（最高優先順序）。
VeLivePlayerStream *rtmStream = [[VeLivePlayerStream alloc] init];
rtmStream.url = @"https://xxx.sdp"; // 替換為你的實際 RTM 拉流位址。
rtmStream.format = VeLivePlayerFormatRTM;
rtmStream.type = VeLivePlayerStreamTypeMain;
rtmStream.protocol = VeLivePlayerProtocolTLS;
rtmStream.retryMaxCount = 3;
rtmStream.priority = 5;
[mainStreams addObject:rtmStream];

// 新增 FLV 主流作為備援串流。
VeLivePlayerStream *flvStream = [[VeLivePlayerStream alloc] init];
flvStream.url = @"https://xxx.flv"; // 替換為你的實際 FLV 拉流位址。
flvStream.format = VeLivePlayerFormatFLV;
flvStream.type = VeLivePlayerStreamTypeMain;
flvStream.protocol = VeLivePlayerProtocolTLS;
flvStream.retryMaxCount = 2;
flvStream.priority = 4;
[mainStreams addObject:flvStream];

streamData.mainStream = mainStreams;

// 配置備流清單。
NSMutableArray *backupStreams = [NSMutableArray new];
// 新增 RTM 備流。
VeLivePlayerStream *rtmBackupStream = [[VeLivePlayerStream alloc] init];
rtmBackupStream.url = @"https://xxx.sdp"; // 替換為你的實際 RTM 拉流位址。
rtmBackupStream.format = VeLivePlayerFormatRTM;
rtmBackupStream.type = VeLivePlayerStreamTypeBackup;
rtmBackupStream.protocol = VeLivePlayerProtocolTLS;
rtmBackupStream.retryMaxCount = 3;
rtmBackupStream.priority = 5; // 備流清單中的最高優先順序。
[backupStreams addObject:rtmBackupStream];

// 新增 FLV 備流作為備援串流。
VeLivePlayerStream *flvBackupStream = [[VeLivePlayerStream alloc] init];
flvBackupStream.url = @"https://xxx.flv"; // 替換為你的實際 FLV 拉流位址。
flvBackupStream.format = VeLivePlayerFormatFLV;
flvBackupStream.type = VeLivePlayerStreamTypeBackup;
flvBackupStream.protocol = VeLivePlayerProtocolTLS;
flvBackupStream.retryMaxCount = 3;
flvBackupStream.priority = 4;
[backupStreams addObject:flvBackupStream];
streamData.backupStream = backupStreams;

// 啟用主備流切換。
streamData.enableMainBackupSwitch = YES;

// 配置播放來源。
[self.livePlayer setPlayStreamData:streamData];

// 開始播放。
[self.livePlayer play];
```

## 播放低延遲 FLV 串流

啟用低延遲 FLV 串流後，FLV 拉流可將直播延遲降低至 2\-3 秒。

> **說明**

> 若要播放低延遲 FLV 串流，請確保你已整合 SDK 1.50.200.3\-premium 或更新版本，且正在使用進階版或試用版 License。

### 操作步驟

開始播放前，你可以透過播放器的進階 API [setProperty:value:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setproperty-value) 啟用低延遲 FLV 串流。呼叫 `setProperty:value:` 時，需要傳入 `key-value` 配置。

**Key**

|參數名稱 |類型 |說明 |
|---|---|---|
|VeLivePlayerKeySetParamsLowLatencyFlv |NSString |低延遲 FLV 串流功能的屬性鍵。 |

**Value**

此值是包含 `key-value` 配對的 `NSDictionary` 物件，用於配置低延遲 FLV 串流功能。

* `Key`：`NSString` 類型。值固定為 `EnableLowLatencyFLV`，表示是否啟用低延遲 FLV 串流功能。

* `Value`：`NSNumber` 類型。值為 `1` 時啟用低延遲 FLV 串流功能，值為 `0` 時停用此功能。預設值為 `0`。

範例程式碼如下。

```objectivec
[self.livePlayer setProperty:VeLivePlayerKeySetParamsLowLatencyFlv value:@{@"EnableLowLatencyFLV": @1}];
```

## QUIC 拉流

Player SDK 支援 QUIC 拉流。此功能應與 BytePlus MediaLive 搭配使用。

> **說明**

> 只有進階版和試用版 License 支援 QUIC 拉流。

### 前提條件

在 BytePlus Live 控制台中使用[位址產生器](https://console.byteplus.com/live/main/locationGenerate)產生 FLV 拉流位址。

### 操作步驟

配置 QUIC 拉流位址並開始播放。範例程式碼如下。

```objectivec
VeLivePlayerStream *playStreamFLV = [[VeLivePlayerStream alloc]init]; 
playStreamFLV.url = @"https://pull.example.com/live/stream.flv"; // 替換為你的實際 FLV 拉流位址。
playStreamFLV.format = VeLivePlayerFormatFLV;
playStreamFLV.protocol = VeLivePlayerProtocolQUIC;

// 建立 VeLivePlayerStreamData 執行個體。
VeLivePlayerStreamData *streamData = [[VeLivePlayerStreamData alloc]init];
NSMutableArray <VeLivePlayerStream *> *mainStreams = [NSMutableArray arrayWithCapacity:1];

// 新增 FLV 串流位址。
[mainStreams addObject:playStreamFLV];

streamData.mainStream = mainStreams;

// 配置播放來源。
[self.livePlayer setPlayStreamData:streamData];

// 開始播放。
[self.livePlayer play];
```

> **說明**

> Player SDK 預設啟用 QUIC 失敗備援策略。如果 QUIC 拉流失敗，SDK 會自動備援至 TCP 拉流。

## 播放 DRM 加密串流

> **說明**

> 只有進階版和試用版 License 支援播放 DRM 加密串流。

若要播放受數位版權管理 (DRM) 保護的串流，請執行下列操作：

1. 依照[使用 DRM 加密你的直播串流](https://docs.byteplus.com/docs/byteplus-media-live/docs-encrypting-your-live-streams-using-drm)中的詳細說明，取得下列資訊：

   * 取得 M3U8 格式的 DRM 加密拉流位址。

   * 使用 [DescribeLicenseDRM](https://docs.byteplus.com/docs/byteplus-media-live/docs-describelicensedrm) 取得 DRM License 的擷取 URL。此 URL 包含鑑權資訊和到期時間。

   * 使用 [DescribeCertDRM](https://docs.byteplus.com/docs/byteplus-media-live/docs-describecertdrm) 取得 FairPlay 串流憑證。

2. 在你的 iOS 專案中，透過呼叫 [initWithType:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#initwithtype) 初始化播放器。

   ```objectivec
   self.livePlayer = [[TVLManager alloc] initWithType:VeLivePlayerTypeSystem];
   ```

   > **說明**

   > 使用 `initWithType:` 初始化的系統播放器不支援下列功能：

   * > 播放 M3U8 格式以外的串流

   * > 主備流切換

   * > ABR 拉流

   * > 擷取快照

   * > 鏡像

   * > 音訊與視訊自訂渲染

   * > 超解析度

   * > SEI

3. 設定 DRM 加密拉流位址。

   ```objectivec
   NSString *playUrl = @"http://pull.example.com/live/stream.m3u8"; // 替換為你的實際 DRM 加密拉流位址。
   [self.livePlayer setPlayUrl:playUrl];
   ```

4. 實作播放器觀察者的 [getDrmResourceLoaderCertificateData:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#getdrmresourceloadercertificatedata) 和 [getDrmResourceLoaderLicenseUrl:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#getdrmresourceloaderlicenseurl) 回呼，以向 SDK 提供 FairPlay 憑證資料與 DRM License URL。

   ```objectivec
   - (NSData *)getDrmResourceLoaderCertificateData:(TVLManager *)player {
       NSString *filePath = [[NSBundle mainBundle] pathForResource:@"testfairplay" ofType:@"cer"]; // 將 testfairplay 替換為實際 FairPlay 憑證檔案名稱。
       NSData *certificate = [NSData dataWithContentsOfFile:filePath];
       return certificate;
   }
   
   - (NSString *)getDrmResourceLoaderLicenseUrl:(TVLManager *)player {
       return @"https://drmtest/license"; // 替換為實際 DRM License URL。
   }
   ```

5. 播放 DRM 加密串流。

   ```objectivec
   [self.livePlayer play];
   ```

## 使用 IP 位址拉流

播放器支援使用網域的 IP 位址拉流，以縮短首幀時間。

### 前提條件

取得拉流位址並解析其 IP 位址。

### 操作步驟

使用播放器的 [setUrlHostIP:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#seturlhostip) API，將 IP 位址與網域名稱建立關聯。播放器接著會直接使用 IP 位址拉流。範例程式碼如下。

```objectivec
[self.livePlayer setPlayUrl:@"https://pull.example.com/live/stream.flv"]; // 替換為你的實際拉流位址。

// 將拉流位址中的網域對應至其解析出的 IP 位址。
NSMutableArray<NSString *> *ipList = [[NSMutableArray alloc] initWithCapacity:1];
[ipList addObject:@"xxx.xxx.xxx.xxx"];  // 替換為從網域解析出的實際 IP 位址。

NSMutableDictionary* ipHost = [[NSMutableDictionary alloc] initWithCapacity:1];
[ipHost setObject:ipList forKey:@"pull.example.com"]; // 將 pull.example.com 替換為你實際拉流位址中的網域。

// 設定網域到 IP 的對應。
[self.livePlayer setUrlHostIP:ipHost];

// 開始播放。
[self.livePlayer play];
```

## 解析度切換

你可以設定多個不同解析度的拉流位址，並在播放期間於這些位址之間切換。

> **說明**

> 解析度切換支援流備援策略。你可以為一組多解析度串流指派相同優先順序，並配置較低優先順序的備援串流。如果較高優先順序的串流群組播放失敗，SDK 會自動嘗試備援群組。如需詳細資訊，請參閱[流備援策略與主備流切換](https://docs.byteplus.com/en/docs/24/107347#stream-fallback-strategy-and-primary-backup-stream-switching)。

### 前提條件

取得不同解析度的拉流位址。如果你使用 BytePlus MediaLive 提供的直播服務，請執行下列操作：

1. [配置轉碼任務](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-transcoding)，以產生多個不同解析度的轉碼串流。

2. 透過下列其中一種方式，取得原始串流和轉碼串流的拉流位址。

   * **偵錯用**：使用[位址產生器](https://console.byteplus.com/live/main/locationGenerate)產生拉流位址。

   * **生產用**：呼叫 [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023)，或使用[服務端 SDK](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-server-sdk) 動態產生拉流位址。

      本節使用下列拉流位址作為範例。

   |**解析度** |**拉流位址** |
   |---|---|
   |原畫質 (Origin) |`https://pull.example.com/live/123456.flv` |
   |超高畫質 (UHD) |`https://pull.example.com/live/123456_uhd.flv` |
   |高畫質 (HD) |`https://pull.example.com/live/123456_hd.flv` |
   |標準畫質 (SD) |`https://pull.example.com/live/123456_sd.flv` |
   |低畫質 (LD) |`https://pull.example.com/live/123456_ld.flv` |

### 操作步驟

1. 配置多解析度拉流位址並開始播放。範例程式碼如下。

   ```objectivec
   // 配置多個畫質等級的拉流位址。
   VeLivePlayerStream *playStreamOrigin = [[VeLivePlayerStream alloc]init];
   playStreamOrigin.url = @"https://pull.example.com/live/123456.flv"; // 替換為原畫質等級的實際拉流位址。
   playStreamOrigin.resolution = VeLivePlayerResolutionOrigin; // 原畫質等級。
   
   VeLivePlayerStream *playStreamUHD = [[VeLivePlayerStream alloc]init];
   playStreamUHD.url = @"https://pull.example.com/live/123456_uhd.flv"; // 替換為 UHD 畫質等級的實際拉流位址。
   playStreamUHD.resolution = VeLivePlayerResolutionUHD; // UHD 畫質等級。
   
   VeLivePlayerStream *playStreamHD = [[VeLivePlayerStream alloc]init];
   playStreamHD.url = @"https://pull.example.com/live/123456_hd.flv"; // 替換為 HD 畫質等級的實際拉流位址。
   playStreamHD.resolution = VeLivePlayerResolutionHD; // HD 畫質等級。
   
   VeLivePlayerStream *playStreamSD = [[VeLivePlayerStream alloc]init];
   playStreamSD.url = @"https://pull.example.com/live/123456_sd.flv"; // 替換為 SD 畫質等級的實際拉流位址。
   playStreamSD.resolution = VeLivePlayerResolutionSD; // SD 畫質等級。
   
   VeLivePlayerStream *playStreamLD = [[VeLivePlayerStream alloc]init];
   playStreamLD.url = @"https://pull.example.com/live/123456_ld.flv"; // 替換為 LD 畫質等級的實際拉流位址。
   playStreamLD.resolution = VeLivePlayerResolutionLD; // LD 畫質等級。
   
   // 建立 VeLivePlayerStreamData 執行個體。
   VeLivePlayerStreamData *streamData = [[VeLivePlayerStreamData alloc]init];
   
   // 新增拉流位址。
   NSMutableArray <VeLivePlayerStream *> *mainStreams = [NSMutableArray arrayWithCapacity:1];
   [mainStreams addObject:playStreamOrigin];
   [mainStreams addObject:playStreamUHD];
   [mainStreams addObject:playStreamHD];
   [mainStreams addObject:playStreamSD];
   [mainStreams addObject:playStreamLD];
   streamData.mainStream = mainStreams;
   
   // 將預設解析度設為原畫質。
   streamData.defaultResolution = VeLivePlayerResolutionOrigin;
   
   // 配置播放來源。
   [self.livePlayer setPlayStreamData:streamData];
   
   // 開始播放。
   [self.livePlayer play];
   ```

2. 呼叫 [switchResolution:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#switchresolution) 變更解析度。

   ```objectivec
   [self.livePlayer switchResolution:VeLivePlayerResolutionUHD]; // 切換至 UHD 畫質等級。
   ```

3. 切換成功時，會觸發 [onResolutionSwitch:resolution:error:reason:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onresolutionswitch-resolution-error-reason) 回呼。

   ```objectivec
   - (void)onResolutionSwitch:(TVLManager *)player resolution:(VeLivePlayerResolution)resolution error:(VeLivePlayerError *)error reason:(VeLivePlayerResolutionSwitchReason)reason  {
     // 解析度切換完成時觸發。
   }
   ```

## ABR 拉流

自適應位元率 (ABR) 拉流可在網路條件變化時切換至更適合的畫質等級，協助維持流暢播放。

> **說明**

* > ABR 拉流支援 **RTM\-ABR 串流**和 **FLV 串流**。

* > 只有進階版和試用版 License 支援 ABR 拉流。

* > ABR 拉流支援流備援策略。對於 RTM\-ABR 串流，你可以在備援策略中將 RTM\-ABR 拉流位址作為 RTM 串流使用。對於 FLV 串流，請為一個 ABR 串流群組中的所有畫質等級指派相同優先順序，並配置較低優先順序的備援串流。如果較高優先順序的 ABR 串流群組播放失敗，SDK 會自動嘗試備援群組。如需詳細資訊，請參閱[流備援策略與主備流切換](https://docs.byteplus.com/en/docs/24/107347#stream-fallback-strategy-and-primary-backup-stream-switching)。

目前，iOS Player SDK 支援下列 ABR 模式：

* **RTM\-ABR 串流**：用於 RTM 播放的服務端 ABR 能力。播放器只使用**一個** RTM\-ABR 拉流位址，伺服器會根據觀眾的網路條件自動選擇並切換畫質等級。這有助於在弱網路環境下降低卡頓，同時保留 RTM 的低延遲播放體驗。

* **FLV 串流**：用戶端 ABR 能力。你提供多個 FLV 拉流位址與位元率資訊，SDK 會根據網路條件在它們之間切換。

### RTM\-ABR 串流

> **警告**

> 只有 1.51.100.3\-premium 及更新版本支援 RTM\-ABR 串流。

#### 前提條件

* 配置多個 ABR 子流，並在新增 ABR 配置時選擇 **RTM\-ABR** 作為**協定類型**。如需詳細資訊，請參閱[管理自適應位元率配置](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-an-hls-abr-task)。

* 透過下列其中一種方式取得 RTM\-ABR 拉流位址。

   * **偵錯用**：使用[位址產生器](https://console.byteplus.com/live/main/locationGenerate)，並選擇啟動畫質等級（後綴），以在**自適應位元率**頁籤取得 **RTM 位址**。如需詳細資訊，請參閱[產生串流位址](https://docs.byteplus.com/docs/byteplus-media-live/docs-address-generator)。

   * **生產用**：呼叫 [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023)，或使用[服務端 SDK](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-server-sdk) 動態產生 RTM\-ABR 拉流位址。不同後綴對應不同的啟動畫質等級。請使用其中一個位址開始播放。請確保 `Protocol` 的值為 `udp`。

   > **警告**

   > 請勿手動將 `rtmabr=true` 附加到一般 RTM 拉流位址。只有完成 RTM\-ABR 配置並使用產生的 RTM\-ABR 位址後，RTM\-ABR 才會生效。

#### 操作步驟

設定 **RTM\-ABR** 拉流位址並開始播放。

```objectivec
[self.livePlayer setPlayUrl:@"https://pull.example.com/live/test_uhd.sdp?rtmabr=true"]; // 替換為你的實際 RTM-ABR 拉流位址。

// 開始播放。
[self.livePlayer play];
```

### FLV 串流

#### 前提條件

取得來源串流與各畫質等級轉碼串流的拉流位址。如果你使用 BytePlus MediaLive，請先登入控制台並完成[轉碼配置](https://console.byteplus.com/live/main/application/transcode)，再取得拉流位址。你可以透過下列任一方式取得位址：

* **偵錯用**：使用[位址產生器](https://console.byteplus.com/live/main/locationGenerate)產生拉流位址。

* **生產用**：呼叫 [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023)，或使用[服務端 SDK](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-server-sdk) 動態產生拉流位址。

本節使用下列拉流位址作為範例。

|畫質等級 |拉流位址 |位元率 (kbps) |
|---|---|---|
|原畫質 (Origin) |`https://pull.example.com/live/123456.flv` |2500 |
|超高畫質 (UHD) |`https://pull.example.com/live/123456_uhd.flv` |2500 |
|高畫質 (HD) |`https://pull.example.com/live/123456_hd.flv` |1000 |
|標準畫質 (SD) |`https://pull.example.com/live/123456_sd.flv` |800 |
|低畫質 (LD) |`https://pull.example.com/live/123456_ld.flv` |500 |

> **警告**

> 為 ABR 配置多個畫質等級拉流位址時，SDK 中每個畫質等級的編碼位元率，必須與[轉碼配置](https://console.byteplus.com/live/main/application/transcode)中配置的編碼位元率相同。如需詳細資訊，請參閱[管理轉碼配置](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-transcoding)。

#### 操作步驟

1. 配置多畫質拉流位址並開始播放。範例程式碼如下。

   ```objectivec
   // 配置多個畫質等級的拉流位址。
   VeLivePlayerStream *playStreamOrigin = [[VeLivePlayerStream alloc]init];
   playStreamOrigin.url = @"https://pull.example.com/live/123456.flv"; // 替換為原畫質等級的實際拉流位址。
   playStreamOrigin.resolution = VeLivePlayerResolutionOrigin; // 原畫質等級。
   playStreamOrigin.bitrate = 2500;
   
   VeLivePlayerStream *playStreamUHD = [[VeLivePlayerStream alloc]init];
   playStreamUHD.url = @"https://pull.example.com/live/123456_uhd.flv"; // 替換為 UHD 畫質等級的實際拉流位址。
   playStreamUHD.resolution = VeLivePlayerResolutionUHD; // UHD 畫質等級。
   playStreamUHD.bitrate = 2500;
   
   VeLivePlayerStream *playStreamHD = [[VeLivePlayerStream alloc]init];
   playStreamHD.url = @"https://pull.example.com/live/123456_hd.flv"; // 替換為 HD 畫質等級的實際拉流位址。
   playStreamHD.resolution = VeLivePlayerResolutionHD; // HD 畫質等級。
   playStreamHD.bitrate = 1000;
   
   VeLivePlayerStream *playStreamSD = [[VeLivePlayerStream alloc]init];
   playStreamSD.url = @"https://pull.example.com/live/123456_sd.flv"; // 替換為 SD 畫質等級的實際拉流位址。
   playStreamSD.resolution = VeLivePlayerResolutionSD; // SD 畫質等級。
   playStreamSD.bitrate = 800;
   
   VeLivePlayerStream *playStreamLD = [[VeLivePlayerStream alloc]init];
   playStreamLD.url = @"https://pull.example.com/live/123456_ld.flv";  // 替換為 LD 畫質等級的實際拉流位址。
   playStreamLD.resolution = VeLivePlayerResolutionLD; // LD 畫質等級。
   playStreamLD.bitrate = 500;
   
   // 建立 VeLivePlayerStreamData 執行個體。
   VeLivePlayerStreamData *streamData = [[VeLivePlayerStreamData alloc]init];
   
   // 新增多畫質串流。
   NSMutableArray <VeLivePlayerStream *> *mainStreams = [NSMutableArray arrayWithCapacity:1];
   [mainStreams addObject:playStreamOrigin];
   [mainStreams addObject:playStreamUHD];
   [mainStreams addObject:playStreamHD];
   [mainStreams addObject:playStreamSD];
   [mainStreams addObject:playStreamLD];
   streamData.mainStream = mainStreams;
   
   // 配置預設啟動畫質等級。
   streamData.defaultResolution = VeLivePlayerResolutionOrigin;
   
   // 啟用 ABR。
   streamData.enableABR = YES;
   
   // 配置播放來源。
   [self.livePlayer setPlayStreamData:streamData];
   
   // 開始播放。
   [self.livePlayer play];
   ```

2. 當 ABR 畫質等級自動切換時，會觸發 [VeLivePlayerObserver](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver) 通訊協定中定義的 [onResolutionSwitch:resolution:error:reason:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onresolutionswitch-resolution-error-reason) 回呼。範例程式碼如下。

   ```objectivec
   - (void)onResolutionSwitch:(TVLManager *)player resolution:(VeLivePlayerResolution)resolution error:(VeLivePlayerError *)error reason:(VeLivePlayerResolutionSwitchReason)reason  {
      // 畫質等級切換回呼。
   }
   ```

## 平滑畫質等級切換

平滑畫質等級切換功能可確保觀眾在手動切換不同畫質等級時，例如超高畫質、高畫質與標準畫質，音訊與視訊能無縫過渡。這可**防止黑畫面或卡頓**，並提升觀看體驗。

若要使用此功能，請為播放器配置來自同一來源、具有多個畫質等級的串流清單，並啟用平滑畫質等級切換。配置後，當觀眾手動切換畫質等級時，播放器會在不同位元率的串流之間平滑過渡，以確保直播音訊與視訊連續且穩定播放。

> **說明**

> 平滑畫質等級切換支援流備援策略。你可以為一組平滑畫質等級切換串流指派相同優先順序，並配置較低優先順序的備援串流。如果較高優先順序的串流群組播放失敗，SDK 會自動嘗試備援群組。如需詳細資訊，請參閱[流備援策略與主備流切換](https://docs.byteplus.com/en/docs/24/107347#stream-fallback-strategy-and-primary-backup-stream-switching)。

> **警告**

* > 平滑畫質等級切換功能目前僅適用於 FLV 串流。

* > 請確保你已整合 Player SDK 1.50.100 或更新版本。

### 前提條件

準備同一來源串流不同畫質等級的拉流位址。

如果你使用 BytePlus MediaLive 的推流位址進行串流，請確保已完成下列操作：

* **新增網域名稱**：在同一網域命名空間下新增推流網域與拉流網域。如需詳細資訊，請參閱[新增網域名稱](https://docs.byteplus.com/docs/byteplus-media-live/docs-domain)。

* **配置轉碼**：在該網域命名空間下為不同畫質等級新增轉碼配置。如需詳細資訊，請參閱[管理轉碼配置](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-transcoding)。

* **取得拉流位址**：取得來源串流與每個轉碼串流的拉流位址。

   * **偵錯用**：使用[位址產生器](https://console.byteplus.com/live/main/locationGenerate)產生拉流位址。

      * **位址類型**：選擇**拉流位址**。

      * **網域名稱**：選擇轉碼配置所使用網域命名空間下的拉流網域。

      * **AppName** 和 **StreamName**：輸入與推流位址相符的 `AppName` 和 `StreamName`。例如，如果推流位址為 `rtmp://push.example.com/live/test?authinfo`，則 `AppName` 為 `live`，`StreamName` 為 `test`。

   * **生產用**：呼叫 [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023)，或使用[服務端 SDK](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-server-sdk) 動態產生拉流位址。

      **範例**

      下表列出不同畫質等級的 FLV 拉流位址與位元率範例。

   |畫質等級 |FLV 拉流位址 |位元率 (kbps) |
   |---|---|---|
   |原畫質 (Origin) |`https://pull.example.com/live/123456.flv` |2500 |
   |超高畫質 (UHD) |`https://pull.example.com/live/123456_uhd.flv` |2500 |
   |高畫質 (HD) |`https://pull.example.com/live/123456_hd.flv` |1000 |
   |標準畫質 (SD) |`https://pull.example.com/live/123456_sd.flv` |800 |
   |低畫質 (LD) |`https://pull.example.com/live/123456_ld.flv` |500 |

### 操作步驟

1. 配置每個畫質等級的串流，並將 [enableSmoothSwitchResolution](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStreamData-enablesmoothswitchresolution) 設為 `YES`，以啟用平滑畫質等級切換。

   ```objectivec
   // 配置每個畫質等級的串流。
   // 原畫質等級。
   VeLivePlayerStream *playStreamOrigin = [[VeLivePlayerStream alloc]init];
   playStreamOrigin.url = @"https://pull.example.com/live/123456.flv"; // 替換為原畫質等級的實際拉流位址。
   playStreamOrigin.format = VeLivePlayerFormatFLV; // 串流格式。
   playStreamOrigin.resolution = VeLivePlayerResolutionOrigin; // 畫質等級識別碼。
   playStreamOrigin.type = VeLivePlayerStreamTypeMain; // 用於區分主流與備流的串流類型。
   playStreamOrigin.bitrate = 2500; // 位元率，單位為 kbps。
   
   // UHD 畫質等級。
   VeLivePlayerStream *playStreamUHD = [[VeLivePlayerStream alloc]init];
   playStreamUHD.url = @"https://pull.example.com/live/123456_uhd.flv"; // 替換為 UHD 畫質等級的實際拉流位址。
   playStreamUHD.format = VeLivePlayerFormatFLV; // 串流格式。
   playStreamUHD.resolution = VeLivePlayerResolutionUHD; // 畫質等級識別碼。
   playStreamUHD.type = VeLivePlayerStreamTypeMain; // 用於區分主流與備流的串流類型。
   playStreamUHD.bitrate = 2500; // 位元率，單位為 kbps。
   
   // HD 畫質等級。
   VeLivePlayerStream *playStreamHD = [[VeLivePlayerStream alloc]init];
   playStreamHD.url = @"https://pull.example.com/live/123456_hd.flv"; // 替換為 HD 畫質等級的實際拉流位址。
   playStreamHD.format = VeLivePlayerFormatFLV; // 串流格式。
   playStreamHD.resolution = VeLivePlayerResolutionHD; // 畫質等級識別碼。
   playStreamHD.type = VeLivePlayerStreamTypeMain; // 用於區分主流與備流的串流類型。
   playStreamHD.bitrate = 1000; // 位元率，單位為 kbps。
   
   // SD 畫質等級。
   VeLivePlayerStream *playStreamSD = [[VeLivePlayerStream alloc]init];
   playStreamSD.url = @"https://pull.example.com/live/123456_sd.flv"; // 替換為 SD 畫質等級的實際拉流位址。
   playStreamSD.format = VeLivePlayerFormatFLV; // 串流格式。
   playStreamSD.resolution = VeLivePlayerResolutionSD; // 畫質等級識別碼。
   playStreamSD.type = VeLivePlayerStreamTypeMain; // 用於區分主流與備流的串流類型。
   playStreamSD.bitrate = 800; // 位元率，單位為 kbps。
   
   // LD 畫質等級。
   VeLivePlayerStream *playStreamLD = [[VeLivePlayerStream alloc]init];
   playStreamLD.url = @"https://pull.example.com/live/123456_ld.flv"; // 替換為 LD 畫質等級的實際拉流位址。
   playStreamLD.format = VeLivePlayerFormatFLV; // 串流格式。
   playStreamLD.resolution = VeLivePlayerResolutionLD; // 畫質等級識別碼。
   playStreamLD.type = VeLivePlayerStreamTypeMain; // 用於區分主流與備流的串流類型。
   playStreamLD.bitrate = 500; // 位元率，單位為 kbps。
   
   // 建立播放來源。
   VeLivePlayerStreamData *streamData = [[VeLivePlayerStreamData alloc]init];
   
   // 新增每個畫質等級的串流。
   NSMutableArray <VeLivePlayerStream *> *mainStreams = [NSMutableArray arrayWithCapacity:5];
   [mainStreams addObject:playStreamOrigin];
   [mainStreams addObject:playStreamUHD];
   [mainStreams addObject:playStreamHD];
   [mainStreams addObject:playStreamSD];
   [mainStreams addObject:playStreamLD];
   streamData.mainStream = mainStreams;
   
   // 配置預設啟動畫質等級。
   streamData.defaultResolution = VeLivePlayerResolutionSD;
   
   // 啟用平滑畫質等級切換。
   streamData.enableSmoothSwitchResolution = YES;
   
   // 配置播放來源。
   [self.livePlayer setPlayStreamData:streamData];
   
   // 開始播放。
   [self.livePlayer play];
   ```

2. 直播期間，當觀眾手動切換畫質等級時，你可以呼叫 [switchResolution:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-switchresolution) 平滑切換畫質等級。範例程式碼如下。

   ```objectivec
   // 切換至 UHD 畫質等級。
   [self.livePlayer switchResolution:VeLivePlayerResolutionUHD];
   ```

3. 新增 [onResolutionSwitch:resolution:error:reason:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onresolutionswitch-resolution-error-reason) 回呼以監聽畫質等級切換結果。當畫質等級變更時，SDK 可觸發此回呼，並傳回切換後的畫質等級和切換原因等資訊。

   ```objectivec
   - (void)onResolutionSwitch:(TVLManager *_Nonnull)player resolution:(VeLivePlayerResolution)resolution error:(VeLivePlayerError *)error reason:(VeLivePlayerResolutionSwitchReason)reason;
   ```

## 擷取快照

此功能可讓你擷取目前影片影格並產生影像。

1. 呼叫 [snapshot](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#snapshot) 拍攝快照。此功能僅在播放期間生效。

```objectivec
int result = [self.livePlayer snapshot];
```

2. 拍攝快照後，會以影像資料觸發 [onSnapshotComplete:image:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#onsnapshotcomplete-image) 回呼函式。

```objectivec
- (void)onSnapshotComplete:(TVLManager *)player image:(UIImage *)image  {
  // 回呼函式透過 image 傳回影像資料。
}
```

## SEI

補充增強資訊 (SEI) 是嵌入直播串流中的其他資料。你可以使用 SEI 傳輸自訂資料或中繼資料。

> **說明**

> 只有進階版和試用版 License 支援 SEI。

### 操作步驟

* 字串 SEI 訊息

   1. 呼叫 [play](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#play) 前，啟用播放器的 [enableSei](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerConfiguration-enablesei) 屬性。啟用此屬性後，播放器會接收字串 SEI 訊息。範例程式碼如下。

      ```objectivec
      // 建立 VeLivePlayerConfiguration 執行個體。
      VeLivePlayerConfiguration *config = [[VeLivePlayerConfiguration alloc]init];
      
      // 啟用接收字串 SEI 訊息。
      config.enableSei = YES;
      
      // 配置播放器的初始設定。
      [self.livePlayer setConfig:config];
      ```

   2. 當播放器接收到字串 SEI 訊息時，會觸發 [onReceiveSeiMessage:message:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onreceiveseimessage-message) 回呼。範例程式碼如下。

      ```objectivec
      - (void)onReceiveSeiMessage:(TVLManager *_Nonnull)player message:(NSString *_Nonnull)message  {
         // 字串 SEI 訊息回呼。
      }
      ```

* 二進位 SEI 訊息

   1. 呼叫 [play](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#play) 前，啟用播放器的 [enableBinarySei](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerConfiguration-enablebinarysei) 屬性。啟用此屬性後，播放器會接收二進位 SEI 訊息，且不再觸發字串 SEI 訊息回呼。範例程式碼如下。

      ```objectivec
      // 建立 VeLivePlayerConfiguration 執行個體。
      VeLivePlayerConfiguration *config = [[VeLivePlayerConfiguration alloc]init];
      
      // 啟用接收二進位 SEI 訊息。
      config.enableBinarySei = YES;
      
      // 配置播放器的初始設定。
      [self.livePlayer setConfig:config];
      ```

   2. 當播放器接收到二進位 SEI 訊息時，會觸發 [onReceiveBinarySeiMessage:message:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onreceivebinaryseimessage-message) 回呼。範例程式碼如下。

      ```objectivec
      - (void)onReceiveBinarySeiMessage:(TVLManager *_Nonnull)player message:(NSData *_Nonnull)message  {
         // 二進位 SEI 訊息回呼。
      }
      ```

## 訂閱視訊資料

透過訂閱解碼後的視訊資料，你可以取得視訊影格資料，以進行自訂處理與渲染。播放器支援多種視訊影格回呼格式，並提供對應的參數與格式選項。

### 前提條件

下表說明視訊影格像素格式與視訊資料封裝格式的列舉值和含義。

|格式類型 |列舉值 |說明 |
|---|---|---|
|視訊影格像素格式 |VeLivePlayerPixelFormatNV12 |NV12 |
|視訊影格像素格式 |VeLivePlayerPixelFormatI420 |I420 |
|視訊資料封裝格式 |VeLivePlayerVideoBufferTypePixelBuffer |CVPixelBufferRef |
|視訊資料封裝格式 |VeLivePlayerVideoBufferTypeSampleBuffer |CVSampleBufferRef |
|視訊資料封裝格式 |VeLivePlayerVideoBufferTypeNSData |NSData |

訂閱視訊資料前，請依需求選擇格式組合。該組合必須遵循下表所示 [VeLivePlayerPixelFormat](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#veliveplayerpixelformat) 與 [VeLivePlayerVideoBufferType](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#veliveplayervideobuffertype) 之間的對應關係。

|像素格式/封裝格式 |VeLivePlayerPixelFormatNV12 |VeLivePlayerPixelFormatI420 |
|---|---|---|
|**VeLivePlayerVideoBufferTypePixelBuffer** |支援（最佳效能） |不支援 |
|**VeLivePlayerVideoBufferTypeSampleBuffer** |支援 |不支援 |
|**VeLivePlayerVideoBufferTypeNSData** |支援 |支援 |

### 操作步驟

1. 呼叫播放器的 [enableVideoFrameObserver:pixelFormat:bufferType:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#enablevideoframeobserver-pixelformat-buffertype) API 以啟用或停用視訊影格資料訂閱。API 參數說明如下表。

   |參數 |類型 |說明 |
   |---|---|---|
   |enable |BOOL |是否啟用視訊影格回呼。 |
   |pixelFormat |VeLivePlayerPixelFormat |視訊影格像素格式。 |
   |bufferType |VeLivePlayerVideoBufferType |視訊資料封裝格式。 |

   範例程式碼如下。

   ```objectivec
   [self.livePlayer enableVideoFrameObserver:YES pixelFormat:VeLivePlayerPixelFormatNV12 bufferType:VeLivePlayerVideoBufferTypePixelBuffer];
   ```

2. SDK 會透過 [VeLivePlayerObserver](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver) 的 [onRenderVideoFrame:videoFrame:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onrendervideoframe-videoframe) 回呼傳回解碼後的視訊影格資料。範例程式碼如下。

   ```objectivec
   - (void)onRenderVideoFrame:(TVLManager *)player videoFrame:(VeLivePlayerVideoFrame *)videoFrame  {
      // 視訊影格資料回呼。
   }
   ```

   [VeLivePlayerVideoFrame](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#veliveplayervideoframe) 參數說明如下表。

   |參數 |類型 |說明 |
   |---|---|---|
   |bufferType |VeLivePlayerVideoBufferType |視訊影格資料封裝格式。 |
   |pixelFormat |VeLivePlayerPixelFormat |視訊影格像素格式。 |
   |width |NSInteger |視訊影格寬度，單位為 px。 |
   |height |NSInteger |視訊影格高度，單位為 px。 |
   |pts |int64_t |視訊影格渲染時間戳記，單位為 ms。 |
   |pixelBuffer |CVPixelBufferRef |當 `bufferType` 為 `VeLivePlayerVideoBufferTypePixelBuffer` 時的視訊資料。 |
   |sampleBuffer |CMSampleBufferRef |當 `bufferType` 為 `VeLivePlayerVideoBufferTypeSampleBuffer` 時的視訊資料。 |
   |data |NSData\* |當 `bufferType` 為 `VeLivePlayerVideoBufferTypeNSData` 時的視訊資料。 |

## 訂閱音訊資料

透過訂閱解碼後的音訊資料，你可以執行自訂音訊處理與渲染。Player SDK 支援訂閱 PCM Float32 取樣格式和 NSData 封裝格式的音訊資料。

|VeLivePlayerAudioBufferType |音訊資料封裝格式 |
|---|---|
|[VeLivePlayerAudioBufferTypeNSData](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#veliveplayeraudiobuffertype) |NSData |

### 操作步驟

1. 呼叫播放器的 [enableAudioFrameObserver:enableRendering:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#enableaudioframeobserver-enablerendering) API，以啟用或停用音訊影格資料訂閱。API 參數說明如下表。

   |參數 |類型 |說明 |
   |---|---|---|
   |enable |BOOL |是否啟用音訊影格回呼。 |
   |enableRendering |BOOL |是否啟用播放器渲染。如果播放器不需要在內部渲染音訊，請將此參數設為 `NO`。 |

   範例程式碼如下。

   ```objectivec
   // 訂閱音訊影格資料，並啟用播放器內部音訊渲染。
   [self.livePlayer enableAudioFrameObserver:YES enableRendering:YES];
   ```

2. SDK 會透過 [VeLivePlayerObserver](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver) 通訊協定中定義的 [onRenderAudioFrame:audioFrame:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onrenderaudioframe-audioframe) 回呼，傳回解碼後的音訊影格資料。範例程式碼如下。

   ```objectivec
   - (void)onRenderAudioFrame:(TVLManager *)player audioFrame:(VeLivePlayerAudioFrame *)audioFrame  {
      // 音訊影格資料回呼。
   }
   ```

   [VeLivePlayerAudioFrame](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#veliveplayeraudioframe) 參數說明如下表。

   |參數 |資料類型 |說明 |
   |---|---|---|
   |bufferType |VeLivePlayerAudioBufferType |音訊影格資料封裝格式。 |
   |sampleRate |int |音訊取樣率，單位為 Hz。 |
   |channels |int |聲道數。 |
   |bitDepth |int |音訊位元深度。 |
   |pts |CMTime |音訊渲染時間戳記，單位為 ms。 |
   |data |NSData\* |PCM 音訊資料。 |
   |samples |int |音訊取樣數。 |

## 超解析度

超解析度 (SR) 是一種從低解析度影像重建高解析度影像的技術。即時 SR 使用演算法即時將低解析度影格重建為高解析度影格。這會產生高解析度影格，然後顯示在螢幕上。SR 可增強影片細節與對比度，提升影片清晰度與觀看體驗。

> **說明**

> 只有進階版和試用版 License 支援 SR。

### 前提條件

從 1.51.300.2\-premium 版本開始，若要使用 SR 功能，整合 Player SDK 時除拉流元件外，還需要新增 `LivePull-BMF` 依賴項。如需詳細資訊，請參閱[整合 iOS 版 Player SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-ios)。

### 操作步驟

1. 從 1.51.300.2\-premium 版本開始，匯入 `VeLivePlayer+SuperResolution.h` 標頭檔。

   **動態函式庫**

```objectivec
   #import <TTSDKFramework/VeLivePlayer+SuperResolution.h>
   ```

   **靜態函式庫**

```objectivec
   #import <TTSDK/VeLivePlayer+SuperResolution.h>
   ```

2. 呼叫播放器的 [setEnableSuperResolution:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#setenablesuperresolution) 方法，以啟用或停用 SR。

   ```objectivec
   [self.livePlayer setEnableSuperResolution:YES];
   ```

   |名稱 |類型 |說明 |
   |---|---|---|
   |enable |BOOL |是否啟用 SR。預設值為 `NO`。<br><br><br>* `YES`：啟用 SR。<br><br>* `NO`：停用 SR。 |

3. 如果啟用 SR 失敗，播放器會透過 [VeLivePlayerObserver](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver) 的 [onStreamFailedOpenSuperResolution:error:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onstreamfailedopensuperresolution-error) 回呼通知你。方法簽章如下。

   ```objectivec
   - (void)onStreamFailedOpenSuperResolution:(TVLManager *_Nonnull)player error:(VeLivePlayerError *_Nullable)error;
   ```

   啟用 SR 失敗的常見原因如下。

   * 實際串流解析度不在 SR 支援範圍內。

   * 實際串流影格率不在 SR 支援範圍內。

   * 目前裝置型號不支援 SR。

## 自訂 HTTP 請求標頭

為播放器的 HTTP 請求設定自訂請求標頭。這通常用於傳輸驗證權杖、Cookie 和服務特定追蹤識別碼等額外資訊。

> **說明**

> 只有 1.50.200.3\-premium 及更新版本支援自訂 HTTP 請求標頭。

### 操作步驟

開始播放前，你可以透過播放器的進階 API [setProperty:value:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setproperty-value) 設定自訂 HTTP 請求標頭。呼叫 `setProperty:value:` 時，需要傳入 `key-value` 配置。

**Key**

|參數名稱 |類型 |說明 |
|---|---|---|
|VeLivePlayerKeySetParamsHttpHeaders |NSString |用於配置自訂 HTTP 請求標頭的屬性鍵。 |

**Value**

此值是包含 `key-value` 配對的 `NSDictionary` 物件，用於設定自訂 HTTP 請求標頭。

* `Key`：`NSString` 類型。請求標頭名稱。

* `Value`：`NSString` 類型。請求標頭值。

範例程式碼如下。

* 設定一個 HTTP 請求標頭

   ```objectivec
   [self.livePlayer setProperty:VeLivePlayerKeySetParamsHttpHeaders value:@{@"key": @"value"}]; // 替換為實際標頭名稱和值。
   ```

* 設定多個 HTTP 請求標頭

   ```objectivec
   [self.livePlayer setProperty:VeLivePlayerKeySetParamsHttpHeaders
                             value:@{
                               @"key1": @"value1", // 替換為實際標頭名稱和值。
                               @"key2": @"value2", // 替換為實際標頭名稱和值。
                               @"key3": @"value3" // 替換為實際標頭名稱和值。
                             }];
   ```

## H.265 硬體解碼與軟體解碼

使用進階版或試用版 License 的 SDK 預設啟用 H.265 硬體解碼與軟體解碼。播放 H.265 編碼的視訊串流時，SDK 會先嘗試使用 H.265 硬體解碼。如果 H.265 硬體解碼失敗，SDK 會自動切換至 H.265 軟體解碼。

呼叫 [play](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#play) 前，請透過播放器的初始配置啟用或停用硬體解碼。範例程式碼如下。

```objectivec
VeLivePlayerConfiguration *config = [VeLivePlayerConfiguration new];
config.enableHardwareDecode = YES;
[self.livePlayer setConfig:config];
```

* `YES`：啟用硬體解碼。

* `NO`：停用硬體解碼，並僅使用軟體解碼。

你可以監聽 [onStatistics:statistics:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onstatistics-statistics) 回呼，並使用 [VeLivePlayerStatistics](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#veliveplayerstatistics) 的 [isHardWareDecode](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerStatistics-ishardwaredecode) 屬性，判斷目前串流是否使用硬體解碼。

## 影片銳化

影片銳化會在裝置本機增強影片，以提升邊緣與紋理細節的清晰度。播放期間，SDK 可即時增強邊緣與紋理細節，使影片看起來更清晰並提升觀看體驗。

> **說明**

> 只有進階版和試用版 License 支援影片銳化。

### 前提條件

從 1.51.300.2\-premium 版本開始，若要使用影片銳化功能，整合 Player SDK 時除拉流元件外，還需要新增 `LivePull-BMF` 依賴項。如需詳細資訊，請參閱[整合 iOS 版 Player SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-ios)。

### 操作步驟

1. 從 1.51.300.2\-premium 版本開始，匯入 `VeLivePlayer+SuperResolution.h` 標頭檔。

   **動態函式庫**

```objectivec
   #import <TTSDKFramework/VeLivePlayer+SuperResolution.h>
   ```

   **靜態函式庫**

```objectivec
   #import <TTSDK/VeLivePlayer+SuperResolution.h>
   ```

2. 呼叫播放器的 [setEnableSharpen:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setenablesharpen) 方法，以啟用或停用影片銳化。

   ```objectivec
   [self.livePlayer setEnableSharpen:YES];
   ```

   |名稱 |類型 |說明 |
   |---|---|---|
   |enable |BOOL |是否啟用影片銳化。預設值為 `NO`。<br><br><br>* `YES`：啟用影片銳化。<br><br>* `NO`：停用影片銳化。 |

3. 如果啟用影片銳化失敗，播放器會透過 [VeLivePlayerObserver](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver) 的 [onError:error:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onerror-error) 回呼通知你。方法簽章如下。

   ```objectivec
   - (void)onError:(TVLManager *_Nonnull)player error:(VeLivePlayerError *_Nonnull)error;
   ```

   啟用影片銳化失敗的常見原因如下。

   * 實際串流解析度不在影片銳化支援範圍內。

   * 實際串流影格率不在影片銳化支援範圍內。

   * 目前裝置型號不支援影片銳化。

   * 目前 License 不支援影片銳化。

## 子母畫面

子母畫面 (PiP) 會將播放器視窗縮小為螢幕角落的小型浮動視窗，讓觀眾在瀏覽其他內容或使用其他應用程式時，仍可繼續觀看直播串流。此功能有助於提升觀看體驗。

### 前提條件

* 你已整合 SDK 1.51.200.4\-premium 或更新版本。

   > **說明**

   > 如果你使用早於 1.51.200.4\-premium 的 SDK 版本，可以整合 PiP 解決方案以啟用 PiP 功能。如需詳細資訊，請參閱 [PiP 解決方案](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#d46ae38e)。

* iOS 15.0 或更新版本。

* 在 Xcode 中，為你的應用程式 Target 啟用 PiP 所需的背景模式。

   1. 在 **Signing & Capabilities** 頁籤上，按一下  **+**  **Capability**，然後按兩下 **Background Modes**。

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f8ccac9b131740cab54e2d294a73885f~tplv-goo7wpa0wc-topic.webp)

   2. 在 **Background Modes** 區段中，選取 **Audio, AirPlay, and Picture in Picture**。

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0782c08333eb411b8f27c201d6968bb3~tplv-goo7wpa0wc-topic.webp)

* 引導觀眾在裝置上啟用系統層級 PiP 設定：前往**設定** \> **一般** \> **子母畫面**，並開啟**自動開始子母畫面**。啟用此設定後，當應用程式進入背景時，PiP 播放可自動開始。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/08beec9cc01b4adb9ca988dc02c4b569~tplv-goo7wpa0wc-topic.webp)

### 操作步驟

1. 匯入 PiP 標頭檔。

   **靜態函式庫整合**

如果你對 SDK 使用靜態函式庫整合，請使用 `#import <TTSDK/VeLivePlayer+PictureInPicture.h>` 匯入 PiP 標頭檔。

   **動態函式庫整合**

如果你對 SDK 使用動態函式庫整合，請使用 `#import <TTSDKFramework/VeLivePlayer+PictureInPicture.h>` 匯入 PiP 標頭檔。

2. 檢查目前裝置是否支援 PiP。

   ```objectivec
   if ([TVLManager isPictureInPictureSupported]) {
       // 根據目前裝置是否支援 PiP 實作你的業務邏輯。
   }
   ```

3. 初始化 SDK 內建播放器並啟用 PiP。PiP 預設為停用。

   ```objectivec
   TVLManager *player = [[TVLManager alloc]initWithType:VeLivePlayerTypeOwn];
   player.enablePictureInPicture = YES;
   ```

   > **說明**

   > PiP 僅受 SDK 內建播放器支援，不受系統播放器支援。

4. 配置應用程式進入背景時 PiP 是否自動開始。此設定僅適用於目前播放器，不會變更觀眾裝置上的系統層級 PiP 設定。

   預設情況下，應用程式進入背景時 PiP 會自動開始。如果你不希望 PiP 自動開始，請將 [canStartPictureInPictureAutomaticallyFromInline](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-canstartpictureinpictureautomaticallyfrominline) 設為 `NO`。下列範例程式碼會啟用應用程式進入背景時自動開始 PiP。

   ```objectivec
   player.canStartPictureInPictureAutomaticallyFromInline = YES;
   ```

5. 如果你希望監聽 PiP 啟動與停止等生命週期事件，可以設定下列 PiP 委派屬性。SDK 已在內部處理 PiP 所需的關鍵委派方法，因此大多數情況下你不需要自行實作。

   ```objectivec
   @property (nonatomic, weak, nullable) id<AVPictureInPictureControllerDelegate> pictureInPictureDelegate;
   @property (nonatomic, weak, nullable) id<AVPictureInPictureSampleBufferPlaybackDelegate> pictureInPicturePlaybackDelegate;
   ```

6. 播放開始後，你可以手動啟動 PiP。

   ```objectivec
   [player startPictureInPicture];
   ```

   如果 PiP 目前處於啟用狀態，你可以手動停止 PiP。

   ```objectivec
   [player stopPictureInPicture];
   ```

7. 若要檢查 PiP 是否已成功啟動，請呼叫下列方法。

   ```objectivec
   BOOL isStarted = [TVLManager isPictureInPictureStarted];
   ```

8. 若要手動更新 PiP 播放按鈕狀態與進度顯示，請呼叫 [invalidatePictureInPicturePlaybackState](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(PictureInPicture)-invalidatepictureinpictureplaybackstate)。SDK 會在內部自動更新播放按鈕狀態與進度顯示，因此大多數情況下你不需要呼叫此方法。

   ```objectivec
   [player invalidatePictureInPicturePlaybackState];
   ```

### PiP 解決方案

如果你使用早於 1.51.200.4\-premium 的 SDK 版本，可以整合 [PiP 解決方案](https://github.com/byteplus-sdk/VeLiveQuickStartDemo/blob/main/VeLivePictureInPicture.podspec)以啟用 PiP 功能。

依需要選擇下列其中一種整合方法：

**線上整合**

```objectivec
pod 'VeLivePictureInPicture', :git => 'https://github.com/byteplus-sdk/VeLiveQuickStartDemo.git', :branch => 'main'
```

**本機整合**

從 [PiP 解決方案](https://github.com/byteplus-sdk/VeLiveQuickStartDemo/blob/main/VeLivePictureInPicture.podspec)複製下列檔案到你的本機專案：

* `VeLivePictureInPicture` 目錄中的原始碼檔案

* `VeLivePictureInPicture.podspec`

`path` 表示這些檔案相對於本機專案中 `Podfile` 的路徑。例如，如果這些檔案位於本機專案中與 `Podfile` 相同的目錄，請將 `path` 設為 `./`。

```objectivec
pod 'VeLivePictureInPicture', :path => './'
```

整合 PiP 解決方案後，你可以使用與 SDK 1.51.200.4\-premium 或更新版本相同的 API。如需詳細資訊，請參閱[操作步驟](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3#97a32559)。

## 進階 API 配置

### 移除 SDK 自動附加的查詢參數

Player SDK 可能會將 `session_id` 等查詢參數附加到拉流位址。這些參數用於識別拉流工作階段，並在排查播放問題時，協助於用戶端與 CDN 記錄中定位同一個工作階段。若要防止 SDK 在實際請求 URL 中包含自動附加的查詢參數，請啟用此功能。啟用此功能後，SDK 附加的查詢參數會從實際請求 URL 中移除，而原始拉流位址中已存在的查詢參數會保留。

> **說明**

> 只有 1.52.1 及更新版本支援移除 SDK 自動附加的查詢參數。

#### 操作步驟

開始播放前，你可以使用播放器的進階 [setProperty:value:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setproperty-value) API，配置是否移除 SDK 自動附加的查詢參數。呼叫 `setProperty:value:` 時，需要傳入 `key-value` 配置。

**Key**

|參數名稱 |類型 |說明 |
|---|---|---|
|VeLivePlayerKeySetParamsRemoveQueryParams |NSString |用於移除 SDK 自動附加查詢參數的屬性鍵。 |

**Value**

`Value` 是 `NSNumber` 值，表示是否移除 SDK 自動附加的查詢參數。預設值為 `0`。

* `1`：移除 SDK 自動附加的查詢參數。

* `0`：保留 SDK 自動附加的查詢參數。

範例程式碼如下。

```objectivec
[self.livePlayer setProperty:@"VeLivePlayerKeySetParamsRemoveQueryParams" value:@1];
```

**效果範例**

例如，拉流位址為：

```text
https://pull.example.com/live/test.flv?auth_key=1779891783-0-0-e1f5a2a****4b5fe21cb3efdc89af901
```

當 SDK 發起播放請求時，會自動附加 `session_id`。

```text
https://pull.example.com/live/test.flv?auth_key=1779891783-0-0-e1f5a2a****4b5fe21cb3efdc89af901&session_id=xxx
```

啟用此功能後，請求 URL 不再包含 `session_id`，但會保留原始拉流位址中的 `auth_key` 鑑權參數：

```text
https://pull.example.com/live/test.flv?auth_key=1779891783-0-0-e1f5a2a****4b5fe21cb3efdc89af901
```
