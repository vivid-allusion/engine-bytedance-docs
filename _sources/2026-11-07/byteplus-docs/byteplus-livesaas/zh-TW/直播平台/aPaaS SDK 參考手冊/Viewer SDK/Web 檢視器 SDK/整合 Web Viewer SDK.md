---
title: "整合 Web Viewer SDK"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/zheng-he-web-viewer-sdk-zh-TW"
---

Web Viewer SDK 可讓你的 PC 或行動平台 Web 應用程式加入互動功能，例如觀看直播、發送評論，以及參加抽獎活動。本指南提供整合 SDK 的逐步操作說明，並詳細介紹所需的參數、事件及 API，協助你快速上手。

<span id="Prerequisite"></span>
## 先決條件

由於 Web Viewer SDK 的 API 無法跨網域呼叫，請聯絡 BytePlus Live 技術支援，將你的網域名稱加到 BytePlus Live 的允許清單。

<span id="Demo"></span>
## 示範

BytePlus Live 提供 PC 與行動平台的示範操作環境。你可以在下方查看結果，並前往 [BytePlus Live aPaaS Solution Web SDK Demo](https://live.byteplus.com/demo/sdk/index.html) 進行線上調試與即時預覽。


<Tabs>
<Tab zoneid="dUWFLJV7fF" title="PC 效果">
<TabTitle>PC 效果</TabTitle>

在 PC 示範操作環境中，點擊 **View Code** 編輯程式碼並預覽結果。

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9d6e24c8579c455c9d15cdd99e5a2b63~tplv-goo7wpa0wc-image.image) </span>


</Tab>
<Tab zoneid="csqQKZnMbK" title="行動端效果">
<TabTitle>行動端效果</TabTitle>

在行動裝置的示範操作平台上，您可以直接編輯右側的程式碼以查看結果。

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/94c477739a434b97aa40f44ffa4da243~tplv-goo7wpa0wc-image.image) </span>


</Tab>
</Tabs>


<span id="Features"></span>
## 功能

如需 Web SDK 功能列表，請參閱 *Web Viewer SDK* 欄位於 [SaaS 與 aPaaS 的功能比較](https://docs.byteplus.com/docs/byteplus-livesaas/saas-yu-apaas-de-gong-neng-bi-jiao-zh-TW) 文件中的表格。

<span id="855885cc"></span>
## 整合方式

請完成以下步驟，將 Web Viewer SDK 整合至你的 Web 應用程式。

<span id="7f20b494"></span>
### Step 1: 匯入 CSS 與 JS 資源

根據你的平台與功能需求選擇合適的整合方式，然後使用 `link` 與 `script` 標籤匯入 CSS 與 JS 資源。

<span id="80ac0262"></span>
#### **PC 整合資源**

若要將 SDK 整合至 PC 端的 Web 應用程式，請選擇下方所述的資源之一。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">建議在平板裝置上整合 PC Web SDK，以獲得更佳的視覺體驗。</div>


* <div data-tips="true" data-tips-type="tip">直接修改 URL 中的版本號即可更新版本。請確保每個平台使用相符的 CSS 和 JS 版本。</div>




<Tabs>
<Tab zoneid="yeWQF7LqKp" title="模組化整合">
<TabTitle>模組化整合</TabTitle>

當需要完整直播間功能時使用，例如聊天、商品卡片、簽到等。

```HTML
// Modular integration on PC
<link rel="stylesheet" href="https://res.gcloudcache.com/bp-fe/livesaas-client/pc/css/index.2.0.31.css">
<script src="https://res.gcloudcache.com/bp-fe/livesaas-client/pc/js/index.2.0.31.js"></script>
```



</Tab>
<Tab zoneid="TlYQQayquf" title="僅播放器整合">
<TabTitle>僅播放器整合</TabTitle>

當僅需播放功能時使用，包括 VOD、直播、畫質切換、播放速度、多線路選擇等。

此方法的效能優於模組化整合。

```HTML
// Player-only integration on PC
<link rel="stylesheet" href="https://res.gcloudcache.com/bp-fe/livesaas-client/player-pc/css/index.2.0.31.css">
<script src="https://res.gcloudcache.com/bp-fe/livesaas-client/player-pc/js/index.2.0.31.js"></script>
```



</Tab>
</Tabs>


<span id="a7cb4e3d"></span>
#### 行動**整合資源**

若要將 SDK 整合至行動端的 Web 應用程式，請選擇下方所述的資源之一。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">直接修改 URL 中的版本號即可更新版本。請確保每個平台使用相符的 CSS 和 JS 版本。</div>



<Tabs>
<Tab zoneid="ELSS2Ekx4F" title="模組化與全頁整合">
<TabTitle>模組化與全頁整合</TabTitle>

當需要完整直播間功能時使用，例如聊天、商品卡片、簽到等。

```HTML
// Modular or full-page integration on Mobile
<link rel="stylesheet" href="https://res.gcloudcache.com/bp-fe/livesaas-client/mobile/css/index.2.0.31.css">
<script src="https://res.gcloudcache.com/bp-fe/livesaas-client/mobile/js/index.2.0.31.js"></script>
```



</Tab>
<Tab zoneid="vpOyhB8WI4" title="僅全頁整合">
<TabTitle>僅全頁整合</TabTitle>

當需要整合不屬於特定模組的功能時使用，例如直播活動預約、主播帳號或頁首圖片。

此方法的效能優於模組化與全頁整合。

```HTML
// Full-page integration on Mobile
<link rel="stylesheet" href="https://res.gcloudcache.com/bp-fe/livesaas-client/mobile-all/css/index.2.0.31.css">
<script src="https://res.gcloudcache.com/bp-fe/livesaas-client/mobile-all/js/index.2.0.31.js"></script>
```



</Tab>
<Tab zoneid="QPOMbxoZby" title="僅播放器整合">
<TabTitle>僅播放器整合</TabTitle>

您必須在以下情況使用此整合方式：


* 需要在觀看頁面顯示隨選播放器。

* 需要在同一頁面顯示多個直播或隨選播放器。


此方法的效能優於模組化與全頁整合。

```HTML
// Player-only integration on Mobile
<link rel="stylesheet" href="https://res.gcloudcache.com/bp-fe/livesaas-client/player-mobile/css/index.2.0.31.css">
<script src="https://res.gcloudcache.com/bp-fe/livesaas-client/player-mobile/js/index.2.0.31.js"></script>
```



</Tab>
</Tabs>


網域名稱：`https://res.gcloudcache.com/bp-fe`

最新版本：2.0.31

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">自 <strong>2.0.30</strong> 版本起，網域已從 <code>https://res.bytepluscdn.com/obj/bp-console-fe-sg</code> 更改為 <code>https://res.gcloudcache.com/bp-fe</code>。整合 SDK 版本 <strong>2.0.30</strong> 或以上時，請務必使用新的網域 <code>https://res.gcloudcache.com/bp-fe</code>。</div>


* <div data-tips="true" data-tips-type="warning">自 1.3.8 版本起，URL 中 <code>mobile/</code> 或 <code>pc/</code> 後的 <code>byteplus</code> 已被移除。例如，<code>https://mediaservice-fe.bytepluscdn.com/obj/vcloud-fe-sgcomm/livesaas-client/pc/byteplus/css/index.VERSIONNUMBER.css"></code> 已更改為 <code>https://mediaservice-fe.bytepluscdn.com/obj/vcloud-fe-sgcomm/livesaas-client/pc/css/index. VERSIONNUMBER.css""></code>。</div>



<span id="829352b2"></span>
### Step 2: 整合 Web Viewer SDK


1. 資源匯入後，ByteLiveWebSDK 會掛載於全域 `window` 物件。請使用以下方法將 Web Viewer SDK 整合至你的 Web 應用程式。

   ```JavaScript
   var webSDK = new window.ByteLiveWebSDK({
     activityId: 173312069231****,
     token: 'ZQ****',
     service: '',
     mode: 1,
     modules: [
       {
         id: "player",
         mode: "player", 
       }, 
       {
         id: "menu", 
         mode: "menu",
         menu: ["comment"],
       }
     ],
     options: {}
   })
   
   webSDK.emit('player.pause'); // Trigger events
   webSDK.on('player.pause', () => {}); // Listen for events
   ```
   

   如需程式碼中參數設定的詳細資訊，請參閱 [Web Viewer SDK：參數](https://docs.byteplus.com/docs/byteplus-livesaas/web-viewer-sdk-can-shu-zh-TW)。如需監聽與觸發事件的詳細資訊，請參閱 [Web Viewer SDK：事件](https://docs.byteplus.com/docs/byteplus-livesaas/web-viewer-sdk-shi-jian-zh-TW)。如需呼叫 API 的詳細資訊，請參閱 [API](https://docs.byteplus.com/docs/byteplus-livesaas/api-zh-TW)。

2. （選用）覆蓋樣式。SDK 元素的 `class` 屬性值不可更改。你可以修改 `class` 屬性的樣式屬性及對應值，以覆蓋該元素的樣式。


<span id="dc1eff46"></span>
### Step 3: 調試

請使用以下任一方法進行調試。


* 線上調試：建議你使用 SDK 示範操作環境，在 PC 上進行線上調試。透過操作環境，你可以配置不同的直播間與不同版本的 SDK，修改範本中的程式碼，並即時預覽結果。如需詳細資訊，請參閱 [Web Viewer SDK 示範操作環境](https://live.byteplus.com/demo/sdk/index.playground.html?mode=pc)。

* 本地調試：在你的本地端口 `localhost:8080` 上調試。此方法無法播放預覽或回放。

   1. 下載並解壓縮套件 [byte-live-sdk-demo-master-plus.zip](https://lf6-cdn-tos.douyinstatic.com/obj/livesaas/byte-live-sdk-demo-master-plus.zip)。

   2. 開啟終端機並執行 `cd` 指令，進入解壓縮資料夾的目錄。例如，`cd C:\Users\Admin\Downloads\byte-live-sdk-demo-master-plus`。

   3. 執行 `yarn` 指令安裝依賴項。

   4. 啟動服務時，Mac 請執行 `yarn start` 指令，Windows 請執行 `yarn start-win` 指令。

   5. 開啟 [http://localhost:8080/demo/sdk/index.html](http://localhost:8080/demo/sdk/index.html) 進行調試。


<span id="1164a8f8"></span>
## 常見問題

[Web Viewer SDK 常見問題](https://docs.byteplus.com/docs/byteplus-livesaas/web-viewer-sdk-chang-jian-wen-ti-zh-TW)
