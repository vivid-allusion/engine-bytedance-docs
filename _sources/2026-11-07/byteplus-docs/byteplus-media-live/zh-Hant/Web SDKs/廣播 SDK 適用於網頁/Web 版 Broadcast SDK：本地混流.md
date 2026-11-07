---
title: "Web 版 Broadcast SDK：本地混流"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-local_mixing-zh-TW"
---

若要將多個視訊與音訊來源（如攝影機、螢幕分享、麥克風與系統音訊）合併為單一串流的推流，可使用 BytePlus MediaLive Broadcast SDK for Web。本指南提供逐步說明，指導如何啟用**本地混流**，協助你降低頻寬使用量、自訂視訊排版，並靈活管理音訊來源。


* **降低頻寬使用量**：在本地將多路串流合併為單一串流，最小化上行頻寬消耗。

* **自訂排版**：調整每路視訊的大小、位置與層級。

* **靈活音訊管理**：混合不同音訊來源並控制各自音量。


<span id="922d04f5"></span>
## 運作原理

在**BytePlus MediaLive Broadcast SDK**中，音訊與視訊的處理方式會依是否啟用**本地混流**而有所不同。SDK 提供兩種模式：


* **預設模式（本地混流關閉，自動合併）** 

   * **使用場景**：僅有攝影機與麥克風的簡單推流。

   * **行為**：

      * 擷取到的音訊與視訊串流**會自動加入**推流，無需手動操作。

      * SDK 會在內部處理音訊／視訊混流，並將最終串流推送至伺服器。

* **本地混流模式（手動串流管理）** 

   * **使用場景**：多個視訊來源（例如攝影機 + 螢幕分享）或更複雜的音訊混流（例如麥克風 + 系統音訊）。

   * **行為**：

      * 擷取到的音訊與視訊串流**不會自動加入**推流。你必須手動加入這些串流。

      * 你需要呼叫：

         * `addVideoStream()` 以將視訊軌道加入混流畫布。

         * `addAudioStream()` 以將音訊軌道加入混音器。


<span id="962898ec"></span>
## 前置條件


* 你已依照[整合指南](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-integrating-the-broadcast-sdk-for-web)完成 SDK 初始化，並取得`livePusher` 物件。

* 你已登入[BytePlus MediaLive 控制台](https://console.byteplus.com/live/main/locationGenerate)以產生 RTM 推流地址。


<span id="6d5c9766"></span>
## 操作流程


1. **啟用本地混流**


在開始推流前，請呼叫下列方法以啟用本地混流，使 SDK 能合併多路音訊與視訊串流：

```JavaScript
livePusher.enableMixing(true);
```



2. **設定混流屬性**


使用`setMixingConfig` 方法，指定混流後的視訊解析度、幀率、背景色等屬性：

```JavaScript
livePusher.setMixingConfig({
  width: 1080,               // Width of the mixing canvas
  height: 720,               // Height of the mixing canvas
  frameRate: 30,             // Frame rate of the merged video
  backgroundColor: '#000000',// Background color of the canvas
});
```



3. **擷取多個媒體來源**


啟用本地混流後，擷取到的來源不會自動加入推流。你必須手動將每個來源的串流 ID 加入混流畫布或音訊混音器。以下為擷取攝影機、螢幕分享與麥克風串流的範例：

```JavaScript
const cameraStreamId = await pushClient.startCamera();
const screenStreamId = await pushClient.startScreenCapture();
const micStreamId = await pushClient.startMicrophone();
```



* 這些方法可能會觸發瀏覽器權限提示。請確保使用者允許存取攝影機與麥克風。

* 不同瀏覽器的螢幕分享實作方式有所不同。請根據目標瀏覽器處理權限與相容性。

4. **手動將串流加入混流會話**


在本地混流模式下，串流不會自動加入。你必須明確地加入這些串流：


* **將視訊串流加入混流畫布**

   ```JavaScript
   livePusher.addVideoStream([{
     streamId: screenStreamId,
     width: 1280,
     height: 720,
     x: 1280 / 2,
     y: 720 / 2,
     zOrder: 1,
     keepRatio: true,
   }, {
     streamId: cameraStreamId,
     width: 320,
     height: 180,
     x: 320 / 2,
     y: 180 / 2,
     zOrder: 2,
     keepRatio: true,
   }]);
   ```
   

   * `x` 與 `y` 定義視訊中心點在畫布上的位置。畫布的座標系統以左上角為原點 (0,0)。

   * `zOrder` 控制視訊的堆疊順序（層級）。`zOrder` 值較高的視訊會疊加在值較低的視訊之上。

   * 當 `keepRatio` 設為 `true` 時，縮放時會保留視訊的原始寬高比。

* **將音訊串流新增至混音器**

   ```JavaScript
   livePusher.addAudioStream({
     streamId: micStreamId,
     volume: 100,
   });
   ```
   

   * 對於多個音訊來源（例如外部檔案或自訂音訊來源），需針對每個來源分別呼叫 `addAudioStream`。

   * 使用 `volume` 來調整每個音訊串流的初始音量。

5. **開始串流**


最後，呼叫 `startPush` 方法並提供推流位址（由主控台產生），以啟動直播串流：

```JavaScript
livePusher.startPush('https://{{domain}}/{{appName}}/{{streamName}}.sdp');
```
