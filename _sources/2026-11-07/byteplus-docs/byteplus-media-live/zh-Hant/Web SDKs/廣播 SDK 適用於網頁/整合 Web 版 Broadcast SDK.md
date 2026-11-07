---
title: "整合 Web 版 Broadcast SDK"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-integrating-the-broadcast-sdk-for-web-zh-TW"
---

要實現基於網頁的直播功能，可以使用 Web 版 Broadcast SDK。本主題提供從安裝 SDK 到推流的端到端操作指引。內容涵蓋攝影機設置、範例程式碼及常見問題，讓你能在幾分鐘內開始直播。

<span id="be143904"></span>
## 先決條件

在整合 **BytePlus MediaLive Broadcast SDK** 前，請確保以下事項：


* **環境需求**：

   * **串流 URL**：登入 [BytePlus MediaLive Console](https://console.byteplus.com/live/main/locationGenerate)，並使用地址生成器取得 RTM 推流地址。

* **硬體設置**：

   * 確認你的裝置（如攝影機、麥克風）已正確連接。

   * 授權瀏覽器存取攝影機、麥克風及螢幕分享的權限。

* **所需工具**：若透過 **NPM** 使用 SDK，請確保已安裝 **Node.js** 及套件管理器。


<span id="e912e634"></span>
## 操作流程

<span id="0fb66f1b"></span>
### Step 1: 匯入 SDK

你可以透過 **NPM** 匯入 SDK


<Tabs>
<Tab zoneid="QcK63z90ae" title="透過 NPM">
<TabTitle>透過 NPM</TabTitle>

1. 安裝 SDK：


```Bash
npm install @byteplus/vepusher@2.0.1 --save
```



2. 匯入 SDK：


```JavaScript
import LivePusher from '@byteplus/vepusher';
```



</Tab>
</Tabs>


<span id="7c3aca7c"></span>
### Step 2: 開始直播


1. 初始化 SDK：


```JavaScript
const livePusher = new LivePusher();
```



2. 在 HTML 中建立本地預覽容器：


```HTML
<div id="preview"></div>
```



3. 綁定預覽容器並開始渲染：


```JavaScript
livePusher.setRenderView('preview');
livePusher.startPreview();
```



4. 可選擇於擷取前設定視訊／音訊品質：


```JavaScript
livePusher.setVideoQuality('720p-1'); // Default video quality
livePusher.setAudioQuality('STANDARD'); // Default audio quality
```



5. 擷取媒體來源。SDK 支援攝影機、麥克風、螢幕分享等多種來源。擷取後，預覽畫面會自動更新：


```JavaScript
livePusher.startCamera();       // Capture camera
livePusher.startMicrophone();   // Capture microphone
```



6. 開始推流。使用 BytePlus MediaLive 控制台取得的 URL：


```JavaScript
livePusher.startPush('https://{{domain}}/{{appName}}/{{streamName}}.sdp');
```


<span id="5bd75e48"></span>
### Step 3: 結束直播


1. 停止推流：


```JavaScript
livePusher.stopPush();
```



2. 釋放媒體裝置（攝影機／麥克風）：


```JavaScript
livePusher.stopCamera();
livePusher.stopMicrophone();
```


<span id="3304c6ec"></span>
## 常見問題

<span id="75db841d"></span>
### 為什麼推流失敗？


* 請確認串流 URL 有效。

* 請確保有視訊軌道，目前不支援純音訊推流。

* 確認你的網路頻寬足以支援推流。


<span id="bbe22907"></span>
### 為什麼畫面延遲？


* 檢查網路上行頻寬是否充足且穩定。

* 降低視訊品質（例如，從 `720p-1` 降至 `360p`）。
