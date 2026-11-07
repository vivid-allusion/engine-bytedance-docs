---
title: "整合網頁版 Player SDK"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-integrating-the-player-sdk-for-web-zh-TW"
---

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">本文適用於 BytePlus MediaLive Player SDK for Web 1.x 版本。我們強烈建議升級至最新版本，以獲得最佳播放器體驗。</div>


本主題說明如何將 BytePlus MediaLive Player SDK for Web（亦稱為 VePlayer）新增至您的網頁應用程式。整合流程包含以下步驟：


1. 匯入依賴項

2. 新增播放器容器

3. 建立 VePlayer 實例

4. 實現更多功能


<span id="Prerequisites"></span>
## 先決條件

若要讓 Player SDK 拉取由 BytePlus MediaLive 分發的串流，請在開始前執行以下操作：


* 新增網域名稱及 CNAME 記錄。詳情請參閱[新增網域名稱](https://docs.byteplus.com/docs/byteplus-media-live/docs-domain#bb9e1337)及[新增 CNAME 記錄](https://docs.byteplus.com/docs/byteplus-media-live/docs-adding-a-cname-record)。

* [產生拉流地址](https://docs.byteplus.com/byteplus-media-live/docs/address-generator)。若需使用 HTTPS 拉流地址，請先新增憑證並完成 HTTPS 設定。詳情請參閱[管理 SSL 憑證](https://docs.byteplus.com/docs/byteplus-media-live/docs-managing-certificates)及[新增 SSL 憑證](https://docs.byteplus.com/docs/byteplus-media-live/docs-https)。


<span id="Importing dependencies"></span>
## 匯入依賴項

<span id="6298ac53"></span>
### 使用 CDN 匯入

若要透過 CDN 匯入 Player SDK 的 CSS 和 JS 檔案，請將以下程式碼新增至本地專案的`index.html`檔案：

```HTML
<link rel="stylesheet" href="//sf-unpkg.bytepluscdn.com/obj/byteplusfe-sg/sdk/@byteplus/veplayer/1.6.3/index.min.css">
<script src="//sf-unpkg.bytepluscdn.com/obj/byteplusfe-sg/sdk/@byteplus/veplayer/1.6.3/index.min.js"></script>
```


<span id="6b8a8eb3"></span>
### 使用 NPM 匯入


1. 若要使用 NPM 安裝 SDK 依賴項，請執行以下指令：


```Bash
npm install @byteplus/veplayer
```



2. 安裝完成後，請依下方方式將 VePlayer 及其 CSS 檔案匯入至您的專案：


```Bash
import VePlayer from '@byteplus/veplayer';
import '@byteplus/veplayer/dist/index.min.css';
```


<span id="Adding a container for the player"></span>
## 新增播放器容器

請在欲顯示播放器的頁面新增播放器容器。例如，將以下程式碼新增至`index.html`：

```html
<div id="video"></div>
```


<span id="Creating a VePlayer instance"></span>
## 建立 VePlayer 實例

請使用以下程式碼建立 VePlayer 實例。頁面載入後，播放器即開始播放。若要播放直播串流，請將`isLive`設為`true`，並將`url`設為拉流地址。有關參數詳情，請參閱[API 參考](https://docs.byteplus.com/byteplus-media-live/docs/api-reference)。

```javascript
const playerSdk = new VePlayer({
  id: 'video',
  isLive: true,
  url: '//livepull.example.com/appname/streamname.flv'
});
```


<span id="Implementing more features"></span>
## 實現更多功能

Player SDK 提供多種功能，涵蓋多種播放場景，包括自訂封面圖片、子母畫面、進度條懸停預覽縮圖，以及自動降解析度、使用 RTM 協議播放直播等進階功能。

有關 Player SDK 所提供的參數、方法及回呼的詳細說明，請參閱[API 參考](https://docs.byteplus.com/byteplus-media-live/docs/api-reference)。
