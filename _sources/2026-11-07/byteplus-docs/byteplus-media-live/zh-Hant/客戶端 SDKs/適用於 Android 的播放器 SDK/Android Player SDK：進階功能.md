---
title: "Android Player SDK：進階功能"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-implementing-advanced-features-2-zh-TW"
---

為提升 Android 應用程式中的觀看體驗，本主題說明如何實作 Android Player SDK 的進階功能。你可以依照實際業務需求，按需實作複雜功能。

## 前提條件

* 你已依照 [Android Player SDK：基本功能](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-basic-features-2)中的說明，實作 Player SDK 的基本功能。

* 若要使用下列功能，請確保使用進階版或試用授權。

   * [播放 RTM 串流](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2#af29cf39)

   * [QUIC 拉流](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2#4d503d05)

   * [播放 CMAF 串流](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2#915c6bb1)

   * [播放低延遲 FLV 串流](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2#1d5784e5)

   * [主備串流切換](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2#77618e0b)

   * [ABR 拉流](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2#5b3ef3d2)

   * [SEI](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2#34e237fb)

   * [超解析度](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2#84bd3b42)

   * [H.265 硬體解碼與軟體解碼](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2#3ca5b85e)

   * [H.266 軟體解碼](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2#71012b84)

   * [影片銳化](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2#15a71a29)

   * 商用 DRM（Digital Rights Management）

   > **警告**

   > 試用授權僅供專案測試使用，且無法續期。試用授權過期會導致驗證失敗，並中斷服務。請在專案上線前升級至正式授權。如需更多資訊，請參閱[將試用授權升級為基本版或進階版授權](https://docs.byteplus.com/docs/byteplus-media-live/managing_sdk_licenses#777c7de7)。

## 注意事項

由於 Player SDK 使用多種 Android 音訊與視訊 API，這些 API 在模擬器上可能無法正常運作，因此建議使用實體裝置進行測試。

## 串流備援策略與主備串流切換

如果你只設定一個拉流位址，當該位址因網路問題或其他例外無法使用時，播放可能卡頓甚至失敗。為降低單一位址例外造成的播放失敗風險，你可以為一次播放工作階段設定多個拉流位址，並依需要選擇下列設定方式之一：

* **串流備援策略**：當你希望播放器依優先順序自動嘗試多個拉流位址時使用。你可以設定每個位址的優先順序與最大重試次數。播放器會先嘗試高優先順序位址。若某個位址在所有重試次數用盡後仍不可用，播放器會切換至下一優先順序的位址。

* **主備串流切換**：當你的應用程式維護獨立的主串流清單與備用串流清單時使用。播放器會先依串流備援策略嘗試主串流清單中的串流。只有在主串流清單中的所有位址都失敗後，播放器才會自動切換到備用串流清單並繼續嘗試。

> **注意**

> 只有進階版與試用授權支援主備串流切換。所有授權類型都可使用串流備援策略。

* 串流備援策略

   主串流或備用串流清單中的播放順序如下：

   1. **播放優先順序最高的串流**：根據你設定的 `priority`，播放器會在目前清單中從最高優先順序到最低優先順序嘗試播放串流。

   2. **失敗時重試**：如果目前串流播放失敗，播放器會根據串流的 `retryMaxCount` 重試。

   3. **切換至備援串流**：如果所有重試都用盡後播放仍失敗，播放器會放棄目前串流，並嘗試目前清單中次高優先順序的串流。

* 主備串流切換

   啟用主備串流切換後，播放器會依下列順序嘗試串流：

   1. **播放主串流**：播放器會先嘗試播放主串流清單中的串流。

   2. **切換至備用串流**：如果主串流清單中的所有串流都播放失敗，播放器會嘗試播放備用串流清單中的串流。

   3. **播放失敗**：如果備用串流清單中的所有串流也播放失敗，播放失敗。

在此過程中，SDK 會使用下列回呼通知你目前狀態：

* [onInfo](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-oninfo)：當某個串流播放失敗但仍存在其他可用串流時觸發。你可以使用此回呼取得詳細錯誤資訊以進行偵錯。

* [onStreamFormatSwitch](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onstreamformatswitch)：當播放器切換串流格式時觸發，例如從 RTM 切換至 FLV。

* [onMainBackupSwitch](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onmainbackupswitch)：當主串流清單中的所有串流都播放失敗，且播放器成功切換到備用串流清單時觸發。

* [onError](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onerror)：當主串流與備用串流清單中的所有串流都播放失敗，且播放最終結束時觸發。

### 前提條件

透過下列任一方式取得 RTM、FLV 等協定的拉流位址。同一清單內的備援順序由每個拉流位址的優先順序決定。

* **用於偵錯**：使用[位址產生器](https://console.byteplus.com/live/main/locationGenerate)產生拉流位址。

* **用於生產環境**：呼叫 [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) 或使用[伺服器端 SDK](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-server-sdk) 動態產生拉流位址。

### 操作步驟

#### 步驟 1：設定備援策略

你可以透過設定 `VeLivePlayerStream` 的 [priority](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStream-priority) 與 [retryMaxCount](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStream-retrymaxcount)，自訂備援策略。

* `priority`：串流的優先順序。值必須為 `0`（預設值）或正整數。**值越大表示優先順序越高**。播放器會優先嘗試播放較高優先順序的串流。

   > **注意**

   > 主串流與備用串流清單的優先順序會獨立計算，且彼此不會影響。

* `retryMaxCount`：串流的最大播放嘗試次數，包含首次嘗試。例如，若值為 `3`，則首次播放失敗後，播放器最多會再重試 2 次。有效值：

   * `-1`（預設值）：使用 `VeLivePlayerConfiguration` 中的 [retryMaxCount](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerConfiguration-retrymaxcount) 值。

   * `0`：不嘗試播放此串流。

   * `>0`：最大播放嘗試次數。

**串流備援策略**

下列程式碼範例示範基本串流備援場景，播放順序如下：

1. 首先，播放器嘗試播放 RTM 串流（優先順序 5），最多嘗試 3 次。

2. 如果失敗，播放器會備援至 FLV 串流（優先順序 4），最多嘗試 2 次。

3. 如果也失敗，播放結束。

```Java
// 建立 VeLivePlayerStreamData 執行個體。
VeLivePlayerStreamData streamData = new VeLivePlayerStreamData();

List<VeLivePlayerStreamData.VeLivePlayerStream> mainStreams = new ArrayList<>();

// 新增 RTM 主串流（最高優先順序）。
VeLivePlayerStreamData.VeLivePlayerStream rtmStream = new VeLivePlayerStreamData.VeLivePlayerStream();
rtmStream.url = "https://xxx.sdp"; // 替換為你的實際 RTM 拉流位址。
rtmStream.format = VeLivePlayerFormatRTM;
rtmStream.streamType = VeLivePlayerDef.VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
rtmStream.retryMaxCount = 3;
rtmStream.priority = 5;
mainStreams.add(rtmStream);

// 新增 FLV 主串流作為備援串流。
VeLivePlayerStreamData.VeLivePlayerStream flvStream = new VeLivePlayerStreamData.VeLivePlayerStream();
flvStream.url = "https://xxx.flv"; // 替換為你的實際 FLV 拉流位址。
flvStream.format = VeLivePlayerFormatFLV;
flvStream.streamType = VeLivePlayerDef.VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
flvStream.retryMaxCount = 2;
flvStream.priority = 4;
mainStreams.add(flvStream);

streamData.mainStreamList = mainStreams;

// 設定播放來源。
mLivePlayer.setPlayStreamData(streamData);

// 開始播放。
mLivePlayer.play();
```

**串流備援策略 + 主備串流切換**

下列程式碼範例示範結合串流備援策略與主備串流切換的場景，播放順序如下：

1. 首先，播放器嘗試播放主串流清單中的 RTM 串流（優先順序 5），最多嘗試 3 次。

2. 如果失敗，播放器會備援至主串流清單中的 FLV 串流（優先順序 4），最多嘗試 2 次。

3. 如果仍失敗，播放器會切換至備用串流清單，並嘗試播放 RTM 串流（優先順序 5），最多嘗試 3 次。

4. 如果失敗，播放器會備援至備用串流清單中的 FLV 串流（優先順序 4），最多嘗試 3 次。

5. 如果所有嘗試都失敗，播放結束。

```Java
// 建立 VeLivePlayerStreamData 執行個體。
VeLivePlayerStreamData streamData = new VeLivePlayerStreamData();

List<VeLivePlayerStreamData.VeLivePlayerStream> mainStreams = new ArrayList<>();

// 新增 RTM 主串流（最高優先順序）。
VeLivePlayerStreamData.VeLivePlayerStream rtmStream = new VeLivePlayerStreamData.VeLivePlayerStream();
rtmStream.url = "https://xxx.sdp"; // 替換為你的實際 RTM 拉流位址。
rtmStream.format = VeLivePlayerDef.VeLivePlayerFormat.VeLivePlayerFormatRTM;
rtmStream.streamType = VeLivePlayerDef.VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
rtmStream.protocol = VeLivePlayerDef.VeLivePlayerProtocol.VeLivePlayerProtocolTLS;
rtmStream.retryMaxCount = 3;
rtmStream.priority = 5;
mainStreams.add(rtmStream);

// 新增 FLV 主串流作為備援串流。
VeLivePlayerStreamData.VeLivePlayerStream flvStream = new VeLivePlayerStreamData.VeLivePlayerStream();
flvStream.url = "https://xxx.flv"; // 替換為你的實際 FLV 拉流位址。
flvStream.format = VeLivePlayerDef.VeLivePlayerFormat.VeLivePlayerFormatFLV;
flvStream.streamType = VeLivePlayerDef.VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
flvStream.protocol = VeLivePlayerDef.VeLivePlayerProtocol.VeLivePlayerProtocolTLS;
flvStream.retryMaxCount = 2;
flvStream.priority = 4;
mainStreams.add(flvStream);

streamData.mainStreamList = mainStreams;

// 設定備用串流清單。
List<VeLivePlayerStreamData.VeLivePlayerStream> backupStreams = new ArrayList<>();
// 新增 RTM 備用串流。
VeLivePlayerStreamData.VeLivePlayerStream rtmBackupStream = new VeLivePlayerStreamData.VeLivePlayerStream();
rtmBackupStream.url = "https://xxx.sdp"; // 替換為你的實際 RTM 拉流位址。
rtmBackupStream.format = VeLivePlayerDef.VeLivePlayerFormat.VeLivePlayerFormatRTM;
rtmBackupStream.streamType = VeLivePlayerDef.VeLivePlayerStreamType.VeLivePlayerStreamTypeBackup;
rtmBackupStream.protocol = VeLivePlayerDef.VeLivePlayerProtocol.VeLivePlayerProtocolTLS;
rtmBackupStream.retryMaxCount = 3;
rtmBackupStream.priority = 5; // 備用串流清單中的最高優先順序。
backupStreams.add(rtmBackupStream);

// 新增 FLV 備用串流作為備援串流。
VeLivePlayerStreamData.VeLivePlayerStream flvBackupStream = new VeLivePlayerStreamData.VeLivePlayerStream();
flvBackupStream.url = "https://xxx.flv"; // 替換為你的實際 FLV 拉流位址。
flvBackupStream.format = VeLivePlayerDef.VeLivePlayerFormat.VeLivePlayerFormatFLV;
flvBackupStream.streamType = VeLivePlayerDef.VeLivePlayerStreamType.VeLivePlayerStreamTypeBackup;
flvBackupStream.protocol = VeLivePlayerDef.VeLivePlayerProtocol.VeLivePlayerProtocolTLS;
flvBackupStream.retryMaxCount = 3;
flvBackupStream.priority = 4;
backupStreams.add(flvBackupStream);
streamData.backupStreamList = backupStreams;

// 啟用主備串流切換。
streamData.enableMainBackupSwitch = true;

// 設定播放來源。
mLivePlayer.setPlayStreamData(streamData);

// 開始播放。
mLivePlayer.play();
```

**多畫質串流備援策略**

串流備援策略支援為多畫質串流設定中的備援串流進行設定，這些設定用於[解析度切換](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2#23c93996)、[ABR 拉流](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2#5b3ef3d2)（僅 FLV 串流），以及[平滑畫質等級切換](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2#d7282079)。設定期間，為同一多畫質串流群組中的串流設定相同的 `priority` 值。播放器會先從最高 `priority` 到最低 `priority` 選擇串流群組。如果高優先順序多畫質串流播放失敗，播放器會備援至較低優先順序串流。

在下列範例中，播放器會先播放 `priority` 為 `5` 的 ABR 多畫質串流。如果 ABR 多畫質串流播放失敗，播放器會備援至 `priority` 為 `4` 的一般 FLV 串流。

```Java
// 建立 VeLivePlayerStreamData 執行個體。
VeLivePlayerStreamData streamData = new VeLivePlayerStreamData();
List<VeLivePlayerStreamData.VeLivePlayerStream> mainStreams = new ArrayList<>();

// 新增 ABR 多畫質串流的原始畫質等級。優先順序為 5。
VeLivePlayerStreamData.VeLivePlayerStream flvOriginStream = new VeLivePlayerStreamData.VeLivePlayerStream();
flvOriginStream.url = "https://xxx_origin.flv"; // 替換為原始畫質等級的實際 FLV 拉流位址。
flvOriginStream.format = VeLivePlayerDef.VeLivePlayerFormat.VeLivePlayerFormatFLV;
flvOriginStream.streamType = VeLivePlayerDef.VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
flvOriginStream.protocol = VeLivePlayerDef.VeLivePlayerProtocol.VeLivePlayerProtocolTLS;
flvOriginStream.resolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionOrigin); // 原始畫質等級。
flvOriginStream.bitrate = 2000;
flvOriginStream.retryMaxCount = 3;
flvOriginStream.priority = 5;
mainStreams.add(flvOriginStream);

// 新增 ABR 多畫質串流的 UHD 畫質等級。優先順序為 5。
VeLivePlayerStreamData.VeLivePlayerStream flvUHDStream = new VeLivePlayerStreamData.VeLivePlayerStream();
flvUHDStream.url = "https://xxx_uhd.flv"; // 替換為 UHD 畫質等級的實際 FLV 拉流位址。
flvUHDStream.format = VeLivePlayerDef.VeLivePlayerFormat.VeLivePlayerFormatFLV;
flvUHDStream.streamType = VeLivePlayerDef.VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
flvUHDStream.protocol = VeLivePlayerDef.VeLivePlayerProtocol.VeLivePlayerProtocolTLS;
flvUHDStream.resolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionUHD); // UHD 畫質等級。
flvUHDStream.bitrate = 1800;
flvUHDStream.retryMaxCount = 3;
flvUHDStream.priority = 5;
mainStreams.add(flvUHDStream);

// 新增 ABR 多畫質串流的 HD 畫質等級。優先順序為 5。
VeLivePlayerStreamData.VeLivePlayerStream flvHDStream = new VeLivePlayerStreamData.VeLivePlayerStream();
flvHDStream.url = "https://xxx_hd.flv"; // 替換為 HD 畫質等級的實際 FLV 拉流位址。
flvHDStream.format = VeLivePlayerDef.VeLivePlayerFormat.VeLivePlayerFormatFLV;
flvHDStream.streamType = VeLivePlayerDef.VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
flvHDStream.protocol = VeLivePlayerDef.VeLivePlayerProtocol.VeLivePlayerProtocolTLS;
flvHDStream.resolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionHD); // HD 畫質等級。
flvHDStream.bitrate = 1500;
flvHDStream.retryMaxCount = 3;
flvHDStream.priority = 5;
mainStreams.add(flvHDStream);

// 新增一般 FLV 串流作為備援串流。優先順序為 4。
VeLivePlayerStreamData.VeLivePlayerStream flvStream = new VeLivePlayerStreamData.VeLivePlayerStream();
flvStream.url = "https://xxx.flv"; // 替換為你的實際 FLV 拉流位址。
flvStream.format = VeLivePlayerDef.VeLivePlayerFormat.VeLivePlayerFormatFLV;
flvStream.streamType = VeLivePlayerDef.VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
flvStream.protocol = VeLivePlayerDef.VeLivePlayerProtocol.VeLivePlayerProtocolTLS;
flvStream.retryMaxCount = 2;
flvStream.priority = 4;
mainStreams.add(flvStream);

streamData.mainStreamList = mainStreams;

// 設定預設啟動畫質等級。
streamData.defaultResolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionOrigin);

// 啟用 ABR。
streamData.enableABR = true;

// 設定播放來源。
mLivePlayer.setPlayStreamData(streamData);

// 開始播放。
mLivePlayer.play();
```

#### 步驟 2：新增回呼

視需要新增下列回呼，以監聽備援過程中的事件。

* 監聽串流格式切換，例如從 RTM 切換至 FLV。

   ```Java
   @Override
   public void onStreamFormatSwitch(
       VeLivePlayer player,
       VeLivePlayerFormat fromStreamFormat,
       VeLivePlayerFormat toStreamFormat,
       VeLivePlayerError error,
       Bundle extraInfo
   ) {
   }
   ```

* 監聽播放期間遇到的可復原問題。當某個串流播放失敗，但 SDK 即將執行復原動作時會觸發此回呼，例如切換至備援串流。這表示播放仍在繼續，你不需要中斷播放流程。偵錯期間，你可以使用傳回的錯誤資訊，了解串流播放失敗的具體原因。

   ```Java
   @Override
   public void onInfo(
       VeLivePlayer player,
       VeLivePlayerError error
   ) {
   }
   ```

* 監聽從主串流切換至備用串流。

   ```Java
   @Override
   public void onMainBackupSwitch(
       VeLivePlayer player,
       VeLivePlayerStreamType streamType,
       VeLivePlayerError error
   ) {
   }
   ```

* 監聽播放最終結束，也就是所有串流都播放失敗。

   ```Java
   @Override
   public void onError(
       VeLivePlayer player,
       VeLivePlayerError error
   ) {
   }
   ```

## 播放 RTM 串流

播放 RTM 串流可將直播延遲降低至 1\-2 秒，為觀眾提供高品質直播體驗。

但是，RTM 的超低延遲功能也對網路環境提出更高要求。在不穩定的網路條件下，可能發生播放延遲、卡頓或失敗。如果你想在 RTM 拉流位址不可用時，自動嘗試 FLV 等其他協定的拉流位址，請搭配串流備援策略或主備串流切換使用此功能。如需更多資訊，請參閱[串流備援策略與主備串流切換](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2#77618e0b)。

> **注意**

> 只有進階版與試用授權支援播放 RTM 串流。

### 前提條件

* 確保已整合 Player SDK 1.50.100 或更新版本。

* 透過下列任一方式取得 RTM、FLV 等協定的拉流位址。

   * **用於偵錯**：使用[位址產生器](https://console.byteplus.com/live/main/locationGenerate)產生拉流位址。

   * **用於生產環境**：呼叫 [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) 或使用[伺服器端 SDK](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-server-sdk) 動態產生拉流位址。

### 操作步驟

本主題提供下列兩個程式碼範例，分別對應由簡到繁的場景：

* **基本場景**：示範當主串流清單中的高優先順序 RTM 串流播放失敗時，如何自動備援至 FLV 等其他協定的串流。

* **進階場景**：在基本場景上新增主備串流切換機制。當主串流清單中的所有串流（包含 RTM 串流與備援串流）都不可用時，播放器會自動切換至備用串流清單並重試。

建議你先從基本場景開始。

**基本場景**

下列程式碼範例示範基本串流備援場景，播放順序如下：

1. 首先，播放器嘗試播放 RTM 串流（優先順序 5），最多嘗試 3 次。

2. 如果失敗，播放器會備援至 FLV 串流（優先順序 4），最多嘗試 2 次。

3. 如果也失敗，播放結束。

```Java
// 建立 VeLivePlayerStreamData 執行個體。
VeLivePlayerStreamData streamData = new VeLivePlayerStreamData();

List<VeLivePlayerStreamData.VeLivePlayerStream> mainStreams = new ArrayList<>();

// 新增 RTM 主串流（最高優先順序）。
VeLivePlayerStreamData.VeLivePlayerStream rtmStream = new VeLivePlayerStreamData.VeLivePlayerStream();
rtmStream.url = "https://xxx.sdp"; // 替換為你的實際 RTM 拉流位址。
rtmStream.format = VeLivePlayerFormatRTM;
rtmStream.streamType = VeLivePlayerDef.VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
rtmStream.retryMaxCount = 3;
rtmStream.priority = 5;
mainStreams.add(rtmStream);

// 新增 FLV 主串流作為備援串流。
VeLivePlayerStreamData.VeLivePlayerStream flvStream = new VeLivePlayerStreamData.VeLivePlayerStream();
flvStream.url = "https://xxx.flv"; // 替換為你的實際 FLV 拉流位址。
flvStream.format = VeLivePlayerFormatFLV;
flvStream.streamType = VeLivePlayerDef.VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
flvStream.retryMaxCount = 2;
flvStream.priority = 4;
mainStreams.add(flvStream);

streamData.mainStreamList = mainStreams;

// 設定播放來源。
mLivePlayer.setPlayStreamData(streamData);

// 開始播放。
mLivePlayer.play();
```

**進階場景**

下列程式碼範例示範結合串流備援策略與主備串流切換的場景，播放順序如下：

1. 首先，播放器嘗試播放主串流清單中的 RTM 串流（優先順序 5），最多嘗試 3 次。

2. 如果失敗，播放器會備援至主串流清單中的 FLV 串流（優先順序 4），最多嘗試 2 次。

3. 如果仍失敗，播放器會切換至備用串流清單，並嘗試播放 RTM 串流（優先順序 5），最多嘗試 3 次。

4. 如果失敗，播放器會備援至備用串流清單中的 FLV 串流（優先順序 4），最多嘗試 3 次。

5. 如果所有嘗試都失敗，播放結束。

```Java
// 建立 VeLivePlayerStreamData 執行個體。
VeLivePlayerStreamData streamData = new VeLivePlayerStreamData();

List<VeLivePlayerStreamData.VeLivePlayerStream> mainStreams = new ArrayList<>();

// 新增 RTM 主串流（最高優先順序）。
VeLivePlayerStreamData.VeLivePlayerStream rtmStream = new VeLivePlayerStreamData.VeLivePlayerStream();
rtmStream.url = "https://xxx.sdp"; // 替換為你的實際 RTM 拉流位址。
rtmStream.format = VeLivePlayerDef.VeLivePlayerFormat.VeLivePlayerFormatRTM;
rtmStream.streamType = VeLivePlayerDef.VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
rtmStream.protocol = VeLivePlayerDef.VeLivePlayerProtocol.VeLivePlayerProtocolTLS;
rtmStream.retryMaxCount = 3;
rtmStream.priority = 5;
mainStreams.add(rtmStream);

// 新增 FLV 主串流作為備援串流。
VeLivePlayerStreamData.VeLivePlayerStream flvStream = new VeLivePlayerStreamData.VeLivePlayerStream();
flvStream.url = "https://xxx.flv"; // 替換為你的實際 FLV 拉流位址。
flvStream.format = VeLivePlayerDef.VeLivePlayerFormat.VeLivePlayerFormatFLV;
flvStream.streamType = VeLivePlayerDef.VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
flvStream.protocol = VeLivePlayerDef.VeLivePlayerProtocol.VeLivePlayerProtocolTLS;
flvStream.retryMaxCount = 2;
flvStream.priority = 4;
mainStreams.add(flvStream);

streamData.mainStreamList = mainStreams;

// 設定備用串流清單。
List<VeLivePlayerStreamData.VeLivePlayerStream> backupStreams = new ArrayList<>();
// 新增 RTM 備用串流。
VeLivePlayerStreamData.VeLivePlayerStream rtmBackupStream = new VeLivePlayerStreamData.VeLivePlayerStream();
rtmBackupStream.url = "https://xxx.sdp"; // 替換為你的實際 RTM 拉流位址。
rtmBackupStream.format = VeLivePlayerDef.VeLivePlayerFormat.VeLivePlayerFormatRTM;
rtmBackupStream.streamType = VeLivePlayerDef.VeLivePlayerStreamType.VeLivePlayerStreamTypeBackup;
rtmBackupStream.protocol = VeLivePlayerDef.VeLivePlayerProtocol.VeLivePlayerProtocolTLS;
rtmBackupStream.retryMaxCount = 3;
rtmBackupStream.priority = 5; // 備用串流清單中的最高優先順序。
backupStreams.add(rtmBackupStream);

// 新增 FLV 備用串流作為備援串流。
VeLivePlayerStreamData.VeLivePlayerStream flvBackupStream = new VeLivePlayerStreamData.VeLivePlayerStream();
flvBackupStream.url = "https://xxx.flv"; // 替換為你的實際 FLV 拉流位址。
flvBackupStream.format = VeLivePlayerDef.VeLivePlayerFormat.VeLivePlayerFormatFLV;
flvBackupStream.streamType = VeLivePlayerDef.VeLivePlayerStreamType.VeLivePlayerStreamTypeBackup;
flvBackupStream.protocol = VeLivePlayerDef.VeLivePlayerProtocol.VeLivePlayerProtocolTLS;
flvBackupStream.retryMaxCount = 3;
flvBackupStream.priority = 4;
backupStreams.add(flvBackupStream);
streamData.backupStreamList = backupStreams;

// 啟用主備串流切換。
streamData.enableMainBackupSwitch = true;

// 設定播放來源。
mLivePlayer.setPlayStreamData(streamData);

// 開始播放。
mLivePlayer.play();
```

## 播放 CMAF 串流

CMAF（Common Media Application Format）是一種專為分段傳遞媒體設計的封裝格式。播放 CMAF 串流時，播放器會從 `.mpd` 拉流位址擷取播放資訊清單，然後拉取對應的音訊與視訊片段進行直播播放。

> **注意**

> 只有進階版與試用授權支援播放 CMAF 串流。

### 前提條件

透過下列任一方式取得來源串流的 `.mpd` 拉流位址。

* **用於偵錯**：使用[位址產生器](https://console.byteplus.com/live/main/locationGenerate)產生 `.mpd` 拉流位址。

* **用於生產環境**：呼叫 [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) 或使用[伺服器端 SDK](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-server-sdk) 動態產生 `.mpd` 拉流位址。

> **警告**

> 只有來源串流的 `.mpd` 拉流位址支援 CMAF 播放。ABR 串流的 `.mpd` 拉流位址不支援 CMAF 播放。

### 操作步驟

* 使用 `.mpd` 拉流位址呼叫 [setPlayUrl](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setplayurl) 方法進行播放。播放器會自動將串流識別為 CMAF 串流，不需要額外設定格式。

   ```Java
   mLivePlayer.setPlayUrl("https://pull.example.com/live/stream/index.mpd"); // 替換為你的實際 .mpd 拉流位址。
   
   // 開始播放。
   mLivePlayer.play();
   ```

* 呼叫 [setPlayStreamData](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setplaystreamdata) 方法設定一個或多個拉流位址，並明確將串流格式設為 `VeLivePlayerFormatCMAF`。下列範例程式碼使用 CMAF 串流作為主串流。

   ```Java
   VeLivePlayerStreamData.VeLivePlayerStream stream = new VeLivePlayerStreamData.VeLivePlayerStream();
   stream.url = "https://pull.example.com/live/stream/index.mpd"; // 替換為你的實際 .mpd 拉流位址。
   stream.format = VeLivePlayerDef.VeLivePlayerFormat.VeLivePlayerFormatCMAF; // 明確將串流格式設為 VeLivePlayerFormatCMAF。
   stream.streamType = VeLivePlayerDef.VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
   // 建立 VeLivePlayerStreamData 執行個體。
   VeLivePlayerStreamData streamData = new VeLivePlayerStreamData();
   streamData.mainStreamList = new ArrayList<>();
   // 新增 CMAF 串流。
   streamData.mainStreamList.add(stream);
   // 將播放來源的預設串流格式設為 CMAF。
   streamData.defaultFormat = VeLivePlayerDef.VeLivePlayerFormat.VeLivePlayerFormatCMAF;
   // 設定播放來源。
   mLivePlayer.setPlayStreamData(streamData);
   // 開始播放。
   mLivePlayer.play();
   ```

## 播放低延遲 FLV 串流

啟用低延遲 FLV 串流後，FLV 拉流可將直播延遲降低至 2\-3 秒。

> **注意**

> 若要播放低延遲 FLV 串流，請確保已整合 SDK 1.50.200.3 或更新版本，並使用進階版或試用授權。

### 操作步驟

開始播放前，你可以透過播放器的進階 API [setProperty](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setproperty) 啟用低延遲 FLV 串流。呼叫 `setProperty` 時，你需要傳入 `key-value` 設定。

**Key**

|參數名稱 |類型 |說明 |
|---|---|---|
|VeLivePlayerKeySetParamsLowLatencyFLV |[VeLivePlayerProperty](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerProperty) |低延遲 FLV 串流功能的屬性鍵。 |

**Value**

該值是包含 `key-value` 配對的 `JSONObject` 物件，用於設定低延遲 FLV 串流功能。

* `Key`：`String` 類型。值固定為 `EnableLowLatencyFLV`，表示是否啟用低延遲 FLV 串流功能。

* `Value`：`Integer` 類型。值為 `1` 會啟用低延遲 FLV 串流功能，值為 `0` 會停用該功能。預設值為 `0`。

範例程式碼如下。

```Java
JSONObject flv2s = new JSONObject();
flv2s.put("EnableLowLatencyFLV", 1);
mLivePlayer.setProperty(VeLivePlayerProperty.VeLivePlayerKeySetParamsLowLatencyFLV, flv2s);
```

## QUIC 拉流

Player SDK 支援 QUIC 拉流。此功能應搭配 BytePlus MediaLive 使用。

> **注意**

> 只有進階版與試用授權支援 QUIC 拉流。

### 前提條件

在 BytePlus Live 控制台中使用[位址產生器](https://console.byteplus.com/live/main/locationGenerate)產生 FLV 拉流位址。

### 操作步驟

設定 QUIC 拉流位址並開始播放。範例程式碼如下。

```Java
VeLivePlayerStreamData.VeLivePlayerStream playStreamFLV = new VeLivePlayerStreamData.VeLivePlayerStream();
playStreamFLV.url = "https://pull.example.com/live/stream.flv"; // 替換為你的實際 FLV 拉流位址。
playStreamFLV.format = VeLivePlayerFormatFLV;
playStreamFLV.protocol = VeLivePlayerProtocolQUIC;
playStreamFLV.resolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionOrigin);
playStreamFLV.streamType = VeLivePlayerStreamTypeMain;

// 建立 VeLivePlayerStreamData 執行個體。
VeLivePlayerStreamData streamData = new VeLivePlayerStreamData();
streamData.mainStreamList = new ArrayList<>();

// 新增 FLV 串流。
streamData.mainStreamList.add(playStreamFLV);

// 設定播放來源。
mLivePlayer.setPlayStreamData(streamData);

// 開始播放。
mLivePlayer.play();
```

> **注意**

> Player SDK 預設啟用 QUIC 失敗備援策略。如果 QUIC 拉流失敗，SDK 會自動備援至 TCP 拉流。

## 使用 IP 位址拉流

播放器支援使用網域的 IP 位址進行拉流，以降低首幀時間。

### 前提條件

取得拉流位址並解析其 IP 位址。

### 注意事項

* 使用 [setUrlHostIP](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-seturlhostip) 對應網域名稱與 IP 位址時，請在初始設定中將 [enableLiveDNS](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-keytype#enablelivedns) 設為 `false`，以停用 DNS 預解析功能。

* 呼叫 [play](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-play) 開始播放前，請先呼叫 [setUrlHostIP](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-seturlhostip) 設定網域到 IP 的對應。

### 操作步驟

使用播放器的 [setUrlHostIP](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-seturlhostip) API 將 IP 位址與網域名稱建立關聯。播放器隨後會直接使用 IP 位址進行拉流。範例程式碼如下。

```Java
mLivePlayer.setPlayUrl("https://pull.example.com/live/stream.flv"); // 替換為你的實際拉流位址。
// 將拉流位址中的網域對應到其解析後的 IP 位址。
List<String> valueList = new ArrayList<>();
valueList.add("xxx.xxx.xxx.xxx"); // 替換為從網域解析出的實際 IP 位址。
Map<String, List<String>> map = new HashMap<>();
map.put("pull.example.com", valueList); // 將 pull.example.com 替換為你實際拉流位址中的網域。

// 設定網域到 IP 的對應。
mLivePlayer.setUrlHostIP(map);

// 開始播放。
mLivePlayer.play();
```

## 解析度切換

你可以設定多個不同解析度的拉流位址，並在播放期間於這些位址之間切換。

> **注意**

> 解析度切換支援串流備援策略。你可以為一組多解析度串流指定相同優先順序，並設定較低優先順序的備援串流。如果較高優先順序串流群組播放失敗，SDK 會自動嘗試備援群組。如需更多資訊，請參閱[串流備援策略與主備串流切換](https://docs.byteplus.com/en/docs/24/107292#stream-fallback-strategy-and-primary-backup-stream-switching)。

### 前提條件

取得不同解析度的拉流位址。如果你使用 BytePlus MediaLive 提供的直播服務，請執行下列操作：

1. [設定轉碼任務](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-transcoding)，以產生多個不同解析度的轉碼串流。

2. 透過下列任一方式取得原始串流與轉碼串流的拉流位址。

   * **用於偵錯**：使用[位址產生器](https://console.byteplus.com/live/main/locationGenerate)產生拉流位址。

   * **用於生產環境**：呼叫 [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) 或使用[伺服器端 SDK](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-server-sdk) 動態產生拉流位址。

此流程使用下列拉流位址作為範例。

|**解析度** |**拉流位址** |
|---|---|
|原始（Origin） |`https://pull.example.com/live/123456.flv` |
|超高畫質（UHD） |`https://pull.example.com/live/123456_uhd.flv` |
|高畫質（HD） |`https://pull.example.com/live/123456_hd.flv` |
|標準畫質（SD） |`https://pull.example.com/live/123456_sd.flv` |
|低畫質（LD） |`https://pull.example.com/live/123456_ld.flv` |

### 操作步驟

1. 設定多解析度拉流位址並開始播放。範例程式碼如下。

   ```Java
   // 設定多個畫質等級的拉流位址。
   VeLivePlayerStreamData.VeLivePlayerStream playStreamOrigin = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamOrigin.url = "https://pull.example.com/live/123456.flv"; // 替換為原始畫質等級的實際拉流位址。
   playStreamOrigin.format = VeLivePlayerFormatFLV;
   playStreamOrigin.resolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionOrigin); // 原始畫質等級。
   playStreamOrigin.streamType = VeLivePlayerStreamTypeMain;
   
   VeLivePlayerStreamData.VeLivePlayerStream playStreamUHD = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamUHD.url = "https://pull.example.com/live/123456_uhd.flv"; // 替換為 UHD 畫質等級的實際拉流位址。
   playStreamUHD.format = VeLivePlayerFormatFLV;
   playStreamUHD.resolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionUHD); // UHD 畫質等級。
   playStreamUHD.streamType = VeLivePlayerStreamTypeMain;
   
   VeLivePlayerStreamData.VeLivePlayerStream playStreamHD = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamHD.url = "https://pull.example.com/live/123456_hd.flv"; // 替換為 HD 畫質等級的實際拉流位址。
   playStreamHD.format = VeLivePlayerFormatFLV;
   playStreamHD.resolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionHD); // HD 畫質等級。
   playStreamHD.streamType = VeLivePlayerStreamTypeMain;
   
   VeLivePlayerStreamData.VeLivePlayerStream playStreamSD = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamSD.url = "https://pull.example.com/live/123456_sd.flv"; // 替換為 SD 畫質等級的實際拉流位址。
   playStreamSD.format = VeLivePlayerFormatFLV;
   playStreamSD.resolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionSD); // SD 畫質等級。
   playStreamSD.streamType = VeLivePlayerStreamTypeMain;
   
   VeLivePlayerStreamData.VeLivePlayerStream playStreamLD = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamLD.url = "https://pull.example.com/live/123456_ld.flv"; // 替換為 LD 畫質等級的實際拉流位址。
   playStreamLD.format = VeLivePlayerFormatFLV;
   playStreamLD.resolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionLD); // LD 畫質等級。
   playStreamLD.streamType = VeLivePlayerStreamTypeMain;
   
   // 建立 VeLivePlayerStreamData 執行個體。
   VeLivePlayerStreamData streamData = new VeLivePlayerStreamData();
   
   // 新增拉流位址。
   streamData.mainStreamList = new ArrayList<>();
   streamData.mainStreamList.add(playStreamOrigin);
   streamData.mainStreamList.add(playStreamUHD);
   streamData.mainStreamList.add(playStreamHD);
   streamData.mainStreamList.add(playStreamSD);
   streamData.mainStreamList.add(playStreamLD);
   
   // 將預設解析度設為原始。
   streamData.defaultResolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionOrigin);
   
   // 傳入拉流設定。
   mLivePlayer.setPlayStreamData(streamData);
   
   // 開始播放。
   mLivePlayer.play();
   ```

2. 呼叫 [switchResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-switchresolution) 變更解析度。

   ```Java
   mLivePlayer.switchResolution(new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionUHD)); // 切換至 UHD 畫質等級。
   ```

3. 切換成功時，會觸發 [onResolutionSwitch](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onresolutionswitch) 回呼函式。

   ```Java
   public void onResolutionSwitch(VeLivePlayer player, VeLivePlayerDef.VeLivePlayerResolution resolution, VeLivePlayerError error, VeLivePlayerDef.VeLivePlayerResolutionSwitchReason reason) {
     // 解析度切換完成時觸發。
   }
   ```

## ABR 拉流

自適應位元率（ABR）拉流可在網路條件變化時切換至更合適的畫質等級，協助維持流暢播放。

> **注意**

* > ABR 拉流支援 **RTM\-ABR 串流**與 **FLV 串流**。

* > 只有進階版與試用授權支援 ABR 拉流。

* > ABR 拉流支援串流備援策略。對於 RTM\-ABR 串流，你可以將 RTM\-ABR 拉流位址作為備援策略中的 RTM 串流使用。對於 FLV 串流，請為一個 ABR 串流群組中的所有畫質等級指定相同優先順序，並設定較低優先順序的備援串流。如果較高優先順序 ABR 串流群組播放失敗，SDK 會自動嘗試備援群組。如需更多資訊，請參閱[串流備援策略與主備串流切換](https://docs.byteplus.com/en/docs/24/107292#stream-fallback-strategy-and-primary-backup-stream-switching)。

目前，Android Player SDK 支援下列 ABR 模式：

* **RTM\-ABR 串流**：用於 RTM 播放的伺服器端 ABR 能力。播放器只使用**一個** RTM\-ABR 拉流位址，伺服器會根據觀眾的網路條件自動選擇並切換畫質等級。這有助於減少弱網路環境下的卡頓，同時保留 RTM 的低延遲播放體驗。

* **FLV 串流**：用戶端 ABR 能力。你提供多個 FLV 拉流位址與位元率資訊，SDK 會根據網路條件在它們之間切換。

### RTM\-ABR 串流

> **警告**

> 只有 1.51.100.8 及更新版本支援 RTM\-ABR 串流。

#### 前提條件

* 設定多個 ABR 子串流，並在新增 ABR 設定時選取 **RTM\-ABR** 作為**協定類型**。如需更多資訊，請參閱[管理自適應位元率設定](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-an-hls-abr-task)。

* 透過下列任一方式取得 RTM\-ABR 拉流位址。

   * **用於偵錯**：使用[位址產生器](https://console.byteplus.com/live/main/locationGenerate)，並選取啟動畫質等級（尾碼），以在**自適應位元率**分頁取得 **RTM 位址**。如需更多資訊，請參閱[產生串流位址](https://docs.byteplus.com/docs/byteplus-media-live/docs-address-generator)。

   * **用於生產環境**：呼叫 [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) 或使用[伺服器端 SDK](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-server-sdk)，動態產生 RTM\-ABR 拉流位址。不同尾碼對應不同啟動畫質等級。使用這些位址之一開始播放。請確保 `Protocol` 的值為 `udp`。

   > **警告**

   > 請勿手動將 `rtmabr=true` 附加到一般 RTM 拉流位址。只有在完成 RTM\-ABR 設定並使用產生的 RTM\-ABR 位址後，RTM\-ABR 才會生效。

#### 操作步驟

設定 **RTM\-ABR** 拉流位址並開始播放。

```Java
mLivePlayer.setPlayUrl("https://pull.example.com/live/test_uhd.sdp?rtmabr=true"); // 替換為你的實際 RTM-ABR 拉流位址。

// 開始播放。
mLivePlayer.play();
```

### FLV 串流

#### 前提條件

取得來源串流與各畫質等級轉碼串流的拉流位址。如果你使用 BytePlus MediaLive，請登入控制台並完成[轉碼設定](https://console.byteplus.com/live/main/application/transcode)，再取得拉流位址。你可以透過下列任一方式取得位址：

* **用於偵錯**：使用[位址產生器](https://console.byteplus.com/live/main/locationGenerate)產生拉流位址。

* **用於生產環境**：呼叫 [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) 或使用[伺服器端 SDK](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-server-sdk) 動態產生拉流位址。

此流程使用下列拉流位址作為範例。

|畫質等級 |拉流位址 |位元率（kbps） |
|---|---|---|
|原始（Origin） |`https://pull.example.com/live/123456.flv` |2500 |
|超高畫質（UHD） |`https://pull.example.com/live/123456_uhd.flv` |2500 |
|高畫質（HD） |`https://pull.example.com/live/123456_hd.flv` |1000 |
|標準畫質（SD） |`https://pull.example.com/live/123456_sd.flv` |800 |
|低畫質（LD） |`https://pull.example.com/live/123456_ld.flv` |500 |

> **警告**

> 為 ABR 設定多個畫質等級拉流位址時，SDK 中每個畫質等級的編碼位元率必須與[轉碼設定](https://console.byteplus.com/live/main/application/transcode)中設定的編碼位元率相同。如需更多資訊，請參閱[管理轉碼設定](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-transcoding)。

#### 操作步驟

1. 設定多畫質拉流位址並開始播放。範例程式碼如下。

   ```Java
   // 設定多個畫質等級的拉流位址。
   VeLivePlayerStreamData.VeLivePlayerStream playStreamOrigin = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamOrigin.url = "https://pull.example.com/live/123456.flv"; // 替換為原始畫質等級的實際拉流位址。
   playStreamOrigin.format = VeLivePlayerFormatFLV;
   playStreamOrigin.resolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionOrigin); // 原始畫質等級。
   playStreamOrigin.streamType = VeLivePlayerStreamTypeMain;
   playStreamOrigin.bitrate = 2500;
   
   VeLivePlayerStreamData.VeLivePlayerStream playStreamUHD = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamUHD.url = "https://pull.example.com/live/123456_uhd.flv"; // 替換為 UHD 畫質等級的實際拉流位址。
   playStreamUHD.format = VeLivePlayerFormatFLV;
   playStreamUHD.resolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionUHD); // UHD 畫質等級。
   playStreamUHD.streamType = VeLivePlayerStreamTypeMain;
   playStreamUHD.bitrate = 2500;
   
   VeLivePlayerStreamData.VeLivePlayerStream playStreamHD = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamHD.url = "https://pull.example.com/live/123456_hd.flv"; // 替換為 HD 畫質等級的實際拉流位址。
   playStreamHD.format = VeLivePlayerFormatFLV;
   playStreamHD.resolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionHD); // HD 畫質等級。
   playStreamHD.streamType = VeLivePlayerStreamTypeMain;
   playStreamHD.bitrate = 1000;
   
   VeLivePlayerStreamData.VeLivePlayerStream playStreamSD = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamSD.url = "https://pull.example.com/live/123456_sd.flv";  // 替換為 SD 畫質等級的實際拉流位址。
   playStreamSD.format = VeLivePlayerFormatFLV;
   playStreamSD.resolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionSD); // SD 畫質等級。
   playStreamSD.streamType = VeLivePlayerStreamTypeMain;
   playStreamSD.bitrate = 800;
   
   VeLivePlayerStreamData.VeLivePlayerStream playStreamLD = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamLD.url = "https://pull.example.com/live/123456_ld.flv";  // 替換為 LD 畫質等級的實際拉流位址。
   playStreamLD.format = VeLivePlayerFormatFLV;
   playStreamLD.resolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionLD); // LD 畫質等級。
   playStreamLD.streamType = VeLivePlayerStreamTypeMain;
   playStreamLD.bitrate = 500;
   
   // 建立 VeLivePlayerStreamData 執行個體。
   VeLivePlayerStreamData streamData = new VeLivePlayerStreamData();
   
   // 新增多畫質串流。
   streamData.mainStreamList = new ArrayList<>();
   streamData.mainStreamList.add(playStreamOrigin);
   streamData.mainStreamList.add(playStreamUHD);
   streamData.mainStreamList.add(playStreamHD);
   streamData.mainStreamList.add(playStreamSD);
   streamData.mainStreamList.add(playStreamLD);
   
   // 設定預設啟動畫質等級。
   streamData.defaultResolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionOrigin);
   
   // 啟用 ABR。
   streamData.enableABR = true;
   
   // 設定播放來源。
   mLivePlayer.setPlayStreamData(streamData);
   
   // 開始播放。
   mLivePlayer.play();
   ```

2. 當 ABR 畫質等級自動切換時，會觸發 [VeLivePlayerObserver](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver) 的 [onResolutionSwitch](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onresolutionswitch) 回呼。範例程式碼如下。

   ```Java
   public void onResolutionSwitch(VeLivePlayer player, VeLivePlayerDef.VeLivePlayerResolution resolution, VeLivePlayerError error, VeLivePlayerDef.VeLivePlayerResolutionSwitchReason reason) {
      // 畫質等級切換回呼。
   }
   ```

## 平滑畫質等級切換

平滑畫質等級切換功能可確保觀眾手動在不同畫質等級之間切換時，音訊與視訊能無縫轉換，例如超高畫質、高畫質與標準畫質。此功能可**防止黑畫面或卡頓**，並改善觀看體驗。

若要使用此功能，請為播放器設定來自同一來源、具備多個畫質等級的串流清單，並啟用平滑畫質等級切換。設定完成後，當觀眾手動切換畫質等級時，播放器會在不同位元率的串流之間平滑轉換，確保持續且穩定的直播音訊與視訊播放。

> **注意**

> 平滑畫質等級切換支援串流備援策略。你可以為一組平滑畫質等級切換串流指定相同優先順序，並設定較低優先順序的備援串流。如果較高優先順序串流群組播放失敗，SDK 會自動嘗試備援群組。如需更多資訊，請參閱[串流備援策略與主備串流切換](https://docs.byteplus.com/en/docs/24/107292#stream-fallback-strategy-and-primary-backup-stream-switching)。

> **警告**

* > 平滑畫質等級切換功能目前僅適用於 FLV 串流。

* > 確保已整合 Player SDK 1.50.100 或更新版本。

### 前提條件

準備同一來源串流不同畫質等級的拉流位址。

如果你使用 BytePlus MediaLive 的推流位址進行串流，請確保已完成下列操作：

* **新增網域名稱**：在同一網域名稱空間下新增推流與拉流網域名稱。如需更多資訊，請參閱[新增網域名稱](https://docs.byteplus.com/docs/byteplus-media-live/docs-domain)。

* **設定轉碼**：在網域名稱空間下新增不同畫質等級的轉碼設定。如需更多資訊，請參閱[管理轉碼設定](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-transcoding)。

* **取得拉流位址**：取得來源串流與各轉碼串流的拉流位址。

   * **用於偵錯**：使用[位址產生器](https://console.byteplus.com/live/main/locationGenerate)產生拉流位址。

      * **位址類型**：選取**拉流位址**。

      * **網域名稱**：選取轉碼設定所使用網域名稱空間下的拉流網域名稱。

      * **AppName** 與 **StreamName**：輸入與推流位址相符的 `AppName` 與 `StreamName`。例如，如果推流位址為 `rtmp://push.example.com/live/test?authinfo`，則 `AppName` 為 `live`，`StreamName` 為 `test`。

   * **用於生產環境**：呼叫 [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) 或使用[伺服器端 SDK](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-server-sdk) 動態產生拉流位址。

**範例**

下表列出不同畫質等級的 FLV 拉流位址與位元率範例。

|畫質等級 |FLV 拉流位址 |位元率（kbps） |
|---|---|---|
|原始（Origin） |`https://pull.example.com/live/123456.flv` |2500 |
|超高畫質（UHD） |`https://pull.example.com/live/123456_uhd.flv` |2500 |
|高畫質（HD） |`https://pull.example.com/live/123456_hd.flv` |1000 |
|標準畫質（SD） |`https://pull.example.com/live/123456_sd.flv` |800 |
|低畫質（LD） |`https://pull.example.com/live/123456_ld.flv` |500 |

### 操作步驟

1. 設定各畫質等級的串流，並將 [enableSmoothSwitchResolution](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStreamData-enablesmoothswitchresolution) 設為 `true`，以啟用平滑畫質等級切換。

   ```Java
   // 設定各畫質等級的串流。
   // 原始畫質等級。
   VeLivePlayerStreamData.VeLivePlayerStream playStreamOrigin = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamOrigin.url = "https://pull.example.com/live/123456.flv"; // 替換為原始畫質等級的實際拉流位址。
   playStreamOrigin.format = VeLivePlayerFormatFLV; // 串流格式。
   playStreamOrigin.resolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionOrigin); // 畫質等級識別碼。
   playStreamOrigin.streamType = VeLivePlayerStreamTypeMain; // 用於區分主串流與備用串流的串流類型。
   playStreamOrigin.bitrate = 2500; // 位元率，單位為 kbps。
   
   // UHD 畫質等級。
   VeLivePlayerStreamData.VeLivePlayerStream playStreamUHD = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamUHD.url = "https://pull.example.com/live/123456_uhd.flv"; // 替換為 UHD 畫質等級的實際拉流位址。
   playStreamUHD.format = VeLivePlayerFormatFLV; // 串流格式。
   playStreamUHD.resolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionUHD); // 畫質等級識別碼。
   playStreamUHD.streamType = VeLivePlayerStreamTypeMain; // 用於區分主串流與備用串流的串流類型。
   playStreamUHD.bitrate = 2500; // 位元率，單位為 kbps。
   
   // HD 畫質等級。
   VeLivePlayerStreamData.VeLivePlayerStream playStreamHD = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamHD.url = "https://pull.example.com/live/123456_hd.flv"; // 替換為 HD 畫質等級的實際拉流位址。
   playStreamHD.format = VeLivePlayerFormatFLV; // 串流格式。
   playStreamHD.resolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionHD); // 畫質等級識別碼。
   playStreamHD.streamType = VeLivePlayerStreamTypeMain; // 用於區分主串流與備用串流的串流類型。
   playStreamHD.bitrate = 1000; // 位元率，單位為 kbps。
   
   // SD 畫質等級。
   VeLivePlayerStreamData.VeLivePlayerStream playStreamSD = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamSD.url = "https://pull.example.com/live/123456_sd.flv"; // 替換為 SD 畫質等級的實際拉流位址。
   playStreamSD.format = VeLivePlayerFormatFLV; // 串流格式。
   playStreamSD.resolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionSD); // 畫質等級識別碼。
   playStreamSD.streamType = VeLivePlayerStreamTypeMain; // 用於區分主串流與備用串流的串流類型。
   playStreamSD.bitrate = 800; // 位元率，單位為 kbps。
   
   // LD 畫質等級。
   VeLivePlayerStreamData.VeLivePlayerStream playStreamLD = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamLD.url = "https://pull.example.com/live/123456_ld.flv"; // 替換為 LD 畫質等級的實際拉流位址。
   playStreamLD.format = VeLivePlayerFormatFLV; // 串流格式。
   playStreamLD.resolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionLD); // 畫質等級識別碼。
   playStreamLD.streamType = VeLivePlayerStreamTypeMain; // 用於區分主串流與備用串流的串流類型。
   playStreamLD.bitrate = 500; // 位元率，單位為 kbps。
   
   // 建立 VeLivePlayerStreamData 執行個體。
   VeLivePlayerStreamData streamData = new VeLivePlayerStreamData();
   
   // 新增各畫質等級的串流。
   streamData.mainStreamList = new ArrayList<>();
   streamData.mainStreamList.add(playStreamOrigin);
   streamData.mainStreamList.add(playStreamUHD);
   streamData.mainStreamList.add(playStreamHD);
   streamData.mainStreamList.add(playStreamSD);
   streamData.mainStreamList.add(playStreamLD);
   
   // 設定預設啟動畫質等級。
   streamData.defaultResolution = new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionSD);
   
   // 啟用平滑畫質等級切換。
   streamData.enableSmoothSwitchResolution = true;
   
   // 設定播放來源。
   mLivePlayer.setPlayStreamData(streamData);
   
   // 開始播放。
   mLivePlayer.play();
   ```

2. 直播期間，當觀眾手動切換畫質等級時，你可以呼叫 [switchResolution](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-switchresolution) 平滑切換畫質等級。範例程式碼如下。

   ```Java
   mLivePlayer.switchResolution(new VeLivePlayerDef.VeLivePlayerResolution(VeLivePlayerDef.VeLivePlayerResolution.VeLivePlayerResolutionUHD)); // 切換至 UHD 畫質等級。
   ```

3. 新增 [onResolutionSwitch](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onresolutionswitch) 回呼，以監聽畫質等級切換結果。當畫質等級變更時，SDK 可觸發此回呼，並傳回切換後的畫質等級與切換原因等資訊。

   ```Java
   @Override
   public void onResolutionSwitch(
       VeLivePlayer player,
       VeLivePlayerResolution resolution,
       VeLivePlayerError error,
       VeLivePlayerResolutionSwitchReason reason
   ) {
   }
   ```

## 擷取快照

此功能可讓你擷取目前影片影格並產生影像。

1. 呼叫 [snapshot](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-snapshot) 擷取快照。此功能僅在播放期間生效。

   ```Java
   int result = mLivePlayer.snapshot();
   ```

2. 快照擷取完成後，會以影像資料觸發 [onSnapshotComplete](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onsnapshotcomplete) 回呼函式。

   ```Java
   public void onSnapshotComplete(VeLivePlayer player, Bitmap bitmap) {
     // 回呼函式透過 Bitmap 傳回影像資料。
   }
   ```

## SEI

補充增強資訊（SEI）是嵌入直播串流中的其他資料。你可以使用 SEI 傳輸自訂資料或中繼資料。

> **注意**

> 只有進階版與試用授權支援 SEI。

* 字串 SEI 訊息

   1. 呼叫 [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-play) 前，啟用播放器的 [enableSei](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerConfiguration-enablesei) 屬性。啟用此屬性後，播放器會接收字串 SEI 訊息。範例程式碼如下。

      ```Java
      // 建立 VeLivePlayerConfiguration 執行個體。
      VeLivePlayerConfiguration config = new VeLivePlayerConfiguration();
      
      // 啟用接收字串 SEI 訊息。
      config.enableSei = true;
      
      // 設定播放器的初始設定。
      mLivePlayer.setConfig(config);
      ```

   2. 當播放器接收到字串 SEI 訊息時，會觸發 [onReceiveSeiMessage](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onreceiveseimessage) 回呼。範例程式碼如下。

      ```Java
      public void onReceiveSeiMessage(VeLivePlayer player, String message) {
         // 字串 SEI 訊息回呼。
      }
      ```

* 二進位 SEI 訊息

   1. 呼叫 [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-play) 前，啟用播放器的 [enableBinarySei](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerConfiguration-enablebinarysei) 屬性。啟用此屬性後，播放器會接收二進位 SEI 訊息，且不再觸發字串 SEI 訊息回呼。範例程式碼如下。

      ```Java
      // 建立 VeLivePlayerConfiguration 執行個體。
      VeLivePlayerConfiguration config = new VeLivePlayerConfiguration();
      
      // 啟用接收二進位 SEI 訊息。
      config.enableBinarySei = true;
      
      // 設定播放器的初始設定。
      mLivePlayer.setConfig(config);
      ```

   2. 當播放器接收到二進位 SEI 訊息時，會觸發 [onReceiveBinarySeiMessage](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onreceivebinaryseimessage) 回呼。範例程式碼如下。

      ```Java
      public void onReceiveBinarySeiMessage(VeLivePlayer player, byte[] message) {
         // 二進位 SEI 訊息回呼。
      }
      ```

## 訂閱視訊資料

透過訂閱解碼後的視訊資料，你可以取得視訊影格資料以進行自訂處理與算繪。播放器支援多種視訊影格回呼格式，並提供對應的參數與格式選項。

### 前提條件

下表說明視訊影格像素格式與視訊資料封裝格式的列舉及含義。

|格式類型 |列舉 |說明 |
|---|---|---|
|視訊影格像素格式 |VeLivePlayerPixelFormatRGBA32 |RGBA32 |
|視訊影格像素格式 |VeLivePlayerPixelFormatTexture |2D 紋理 |
|視訊資料封裝格式 |VeLivePlayerVideoBufferTypeByteBuffer |ByteBuffer |
|視訊資料封裝格式 |VeLivePlayerVideoBufferTypeByteArray |ByteArray |
|視訊資料封裝格式 |VeLivePlayerVideoBufferTypeTexture |Texture |

訂閱視訊資料前，請根據需求選擇格式組合。該組合必須符合下表所示的 [VeLivePlayerPixelFormat](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#veliveplayerpixelformat) 與 [VeLivePlayerVideoBufferType](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#veliveplayervideobuffertype) 對應關係。

|像素格式/封裝格式 |VeLivePlayerPixelFormatRGBA32 |VeLivePlayerPixelFormatTexture |
|---|---|---|
|**VeLivePlayerVideoBufferTypeByteBuffer** |支援 |不支援 |
|**VeLivePlayerVideoBufferTypeByteArray** |支援 |不支援 |
|**VeLivePlayerVideoBufferTypeTexture** |不支援 |支援（最佳效能） |

### 操作步驟

1. 呼叫播放器的 [enableVideoFrameObserver](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-enablevideoframeobserver) API，以啟用或停用視訊影格資料訂閱。API 參數如下表所述。

   |參數 |類型 |說明 |
   |---|---|---|
   |enable |boolean |是否啟用視訊影格回呼。 |
   |pixelFormat |VeLivePlayerPixelFormat |視訊影格像素格式。 |
   |bufferType |VeLivePlayerVideoBufferType |視訊資料封裝格式。 |

   範例程式碼如下。

   ```Java
   //
   mLivePlayer.enableVideoFrameObserver(true, VeLivePlayerPixelFormatRGBA32, VeLivePlayerVideoBufferTypeByteBuffer);
   ```

2. SDK 透過 [VeLivePlayerObserver](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver) 的 [onRenderVideoFrame](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onrendervideoframe) 回呼傳回解碼後的視訊影格資料。範例程式碼如下。

   ```Java
   public void onRenderVideoFrame(VeLivePlayer player, VeLivePlayerVideoFrame videoFrame) {
      // 視訊影格資料回呼。
   }
   ```

   [VeLivePlayerVideoFrame](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerVideoFrame) 參數如下表所述。

   |參數 |類型 |說明 |
   |---|---|---|
   |bufferType |VeLivePlayerVideoBufferType |視訊影格資料封裝格式。 |
   |pixelFormat |VeLivePlayerPixelFormat |視訊影格像素格式。 |
   |width |int |視訊影格寬度，單位為 px。 |
   |height |int |視訊影格高度，單位為 px。 |
   |pts |long |視訊影格算繪時間戳記，單位為 ms。 |
   |texture |VeLivePlayerVideoTexture |`bufferType` 為 `VeLivePlayerVideoBufferTypeTexture` 時的視訊資料。此欄位攜帶用於 OpenGL 算繪的紋理資料。 |
   |buffer |ByteBuffer |`bufferType` 為 `VeLivePlayerVideoBufferTypeByteBuffer` 時的視訊資料。此欄位攜帶 JNI 層使用的直接緩衝區。 |
   |data |byte[] |`bufferType` 為 `VeLivePlayerVideoBufferTypeByteArray` 時的視訊資料。此欄位攜帶 Java 層使用的位元組陣列資料。 |

## 訂閱音訊資料

透過訂閱解碼後的音訊資料，你可以執行自訂音訊處理與算繪。Player SDK 支援以 PCM Float32 取樣格式與 ByteArray 封裝格式訂閱音訊資料。

|VeLivePlayerAudioBufferType |音訊資料封裝格式 |
|---|---|
|[VeLivePlayerAudioBufferTypeByteArray](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerAudioBufferType) |ByteArray |

### 操作步驟

1. 呼叫播放器的 [enableAudioFrameObserver](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-enableaudioframeobserver) API，以啟用或停用音訊影格資料訂閱。API 參數如下表所述。

   |參數 |類型 |說明 |
   |---|---|---|
   |enable |boolean |是否啟用音訊影格回呼。 |
   |enableRendering |boolean |是否啟用播放器算繪。如果播放器不需要在內部算繪音訊，請將此參數設為 `false`。 |

   範例程式碼如下。

   ```Java
   // 訂閱音訊影格資料，並啟用播放器內部音訊算繪。
   mLivePlayer.enableAudioFrameObserver(true, true);
   ```

2. SDK 透過 [VeLivePlayerObserver](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver) 的 [onRenderAudioFrame](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onrenderaudioframe) 回呼傳回解碼後的音訊影格資料。範例程式碼如下。

   ```Java
   void onRenderAudioFrame(VeLivePlayer player, VeLivePlayerAudioFrame audioFrame) {
      // 音訊影格資料回呼。
   }
   ```

   [VeLivePlayerAudioFrame](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerAudioFrame) 參數如下表所述。

   |參數 |資料類型 |說明 |
   |---|---|---|
   |bufferType |VeLivePlayerAudioBufferType |音訊影格資料封裝格式。 |
   |sampleRate |int |音訊取樣率，單位為 Hz。 |
   |channels |int |聲道數。 |
   |bitDepth |int |音訊位元深度。 |
   |pts |long |音訊算繪時間戳記，單位為 ms。 |
   |buffer |byte[] |PCM 音訊資料。 |
   |samples |int |音訊樣本數。 |

## 超解析度

超解析度（SR）是一種從低解析度影像重建高解析度影像的技術。即時 SR 使用演算法即時將低解析度影格重建為高解析度影格。這會產生高解析度影格，隨後顯示在螢幕上。SR 可增強影片細節與對比，提升影片清晰度與觀看體驗。

> **注意**

> 只有進階版與試用授權支援 SR。

1. 呼叫播放器的 [setEnableSuperResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setenablesuperresolution) 方法啟用或停用 SR。

   ```Java
   mLivePlayer.setEnableSuperResolution(true);
   ```

   |名稱 |類型 |說明 |
   |---|---|---|
   |enable |boolean |是否啟用 SR。預設值為 `false`。<br><br><br>* `true`：啟用 SR。<br><br>* `false`：停用 SR。 |

2. 如果啟用 SR 失敗，播放器會透過 [VeLivePlayerObserver](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver) 的 [onStreamFailedOpenSuperResolution](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onstreamfailedopensuperresolution) 回呼通知你。方法簽章如下。

   ```Java
   void onStreamFailedOpenSuperResolution(VeLivePlayer player, VeLivePlayerError error);
   ```

   啟用 SR 失敗的常見原因如下。

   * 實際串流解析度不在 SR 支援範圍內。

   * 實際串流影格率不在 SR 支援範圍內。

   * 目前裝置型號不支援 SR。

## 自訂 HTTP 請求標頭

為播放器的 HTTP 請求設定自訂請求標頭。此功能通常用於傳輸驗證權杖、Cookie 與業務追蹤識別碼等額外資訊。

> **注意**

> 只有 1.50.200.3 及更新版本支援自訂 HTTP 請求標頭。

### 操作步驟

開始播放前，你可以透過播放器的進階 API [setProperty](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setproperty) 設定自訂 HTTP 請求標頭。呼叫 `setProperty` 時，你需要傳入 `key-value` 設定。

**Key**

|參數名稱 |類型 |說明 |
|---|---|---|
|VeLivePlayerKeySetParamsHttpHeaders |[VeLivePlayerProperty](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerProperty) |用於設定自訂 HTTP 請求標頭的屬性鍵。 |

**Value**

該值是包含 `key-value` 配對的 `Map<String, String>` 物件，用於設定自訂 HTTP 請求標頭。

* `Key`：`String` 類型。請求標頭名稱。

* `Value`：`String` 類型。請求標頭值。

範例程式碼如下。

* 若要設定 HTTP 請求標頭

   ```Java
   Map<String, String> headerMap = new HashMap<>();
   headerMap.put("key", "value"); // 替換為實際標頭名稱和值。
   mLivePlayer.setProperty(VeLivePlayerProperty.VeLivePlayerKeySetParamsHttpHeaders, headerMap);
   ```

* 若要設定多個 HTTP 請求標頭

   ```Java
   Map<String, String> headerMap = new HashMap<>();
   headerMap.put("key1", "value1"); // 替換為實際標頭名稱和值。
   headerMap.put("key2", "value2"); // 替換為實際標頭名稱和值。
   headerMap.put("key3", "value3"); // 替換為實際標頭名稱和值。
   mLivePlayer.setProperty(VeLivePlayerProperty.VeLivePlayerKeySetParamsHttpHeaders, headerMap);
   ```

## H.265 硬體解碼與軟體解碼

具備進階版或試用授權的 SDK 預設啟用 H.265 硬體解碼與軟體解碼。播放 H.265 編碼的影片串流時，SDK 會先嘗試使用 H.265 硬體解碼。如果 H.265 硬體解碼失敗，SDK 會自動切換至 H.265 軟體解碼。

呼叫 [play](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-play) 前，透過播放器的初始設定啟用或停用硬體解碼。範例程式碼如下。

```Java
VeLivePlayerConfiguration config = new VeLivePlayerConfiguration();
config.enableHardwareDecode = true;
mLivePlayer.setConfig(config);
```

* `true`：啟用硬體解碼。

* `false`：停用硬體解碼，且僅使用軟體解碼。

你可以監聽 [onStatistics](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onstatistics) 回呼，並使用 [VeLivePlayerStatistics](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStatistics) 的 [isHardwareDecode](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerStatistics-ishardwaredecode) 屬性，判斷目前串流是否使用硬體解碼。

## H.266 軟體解碼

具備進階版或試用授權的 SDK 預設啟用 H.266 軟體解碼，無需額外設定。

## 影片銳化

影片銳化會在裝置本機增強影片，以提升邊緣與紋理細節的清晰度。播放期間，SDK 可即時增強邊緣與紋理細節，讓影片看起來更清晰，並改善觀看體驗。

> **注意**

> 只有進階版與試用授權支援影片銳化。

### 操作步驟

1. 呼叫播放器的 [setEnableSharpen](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setenablesharpen) 方法啟用或停用影片銳化。

   ```Java
   mLivePlayer.setEnableSharpen(true);
   ```

   |名稱 |類型 |說明 |
   |---|---|---|
   |enable |boolean |是否啟用影片銳化。預設值為 `false`。<br><br><br>* `true`：啟用影片銳化。<br><br>* `false`：停用影片銳化。 |

2. 如果啟用影片銳化失敗，播放器會透過 [VeLivePlayerObserver](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver) 的 [onStreamFailedOpenSharpen](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onstreamfailedopensharpen) 回呼通知你。方法簽章如下。

   ```Java
   default void onStreamFailedOpenSharpen(VeLivePlayer player, VeLivePlayerError error)
   ```

   啟用影片銳化失敗的常見原因如下。

   * 實際串流解析度不在影片銳化支援範圍內。

   * 實際串流影格率不在影片銳化支援範圍內。

   * 目前裝置型號不支援影片銳化。

   * 目前授權不支援影片銳化。

## 子母畫面

子母畫面（PiP）會將播放器視窗縮小為螢幕角落的小型浮動視窗，讓觀眾在瀏覽其他內容或使用其他應用程式時，仍可繼續觀看直播。此功能有助於提升觀看體驗。

### 前提條件

Android 6.0 或更新版本。

### 操作步驟

1. 將 [vepicutureinpicture](https://github.com/byteplus-sdk/VeLiveQuickStartDemo/tree/main/Android/VeLiveQuickStartDemo/vepicutureinpicture) 模組程式碼複製到主專案的根目錄。

2. 修改 `vepicutureinpicture/live/build.gradle` 中的 SDK 版本。將 `x.x.x.x` 替換為你已整合的 SDK 版本。版本號請參閱 [Android Player SDK 發行說明](https://docs.byteplus.com/docs/byteplus-media-live/docs-native-sdk-release-notes)。

   ```Plain
   implementation 'com.bytedanceapi:ttsdk-ttlivepull_premium:x.x.x.x'
   ```

3. 將 `vepicutureinpicture` 模組匯入你的專案。你可以參考 [VeLiveQuickStartDemo](https://github.com/byteplus-sdk/VeLiveQuickStartDemo) 進行設定。

   ```Java
   include ':vepicutureinpicture:live'
   include ':vepicutureinpicture:base'
   
   api project(path: ':vepicutureinpicture:live')
   ```

4. 初始化 PiP 功能。

   ```Java
   // mLivePlayer 是播放器執行個體。
   VeLivePictureInPicturePlayerManager mPipManager = new VeLivePictureInPicturePlayerManager(mLivePlayer, context);
   ```

5. 設定 PiP 觀察器，以處理從 PiP 模式恢復正常播放的邏輯。在下列範例程式碼中，將 `XXXActivity` 替換為專案中承載直播播放頁面的 Activity。

   ```Java
   mPipManager.setObserver(new VeLivePictureInPicturePlayerManager.VeLivePictureInPicturePlayerManagerObserver() {
       @Override
       public void onClickResumeAction() {
           // 從 PiP 模式恢復正常播放。
           try {
               Class<?> cls = Class.forName(XXXActivity.class.getName());
               Intent intent = new Intent(getBaseContext(), cls);
               intent.setFlags(Intent.FLAG_ACTIVITY_SINGLE_TOP | Intent.FLAG_ACTIVITY_NEW_TASK);
               startActivity(intent);
           } catch (ClassNotFoundException e) {
   
           }
       }
   });
   ```

6. 檢查目前應用程式是否具備系統浮層權限。

   ```Java
   boolean isPermission = mPipManager.isPermissionGranted();
   ```

   如果尚未授予系統浮層權限，請參考下列範例程式碼請求權限，並引導使用者前往系統設定頁面啟用權限。

   ```Java
   if (!isPermission) {
       mPipManager.requestPermission(new VePictureInPictureManager.VePictureInPicturePermissionCallback() {
           @Override
           public void onGranted(boolean granted) {
               // 權限請求結果回呼。true 表示已授予系統浮層權限。false 表示尚未授予系統浮層權限。
           }
   
           @Override
           public void onRequestPermission(Context context, VePictureInPictureManager.VePictureInPicturePermissionResult result) {
               // 引導使用者前往系統設定頁面啟用系統浮層權限。
               new AlertDialog.Builder(context)
                       .setMessage("The system overlay permission is not enabled. Go to Settings and enable the [Display over other apps] permission.")
                       .setPositiveButton("Enable", (dialog, which) -> {
                           // 使用者同意啟用系統浮層權限。
                           result.accept();
                       })
                       .setNegativeButton("Cancel", (dialog, which) -> {
                           // 使用者不同意啟用系統浮層權限。
                           result.cancel();
                       })
                       .setCancelable(false)
                       .show();
           }
       });
   }
   ```

7. 在頁面上進行直播播放期間，影片會算繪到 `Surface` 或 `SurfaceHolder`。整合 PiP 功能後，請將相同的 `Surface` 或 `SurfaceHolder` 傳給 `mPipManager`，讓目前直播影片在進入 PiP 模式後仍可繼續顯示。

   **設定 Surface**

```Java
   // 設定 Surface。
   mLivePlayer.setSurface(surface);
   mPipManager.setSurface(surface);
   ```

   **設定 SurfaceHolder**

```Java
   // 設定 SurfaceHolder。
   mLivePlayer.setSurfaceHolder(surfaceHolder);
   mPipManager.setSurfaceHolder(surfaceHolder);
   ```

8. 將播放器回呼傳回的目前影片寬度與高度傳給 `mPipManager`。這可讓 PiP 視窗使用影片的實際長寬比顯示影片。

   ```Java
   mLivePlayer.setVeLivePlayerObserver(new VeLivePlayerObserver() {
       @Override
       public void onVideoSizeChanged(VeLivePlayer player, int width, int height) {
           mPipManager.setVideoSize(width, height);
       }
   });
   ```

9. 如果需要自訂 PiP 視窗大小，請參考下列範例程式碼進行設定。

   **依寬度自訂**

```Java
   VeLivePictureInPictureConfiguration configuration = new VeLivePictureInPictureConfiguration();
   // 將 PiP 視窗最大寬度設為 720 px。最小寬度預設為最大寬度的 50%。高度會根據影片長寬比自動計算。
   configuration.maxWidth = 720;
   VeLivePictureInPicturePlayerManager.setConfiguration(configuration);
   ```

   你也可以根據裝置螢幕寬度比例設定 PiP 視窗大小。

   ```Java
   VeLivePictureInPictureConfiguration configuration = new VeLivePictureInPictureConfiguration();
   // 將 PiP 視窗最大寬度設為裝置螢幕寬度的 50%。最小寬度預設為最大寬度的 50%。高度會根據影片長寬比自動計算。
   configuration.maxWidthRatio = 0.5;
   VeLivePictureInPicturePlayerManager.setConfiguration(configuration);
   ```

   **依高度自訂**

```Java
   VeLivePictureInPictureConfiguration configuration = new VeLivePictureInPictureConfiguration();
   // 將 PiP 視窗最大高度設為 720 px。最小高度預設為最大高度的 50%。寬度會根據影片長寬比自動計算。
   configuration.maxHeight = 720;
   VeLivePictureInPicturePlayerManager.setConfiguration(configuration);
   ```

   你也可以根據裝置螢幕高度比例設定 PiP 視窗大小。

   ```Java
   VeLivePictureInPictureConfiguration configuration = new VeLivePictureInPictureConfiguration();
   // 將 PiP 視窗最大高度設為裝置螢幕高度的 50%。最小高度預設為最大高度的 50%。寬度會根據影片長寬比自動計算。
   configuration.maxHeightRatio = 0.5;
   VeLivePictureInPicturePlayerManager.setConfiguration(configuration);
   ```

10. 直播播放開始且已授予系統浮層權限後，你可以啟動 PiP 模式。

```Java
mPipManager.startPictureInPicture();
```

如果 PiP 模式目前啟用中，你可以停止 PiP 模式。

```Java
mPipManager.stopPictureInPicture();
```

11. 若要判斷 PiP 視窗目前是否顯示，請呼叫下列方法。

```Java
boolean showing = mPipManager.isPictureInPictureShowing();
```

12. 當不再需要 PiP 功能時，請銷毀 `mPipManager`。

```Java
mPipManager.destroy();
```

## 進階 API 設定

### 移除 SDK 自動附加的查詢參數

Player SDK 可能會將 `session_id` 等查詢參數附加到拉流位址。這些參數會識別拉流工作階段，並在排查播放問題時協助在用戶端與 CDN 記錄中定位相同工作階段。若要防止 SDK 在實際請求 URL 中包含自動附加的查詢參數，請啟用此功能。啟用此功能後，SDK 附加的查詢參數會從實際請求 URL 中移除，而原始拉流位址中已存在的查詢參數會保留。

> **注意**

> 只有 1.52.100.5 及更新版本支援移除 SDK 自動附加的查詢參數。

#### 操作步驟

開始播放前，你可以使用播放器的進階 [setProperty](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setproperty) API 設定是否移除 SDK 自動附加的查詢參數。呼叫 `setProperty` 時，你需要傳入 `key-value` 設定。

**Key**

|參數名稱 |類型 |說明 |
|---|---|---|
|VeLivePlayerKeySetParamsRemoveQueryParams |[VeLivePlayerProperty](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerProperty) |用於移除 SDK 自動附加查詢參數的屬性鍵。 |

**Value**

`Value` 是 Boolean 值，表示是否移除 SDK 自動附加的查詢參數。預設值為 `false`。

* `true`：移除 SDK 自動附加的查詢參數。

* `false`：保留 SDK 自動附加的查詢參數。

範例程式碼如下。

```Java
mLivePlayer.setProperty(VeLivePlayerProperty.VeLivePlayerKeySetParamsRemoveQueryParams, true);
```

**效果範例**

例如，拉流位址為：

```text
https://pull.example.com/live/test.flv?auth_key=1779891783-0-0-e1f5a2a****4b5fe21cb3efdc89af901
```

當 SDK 發起播放請求時，會自動附加 `session_id`：

```text
https://pull.example.com/live/test.flv?auth_key=1779891783-0-0-e1f5a2a****4b5fe21cb3efdc89af901&session_id=xxx
```

啟用此功能後，請求 URL 不再包含 `session_id`，但會保留原始拉流位址中的 `auth_key` 驗證參數：

```text
https://pull.example.com/live/test.flv?auth_key=1779891783-0-0-e1f5a2a****4b5fe21cb3efdc89af901
```
