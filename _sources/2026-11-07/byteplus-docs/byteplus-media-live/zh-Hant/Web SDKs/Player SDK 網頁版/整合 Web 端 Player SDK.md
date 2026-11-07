---
title: "整合 Web 端 Player SDK"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-integrating-the-player-sdk-for-web_1-zh-TW"
---

若要將影片播放器嵌入網頁中，可將 Web 端 Player SDK（亦稱 VePlayer）整合至您的網頁應用程式。本主題說明如何整合 Web 端 Player SDK。

<span id="e625f8f3"></span>
## 先決條件


* 請根據 SDK 版本完成以下操作。

   * 2.11.0 及以上版本（建議）：建立 SDK 應用，並取得授權檔案、授權 URL 及 App ID。如需詳細資訊，請參閱 [取得您的 SDK 授權](https://docs.byteplus.com/docs/byteplus-media-live/managing_sdk_licenses-zh-TW)。

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">自 2.11.0 版本起，必須使用授權管理 Player SDK 及其增值服務的使用權限與期限。高級授權包含更多功能，例如 <a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-adaptive-bitrate-streaming-abr-zh-TW">自適應位元率串流</a>、<a href="https://docs.byteplus.com/en/docs/byteplus-media-live/adaptive-buffer-strategy">自適應緩衝策略</a>、<a href="https://docs.byteplus.com/en/docs/byteplus-media-live/achieving_2-3s_live_stream_latency_with_low-latency_FLV_web">低延遲 FLV 拉流</a>及<a href="https://docs.byteplus.com/en/docs/byteplus-media-live/RTM-Streaming-Integration">播放 RTM 流</a>，但需收費。如需瞭解不同授權類型及計費資訊，請參閱。      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">試用授權僅供專案測試使用，且無法續期。試用授權過期後將導致驗證失敗，進而中斷服務。請在專案正式上線前升級為正式授權。如需更多資訊，請參閱<a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management-zh-TW#777c7de7">將試用授權升級為基礎版或高級版授權</a>。      </div>
      

   * 2.11.0 以下版本：僅需建立 SDK 應用並取得 App ID。不需要授權。如需詳細資訊，請參閱 [取得您的 SDK 授權](https://docs.byteplus.com/docs/byteplus-media-live/managing_sdk_licenses-zh-TW)。建議您升級至最新版本，以獲得更佳功能與服務。

* 若要使用 Player SDK 拉取 BytePlus MediaLive 分發的串流，請完成以下先決條件：

   * 新增網域名稱及 CNAME 記錄。如需詳細資訊，請參閱 [新增網域名稱](https://docs.byteplus.com/docs/byteplus-media-live/docs-domain-zh-TW) 和 [新增 CNAME 記錄](https://docs.byteplus.com/docs/byteplus-media-live/docs-adding-a-cname-record-zh-TW)。

   * [產生拉流地址](https://docs.byteplus.com/byteplus-media-live/docs/address-generator)。若需使用 HTTPS 拉流地址，必須先新增 SSL 憑證並完成 HTTPS 設定。如需詳細資訊，請參閱 [管理 SSL 憑證](https://docs.byteplus.com/docs/byteplus-media-live/docs-managing-certificates-zh-TW) 和 [HTTPS 設定](https://docs.byteplus.com/docs/byteplus-media-live/docs-https-zh-TW)。


<span id="ceef554f"></span>
## Step 1: 匯入依賴項

可選擇以下任一方式匯入 SDK：


<Tabs>
<Tab zoneid="ed9MdfMr9t" title="CDN">
<TabTitle>CDN</TabTitle>

要透過 CDN 匯入 Player SDK 的 CSS 和 JS 檔案，請將以下程式碼加入本地專案的 `index.html` 檔案：

```HTML
<link rel="stylesheet" href="https://sf-unpkg.bytepluscdn.com/obj/byteplusfe-sg/sdk/@byteplus/veplayer/2.11.2/umd/veplayer.production.css">

<script src="https://sf-unpkg.bytepluscdn.com/obj/byteplusfe-sg/sdk/@byteplus/veplayer/2.11.2/umd/veplayer.production.js"></script>
```



</Tab>
<Tab zoneid="YBRvWrZztx" title="NPM">
<TabTitle>NPM</TabTitle>

1. 執行以下指令以安裝 Player SDK。

   ```Plain
   npm install @byteplus/veplayer@next
   npm install @byteplus/veplayer-plugin@next
   ```
   

2. 將以下程式碼加入本地專案的 `index.html` 檔案。

   ```Plain
   import { createLivePlayer, register } from '@byteplus/veplayer';
   import '@byteplus/veplayer/style';
   ```
   

3. 如有需要，請匯入並註冊插件。範例程式碼如下。

   ```JavaScript
   // To play HLS streams
   import { hlsjs } from '@byteplus/veplayer-plugin';
   register([hlsjs]);
   
   // To play FLV streams
   import { flv } from '@byteplus/veplayer-plugin';
   register([flv]);
   
   // To play RTM streams
   import { rtm } from '@byteplus/veplayer-plugin';
   register([rtm]);
   
   // To play multiple streams in different protocols
   import { flv, hlsjs, rtm } from '@byteplus/veplayer-plugin';
   register([rtm, flv, hlsjs]);
   ```
   

   為減少套件體積，您可以依路徑匯入單一插件。例如，將 `import { hlsjs } from '@byteplus/veplayer-plugin';` 替換為 `import * as hlsjs from '@byteplus/veplayer-plugin/hlsjs';` 以匯入 hlsjs 插件。同樣地，您可以按需匯入以下插件：`flv`、`rtm`、`abr`、`drm`、`timeshift` 和 `ad`。


</Tab>
</Tabs>


<span id="7d0334fc"></span>
## Step 2: 新增播放器容器

在您希望顯示播放器的頁面新增播放器容器。例如，將以下程式碼新增至 `index.html`：

```html
<div id="veplayer"></div>
```


<span id="f1396aa0"></span>
## Step 3: 設定授權

自 2.11.0 版本起，必須設定授權才能使用 Player SDK。請依步驟完成設定。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">2.11.0 之前的版本無需授權，但建議您升級至最新版本以獲得更佳功能與服務。</div>


* <div data-tips="true" data-tips-type="warning">請確保嵌入播放器的頁面網域與 SDK 應用程式所設定的萬用網域一致。否則，授權驗證將會失敗。例如，若您設定 <code>*. example.com</code> 為萬用網域，則頁面網域必須為第一層子網域，如 <code>a.example.com</code>。</div>



授權驗證於頁面層級執行，因此即使在單頁多實例場景下，也只需設定一次。為優化播放體驗並提升首幀載入速度，建議於初始化播放器前先設定授權。

您可透過以下任一方式設定授權。


<Tabs>
<Tab zoneid="OXn9NTyhoQ" title="設定授權檔案內容">
<TabTitle>設定授權檔案內容</TabTitle>

呼叫 `setLicenseConfig` 並提供授權檔案內容。


* `sign`：來自授權檔案的 `Signature`，用於驗證。

* `content`：來自授權檔案的 `Content`，包含權限等級及版本資訊。

* `mainUrl`（非必填但建議設定）：來自授權檔案的 `MainUrl`，即授權 URL。若已設定，SDK 會在授權升級或續期後自動更新至最新授權版本，無需手動更新。如需取得授權 URL 的詳細方法，請參閱[Step 2: Get the license file](https://docs.byteplus.com/docs/byteplus-media-live/managing_sdk_licenses-zh-TW#8a4f3efc)。


範例程式碼如下。


* CDN

   ```JavaScript
   VePlayer.live.setLicenseConfig({
     license: {
        sign: "xxx",
        content: "xxx",
        mainUrl: "https://example.com/obj/license-byteplus/license.lic", 
    }
   })
   ```
   

* NPM

   ```JavaScript
   import { live } from '@byteplus/veplayer';
   live.setLicenseConfig({
     license: {
        sign: "xxx",
        content: "xxx",
        mainUrl: "https://example.com/obj/license-byteplus/license.lic", 
    }
   })
   ```
   


</Tab>
<Tab zoneid="Pp4sIVTe3d" title="設定授權 URL">
<TabTitle>設定授權 URL</TabTitle>

呼叫 `setLicenseConfig` 並提供授權 URL。如需取得授權 URL 的詳細方法，請參閱[Step 2: Get the license file](https://docs.byteplus.com/docs/byteplus-media-live/managing_sdk_licenses-zh-TW#8a4f3efc)。

SDK 會自動處理驗證邏輯並啟用授權自動更新。範例程式碼如下。


* CDN

   ```JavaScript
   VePlayer.setLicenseConfig({
       // The license URL.SDK 在授權升級或續約後會自動更新至最新授權版本，無需手動更新。
       license: "https://example.com/obj/license-byteplus/license.lic"
   }) 
   ```
   

* NPM

   ```JavaScript
   import { live } from '@byteplus/veplayer';
   live.setLicenseConfig({
       // The license URL.SDK 在授權升級或續約後會自動更新至最新授權版本，無需手動更新。
       license: "https://example.com/obj/license-byteplus/license.lic"
   }) 
   ```
   


</Tab>
</Tabs>


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">若播放器初始化並播放影片時未出現任何授權相關錯誤，即驗證成功。</div>


<span id="f816d63b"></span>
## Step 4: 建立 VePlayer 實例並啟用日誌上報

使用以下程式碼建立 VePlayer 實例並啟用日誌上報。頁面載入後，播放器即開始播放。若要播放直播流，請將 `url` 設為拉流地址。


<Tabs>
<Tab zoneid="vZsfRFMCNn" title="CDN">
<TabTitle>CDN</TabTitle>

```javascript
VePlayer.createLivePlayer({
  width: 640,
  height: 360,
  url: 'https://livepull.example.com/appname/streamname.flv',
  logger:{
    // 啟用日誌上報。啟用後，SDK 會將播放相關資訊傳送至 BytePlus MediaLive 伺服器，以便故障排查與分析，協助提升應用程式的穩定性與用戶體驗。
    appId: 'APP_ID', // 必填。將 APP_ID 替換為 app ID，該 ID 來自你所建立的 SDK 應用程式。
    userId: 'USER_ID', // Optional.將 USER_ID 替換為應用程式用戶 ID。
    deviceId: 'DEVICE_ID', // Optional.將 DEVICE_ID 替換為用戶的裝置 ID。
  }
}).then(function(veplayer){
  console.log('VePlayer is successfully created. The VePlayer instance is:', veplayer)
}).catch(function(err){
  console.log('Creating VePlayer failed due to:', err)
});
```



</Tab>
<Tab zoneid="GN2wSm1VS5" title="NPM">
<TabTitle>NPM</TabTitle>

```javascript
createLivePlayer({
  width: 640,
  height: 360,
  url: 'https://livepull.example.com/appname/streamname.flv',
  logger:{
    // 啟用日誌上報。啟用後，SDK 會將播放相關資訊傳送至 BytePlus MediaLive 伺服器，以便故障排查與分析，協助提升應用程式的穩定性與用戶體驗。
    appId: 'APP_ID', // Required.將 APP_ID 替換為 app ID，該 ID 來自你所建立的 SDK 應用程式。
    userId: 'USER_ID', // Optional.將 USER_ID 替換為應用程式用戶 ID。
    deviceId: 'DEVICE_ID', // Optional.將 DEVICE_ID 替換為用戶的裝置 ID。
  }
}).then(function(veplayer){
  console.log('VePlayer is successfully created. The VePlayer instance is:', veplayer)
}).catch(function(err){
  console.log('Creating VePlayer failed due to:', err)
});
```



</Tab>
</Tabs>


直播流播放過程中若發生問題，請收集相關資訊（如問題發生時間及使用者 ID），並 [聯繫技術支援](https://console.byteplus.com/workorder/create)協助排查。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">自 2.5.1 版本起，若未設定 <code>appId</code>，將觸發主控台錯誤，且 SDK 會以預設 <code>appId</code> 回報日誌。</div>


* <div data-tips="true" data-tips-type="tip">強烈建議同時傳入 <code>userId</code> 與 <code>deviceId</code>。這有助於快速定位並排除播放問題。若未提供 <code>userId</code> 與 <code>deviceId</code>，SDK 會根據使用者瀏覽器產生隨機值並儲存於本地。</div>



<span id="fa2afbea"></span>
## 後續操作

Player SDK 提供多種功能，涵蓋多種播放場景，包括自訂封面圖片、畫中畫、進度條縮圖預覽，以及自動降畫質、播放 RTM 流等進階功能。如需詳細資訊，請參閱 [功能整合](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-web-feature-integration)。

VePlayer 亦針對各種播放場景提供豐富功能。您可試用 [Web 播放器示範](https://demo.byteplus.com/common/veplayer/basic/example?tab=function-display)，探索其功能、效果及整合方式。
