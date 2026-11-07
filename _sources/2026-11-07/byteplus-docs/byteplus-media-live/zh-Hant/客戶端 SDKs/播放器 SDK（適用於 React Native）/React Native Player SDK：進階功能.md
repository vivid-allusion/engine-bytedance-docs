---
title: "React Native Player SDK：進階功能"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-rnplayer-advanced-features-zh-TW"
---

為提升應用程式中的觀看體驗，本主題詳細說明如何實作 React Native Player SDK 的進階功能。你可以根據實際業務需求，按需實作複雜功能。

<span id="0410f60d"></span>
## 先決條件


* 你已依照 [iOS 版 Player SDK：基本功能](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-basic-features-3-zh-TW) 提供的指引完成 Player SDK 的基本功能實作。

* 若要使用以下功能，請確保使用的是高級或試用授權。

   * H.265 硬體與軟體解碼

   * [超解析度](https://docs.byteplus.com/docs/byteplus-media-live/docs-rnplayer-advanced-features-zh-TW#b0f80f88)

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">試用授權僅供專案測試使用，無法續期。試用授權到期後將導致驗證失敗，服務會因此中斷。請於專案正式上線前升級為正式授權。如需更多資訊，請參閱 <a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management-zh-TW#777c7de7">將試用授權升級為基礎版或高級版授權</a>。   </div>
   

<span id="f5462033"></span>
## 說明

由於 Player SDK 使用多種音訊與視訊 API，這些 API 在模擬器上可能無法正常運作，建議你使用實體裝置進行測試。

<span id="5c83d510"></span>
## RTM 串流拉取

此功能需搭配 BytePlus MediaLive 提供的直播服務使用。詳細資訊請參考 [Introduction to Real Time Media](https://docs.byteplus.com/docs/byteplus-media-live/docs-introduction-to-real-time-media)。


1. 請使用 [address generator](https://docs.byteplus.com/en/byteplus-media-live/docs/address-generator) 產生 RTM 拉流地址與 FLV 拉流地址。若 RTM 拉流失敗，播放器會自動切換至 FLV 拉流。

2. 請使用以下程式碼設定 RTM 地址與 FLV 地址：

   ```JavaScript
   // Set the RTM address.
   const playStreamRTM = new VeLivePlayerStream();
   playStreamRTM.url = 'https://pull.example.com/live/stream.sdp';
   playStreamRTM.format = VeLivePlayerFormat.VeLivePlayerFormatRTM;
   playStreamRTM.resolution = VeLivePlayerResolution.VeLivePlayerResolutionOrigin;
   playStreamRTM.streamType = VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
   
   // Set the FLV address.
   const playStreamFLV = new VeLivePlayerStream();
   playStreamFLV.url = 'https://pull.example.com/live/stream.flv';
   playStreamFLV.format = VeLivePlayerFormat.VeLivePlayerFormatFLV;
   playStreamFLV.resolution = VeLivePlayerResolution.VeLivePlayerResolutionOrigin;
   playStreamFLV.streamType = VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
   
   // Create a VeLivePlayerStreamData instance.
   const streamData = new VeLivePlayerStreamData();
   const mainStreamList = [];
   
   // Add the RTM stream address.
   mainStreamList.push(playStreamRTM);
   
   // Add the FLV stream address.
   mainStreamList.push(playStreamFLV);
   
   // Set the default format and protocol.
   streamData.defaultFormat = VeLivePlayerFormat.VeLivePlayerFormatRTM;
   streamData.defaultProtocol = VeLivePlayerProtocol.VeLivePlayerProtocolTLS;
   
   // Pass in the pull-stream configurations.
   mLivePlayer.setPlayStreamData(streamData);
   
   // Start playback.
   mLivePlayer.play();
   ```
   


<span id="aa70c92b"></span>
## QUIC 串流拉取

此功能需搭配 BytePlus MediaLive 提供的直播服務使用。

請依下列步驟使用 QUIC 協議拉取串流：


1. 請使用 [address generator](https://docs.byteplus.com/en/byteplus-media-live/docs/address-generator) 產生 FLV 拉流地址。

2. 傳入 FLV 拉流地址，並使用以下程式碼將串流協議設為 QUIC：

   ```JavaScript
   // Set the FLV address.
   const playStreamFLV = new VeLivePlayerStream();
   playStreamFLV.url = 'https://pull.example.com/live/stream.flv';
   playStreamFLV.format = VeLivePlayerFormat.VeLivePlayerFormatFLV;
   playStreamFLV.resolution = VeLivePlayerResolution.VeLivePlayerResolutionOrigin;
   playStreamFLV.streamType = VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
   
   // Create a VeLivePlayerStreamData instance.
   const streamData = new VeLivePlayerStreamData();
   const mainStreamList = [];
   
   // Add the FLV stream address.
   mainStreamList.push(playStreamFLV);
   
   // Set the default format and protocol.
   streamData.defaultFormat = VeLivePlayerFormat.VeLivePlayerFormatFLV;
   streamData.defaultProtocol = VeLivePlayerProtocol.VeLivePlayerProtocolQUIC; // Use QUIC protocol
   
   // Pass in the pull-stream configurations.
   mLivePlayer.setPlayStreamData(streamData);
   
   // Start playback.
   mLivePlayer.play();
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">若播放器使用 QUIC 協議拉流失敗，將自動切換至 TCP 協議。   </div>
   

<span id="8a517a0b"></span>
## 使用 IP 地址拉取串流

播放器支援透過設定播放網域的 IP 地址來拉取串流，可縮短首幀時間。

請依下列步驟使用 IP 地址拉取串流：


1. 取得直播串流 URL 並解析 IP 地址。

2. 播放器會使用指定的 IP 地址拉取串流。範例程式碼如下。

   ```JavaScript
   // Set Playback URL
   mLivePlayer.setPlayUrl('https://pull.example.com/live/stream.flv');
   // Add IP Address and Domain name association
   const valueList = [];
   valueList.push('xxx.xxx.xxx.xxx'); // IP Address
   const map = {};
   map['pull.example.com'] = valueList;
   
   // Set IP Address
   mLivePlayer.setUrlHostIP(map);
   
   // Start playback
   mLivePlayer.play();
   ```
   


<span id="a95a61a8"></span>
## 主備串流

主備串流功能可為直播提供災難復原機制。透過配置主串流與備串流，播放器可在其中一個串流故障時自動切換。例如，若主串流故障，播放器會切換至備串流。你可以使用來自同一或不同服務商的串流地址。

請依下列步驟設定主串流與備串流地址：


1. 取得主串流與備串流地址。若你使用 BytePlus MediaLive 提供的直播服務，可使用 [address generator](https://docs.byteplus.com/en/byteplus-media-live/docs/address-generator) 產生地址。

2. 請使用以下程式碼設定主串流與備串流地址：

   ```JavaScript
   // Set the primary stream address.
   const playStreamMain = new VeLivePlayerStream();
   playStreamMain.url = 'https://pull.example.com/live/main.flv';
   playStreamMain.format = VeLivePlayerFormat.VeLivePlayerFormatFLV;
   playStreamMain.resolution = VeLivePlayerResolution.VeLivePlayerResolutionOrigin;
   playStreamMain.streamType = VeLivePlayerStreamType.VeLivePlayerStreamTypeMain; // Set the stream type to primary.
   
   // Set the backup stream address.
   const playStreamBackup = new VeLivePlayerStream();
   playStreamBackup.url = 'https://pull.example.com/live/backup.flv';
   playStreamBackup.format = VeLivePlayerFormat.VeLivePlayerFormatFLV;
   playStreamBackup.resolution =
     VeLivePlayerResolution.VeLivePlayerResolutionOrigin;
   playStreamBackup.streamType =
     VeLivePlayerStreamType.VeLivePlayerStreamTypeBackup; // Set the stream type to backup.
   
   // Create a VeLivePlayerStreamData instance.
   const streamData = new VeLivePlayerStreamData();
   
   // Enable automatic switching between primary and backup streams.
   streamData.enableMainBackupSwitch = true;
   
   // Add the primary stream.
   const mainStreamList = [];
   mainStreamList.push(playStreamMain);
   
   // Add the backup stream.
   const backupStreamList = [];
   backupStreamList.push(playStreamBackup);
   
   // Pass in the pull-stream configurations.
   mLivePlayer.setPlayStreamData(streamData);
   
   // Start playback.
   mLivePlayer.play();
   ```
   

3. 當播放器在主串流與備串流地址間切換時，會觸發 [onMainBackupSwitch](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#onmainbackupswitch) 回呼函式。

   ```JavaScript
   mLivePlayer.setObserver('onMainBackupSwitch', event => {});
   ```
   


<span id="3276b5ea"></span>
## 解析度切換

你可以設定多個不同解析度的拉流地址，並在播放過程中切換這些地址。

請依下列步驟啟用解析度切換：


1. 取得不同解析度的拉流地址。若你使用 BytePlus MediaLive 提供的直播服務，請執行以下操作：

   1. [配置轉碼任務](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-transcoding)以產生多個不同解析度的轉碼串流。

   2. 使用[地址生成器](https://docs.byteplus.com/en/byteplus-media-live/docs/address-generator)或呼叫[GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023)，為原始串流及轉碼串流生成相應的拉流地址。

2. 設定拉流地址。以下地址在範例程式碼中作為示例使用。

   
   |解析度 |拉流地址 |
   |---|---|
   |原始（Origin） |https://pull.example.com/live/123456.flv |
   |超高畫質（UHD） |https://pull.example.com/live/123456_uhd.flv |
   |高畫質（HD） |https://pull.example.com/live/123456_hd.flv |
   |標準畫質（SD） |https://pull.example.com/live/123456_sd.flv |
   |低畫質（LD） |https://pull.example.com/live/123456_ld.flv |
   

   ```JavaScript
   // Set multiple pull stream addresses with different resolutions.
   const playStreamOrgin = new VeLivePlayerStream();
   playStreamOrgin.url = "https://pull.example.com/live/123456.flv";
   playStreamOrgin.format = VeLivePlayerFormat.VeLivePlayerFormatFLV;
   playStreamOrgin.resolution = VeLivePlayerResolution.VeLivePlayerResolutionOrigin; // Original.
   playStreamOrgin.streamType = VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
   
   const playStreamUHD = new VeLivePlayerStream();
   playStreamUHD.url = "https://pull.example.com/live/123456_uhd.flv";
   playStreamUHD.format = VeLivePlayerFormat.VeLivePlayerFormatFLV;
   playStreamUHD.resolution = VeLivePlayerResolution.VeLivePlayerResolutionUHD; // UHD.
   playStreamUHD.streamType = VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
   
   VeLivePlayerStreamData.VeLivePlayerStream playStreamHD = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamHD.url = "https://pull.example.com/live/123456_hd.flv";
   playStreamHD.format = VeLivePlayerFormat.VeLivePlayerFormatFLV;
   playStreamHD.resolution = VeLivePlayerResolution.VeLivePlayerResolutionHD; // HD.
   playStreamHD.streamType = VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
   
   VeLivePlayerStreamData.VeLivePlayerStream playStreamSD = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamSD.url = "https://pull.example.com/live/123456_sd.flv";
   playStreamSD.format = VeLivePlayerFormat.VeLivePlayerFormatFLV;
   playStreamSD.resolution = VeLivePlayerResolution.VeLivePlayerResolutionSD; // SD.
   playStreamSD.streamType = VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
   
   VeLivePlayerStreamData.VeLivePlayerStream playStreamLD = new VeLivePlayerStreamData.VeLivePlayerStream();
   playStreamLD.url = "https://pull.example.com/live/123456_ld.flv";
   playStreamLD.format = VeLivePlayerFormat.VeLivePlayerFormatFLV;
   playStreamLD.resolution = VeLivePlayerResolution.VeLivePlayerResolutionLD; // LD.
   playStreamLD.streamType = VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
   
   // Create a VeLivePlayerStreamData instance.
   VeLivePlayerStreamData streamData = new VeLivePlayerStreamData();
   
   // Add the pull stream addresses.
   const mainStreamList = [];
   mainStreamList.push(playStreamOrgin);
   mainStreamList.push(playStreamUHD);
   mainStreamList.push(playStreamHD);
   mainStreamList.push(playStreamSD);
   mainStreamList.push(playStreamLD);
   
   // Set the default resolution to original.
   streamData.defaultResolution = VeLivePlayerResolution.VeLivePlayerResolutionOrigin;
   
   // Pass in the pull-stream configurations.
   mLivePlayer.setPlayStreamData(streamData);
   
   // Start playback.
   mLivePlayer.play();
   ```
   

3. 呼叫[switchResolution](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#switchresolution)以切換解析度。

   ```Python
   mLivePlayer.switchResolution(VeLivePlayerResolution.VeLivePlayerResolutionUHD); // Switch to UHD.
   ```
   

4. 切換成功後，將觸發[onResolutionSwitch](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#onresolutionswitch)回呼函式。

   ```JavaScript
   mLivePlayer.setObserver('onResolutionSwitch', () => {});
   ```
   


<span id="1ada31f7"></span>
## ABR 拉流

自適應位元率（ABR）是一種串流技術，利用演算法根據網路狀況自動切換不同解析度的串流。此過程可減少播放卡頓，提升觀看體驗。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">ABR 拉流僅適用於 FLV 串流。</div>


請依下列步驟啟用 ABR 拉流：


1. 取得不同解析度的拉流地址。若您使用 BytePlus MediaLive 提供的直播服務，請執行以下操作：

   1. [配置轉碼任務](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-transcoding)以產生多個不同解析度的轉碼串流。

   2. 使用[地址生成器](https://docs.byteplus.com/en/byteplus-media-live/docs/address-generator)或呼叫[GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023)，為原始串流及轉碼串流生成相應的拉流地址。

2. 設定拉流地址。以下地址在範例程式碼中作為示例使用。

   
   |**解析度** |**拉流地址** |**位元率（Kbps）**  |
   |---|---|---|
   |原始（Orgin） |https://pull.example.com/live/123456.flv |2500 |
   |超高畫質（UHD） |https://pull.example.com/live/123456_uhd.flv |2500 |
   |高畫質（HD） |https://pull.example.com/live/123456_hd.flv |1000 |
   |標準畫質（SD） |https://pull.example.com/live/123456_sd.flv |800 |
   |低畫質（LD） |https://pull.example.com/live/123456_ld.flv |500 |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">每個地址的編碼位元率必須與轉碼配置中設定的值一致。例如，若在轉碼配置中將 UHD 串流的位元率設為 2500 Kbps，則必須在 <code>playStreamUHD.bitrate</code> 設為 <code>2500</code> 的程式碼中。   </div>
   

   ```JavaScript
   // Set multiple pull stream addresses with different resolutions.
   const playStreamOrgin = new VeLivePlayerStream();
   playStreamOrgin.url = 'https://pull.example.com/live/123456.flv';
   playStreamOrgin.format = VeLivePlayerFormat.VeLivePlayerFormatFLV;
   playStreamOrgin.resolution =
     VeLivePlayerResolution.VeLivePlayerResolutionOrigin; // Original.
   playStreamOrgin.streamType = VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
   playStreamOrgin.bitrate = 2500; // The bitrate must be consistent with the transcoding configurations.
   
   const playStreamUHD = new VeLivePlayerStream();
   playStreamUHD.url = 'https://pull.example.com/live/123456_uhd.flv';
   playStreamUHD.format = VeLivePlayerFormat.VeLivePlayerFormatFLV;
   playStreamUHD.resolution = VeLivePlayerResolution.VeLivePlayerResolutionUHD; // UHD.
   playStreamUHD.streamType = VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
   playStreamUHD.bitrate = 2500;
   
   const playStreamHD = new VeLivePlayerStream();
   playStreamHD.url = 'https://pull.example.com/live/123456_hd.flv';
   playStreamHD.format = VeLivePlayerFormat.VeLivePlayerFormatFLV;
   playStreamHD.resolution = VeLivePlayerResolution.VeLivePlayerResolutionHD; // HD.
   playStreamHD.streamType = VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
   playStreamHD.bitrate = 1000;
   
   const playStreamSD = new VeLivePlayerStream();
   playStreamSD.url = 'https://pull.example.com/live/123456_sd.flv';
   playStreamSD.format = VeLivePlayerFormat.VeLivePlayerFormatFLV;
   playStreamSD.resolution = VeLivePlayerResolution.VeLivePlayerResolutionSD; // SD.
   playStreamSD.streamType = VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
   playStreamSD.bitrate = 800;
   
   const playStreamLD = new VeLivePlayerStream();
   playStreamLD.url = 'https://pull.example.com/live/123456_ld.flv';
   playStreamLD.format = VeLivePlayerFormat.VeLivePlayerFormatFLV;
   playStreamLD.resolution = VeLivePlayerResolution.VeLivePlayerResolutionLD; // LD.
   playStreamLD.streamType = VeLivePlayerStreamType.VeLivePlayerStreamTypeMain;
   playStreamLD.bitrate = 500;
   
   // Create a VeLivePlayerStreamData instance.
   const streamData = new VeLivePlayerStreamData();
   
   // Add the pull stream addresses.
   const mainStreamList = [];
   mainStreamList.push(playStreamOrgin);
   mainStreamList.push(playStreamUHD);
   mainStreamList.push(playStreamHD);
   mainStreamList.push(playStreamSD);
   mainStreamList.push(playStreamLD);
   
   // Set the default resolution to original.
   streamData.defaultResolution =
     VeLivePlayerResolution.VeLivePlayerResolutionOrigin;
   
   // Enable ABR.
   streamData.enableABR = true;
   
   // Pass in the pull-stream configurations.
   mLivePlayer.setPlayStreamData(streamData);
   
   // Start playback.
   mLivePlayer.play();
   ```
   

3. 解析度切換完成後，將觸發[onResolutionSwitch](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#onresolutionswitch)回呼函式。

   ```JavaScript
   mLivePlayer.setObserver('onResolutionSwitch', () => {});
   ```
   


<span id="dd3af7d9"></span>
## SEI

補充增強資訊（SEI）是嵌入於直播串流中的額外資料。您可以利用 SEI 傳輸自訂資料或中繼資料。


1. 在播放器初始化期間，可透過設定播放器的 enableSei 屬性來啟用接收 SEI 資訊。

   ```JavaScript
   // Create a player initialization configuration
   initPlayer({
     enableSei: true, // Enable receiving SEI messages.
     ...
   })
   ```
   

2. 當直播串流包含 SEI 訊息時，將觸發[onReceiveSeiMessage](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#onreceiveseimessage)回呼，並提供該訊息。

   ```JavaScript
   mLivePlayer.setObserver('onReceiveSeiMessage', seiMessage => {
     // processing received SEI messages
   });
   ```
   


<span id="b0f80f88"></span>
## 超解析度

超解析度（SR）是一項將低解析度影像重建為高解析度影像的技術。用戶端的即時 SR 會在用戶端裝置上利用演算法即時重建低解析度畫面。此舉會產生高解析度畫面，並顯示於螢幕上。SR 可增強影片細節與對比，提升影片清晰度及觀看體驗。


1. 請先聯繫 BytePlus[技術支援](https://www.byteplus.com/en/support)以啟用此功能，然後再使用。

2. 透過呼叫[setEnableSuperResolution](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-api#setenablesuperresolution)啟用 SR。預設值為`false`。

   
   |參數 |類型 |說明 |
   |---|---|---|
   |enable |boolean |是否啟用超分辨率功能。 |
   

3. 若 SDK 啟用 SR 失敗，將觸發[onStreamFailedOpenSuperResolution](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-rn-callback#onstreamfailedopensuperresolution)回呼。

   ```JavaScript
   mLivePlayer.setObserver('onStreamFailedOpenSuperResolution', () => {});
   ```
   


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">SR 可能因以下原因無法啟用：</div>



* <div data-tips="true" data-tips-type="tip">原始串流的解析度高於 SR 支援的最大解析度（1300\*750）。</div>


* <div data-tips="true" data-tips-type="tip">原始串流的幀率高於 SR 支援的最大幀率（30 fps）。</div>


* <div data-tips="true" data-tips-type="tip">用戶端裝置不支援 SR。</div>



<div data-tips="true" data-tips-type="tip">若最大解析度與幀率無法滿足您的業務需求，請聯繫 BytePlus 技術支援。</div>


<span id="7074e732"></span>
## 子母畫面

子母畫面（PiP）允許使用者在浮動視窗中繼續觀看影片，同時操作其他應用程式，實現多工處理。此功能支援具備原生 PiP 能力的 Android 與 iOS 系統。

<span id="f8c90919"></span>
### Step 1: Configure iOS permissions

要在 iOS 啟用 PiP，必須在 Xcode 中配置必要權限：


1. 在 Xcode 中開啟您的專案並選擇目標。

2. 前往**Signing & Capabilities**分頁。

3. 點擊\*\*+ Capability\*\*，然後新增**Background Modes**。

4. 啟用**Audio, AirPlay, and Picture in Picture**選項。


<span id="b7f3f8d3"></span>
### Step 2: Start Picture\-in\-Picture mode

影片播放時，呼叫`startPictureInPicture`方法以進入 PiP 模式：

```TypeScript
startPictureInPicture(aspectRatio?: number, x?: number, y?: number): Promise<void>
```



* 在**Android**上，您可以傳入選擇性參數以控制 PiP 視窗的長寬比及初始位置。

* 在**iOS**上，無需參數。系統會自動決定 PiP 視窗的大小與位置。


<span id="171026db"></span>
### Step 3: Manage background behavior on iOS

若要在應用程式進入背景時（僅限 iOS），讓播放器進入 PiP 模式，請於播放器處於播放狀態**時**依照以下步驟操作：


1. 呼叫 `enablePictureInPicture` 以啟用 PiP 功能。

2. 接著呼叫 `startPictureInPicture` 以進入 PiP 模式。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">若需防止應用程式切換至背景時自動啟動 PiP，請改為呼叫 disablePictureInPicture。</div>


<span id="6482915f"></span>
### Step 4: 監聽 PiP 事件

使用 `setPictureInPictureListener` 方法監聽 PiP 相關事件，例如進入、退出、點擊浮動視窗或發生錯誤。

範例：

```JavaScript
playerRef.current?.setPictureInPictureListener({
  onStartPictureInPicture: () => {
    addLog('onStartPictureInPicture');
  },
  onStopPictureInPicture: () => {
    addLog('onStopPictureInPicture');
    if (AppState.currentState !== 'active') {
      playerRef.current?.stop();
    }
    manualPip.current = false;
  },
  onClickPictureInPicture: () => {
    addLog('onClickPictureInPicture');
  },
  onError: errorCode => {
    addLog('onError' + errorCode);
  },
});
```
