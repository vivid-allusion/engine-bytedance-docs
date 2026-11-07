---
title: "Web 廣播 SDK：SDK 概述"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-introduction-to-the-broadcast-sdk-for-web-zh-TW"
---

BytePlus MediaLive 廣播 SDK 專為直播場景設計，協助主播順利將瀏覽器中擷取的音訊與視訊內容傳送至視訊直播伺服器。它支援多種串流場景，包括攝影機串流、螢幕分享、線上視訊串流、本地視訊混流，以及音訊混流。透過 [BytePlus MediaLive 的串流服務](https://www.byteplus.com/en/product/medialive)，您可以快速在網頁上啟用直播功能。

<span id="912d74c3"></span>
## 協議支援

廣播 SDK 支援使用 RTM 協議傳輸以 H.264 編碼的串流內容。

<span id="7ecc10a5"></span>
## 瀏覽器支援

我們建議您使用 **最新穩定版本**的網頁瀏覽器，以提升您的直播體驗。


|**平台** ||**Chrome 70 及以上版本** |**Edge 83 及以上版本** |**Safari 12 及以上版本** |**Firefox 80 及以上版本** |
|---|---|---|---|---|---|
|PC |Windows 10 |支援<br><br>（螢幕分享需 Chrome 74 或以上版本。） |支援<br><br>（螢幕分享需 Edge 99 或以上版本。） |不支援 |支援 |
||macOS 15 |支援<br><br>（螢幕分享需 Chrome 74 或以上版本。） |支援 |支援<br><br>（螢幕分享需 Safari 13 或以上版本。） |支援 |
|行動裝置 ||SDK 目前未正式支援行動裝置。若需將 SDK 整合至您的行動應用程式，請聯絡您的業務代表。 ||||
|Electron ||SDK 目前未正式支援 Electron。若需將 SDK 整合至您的 Electron 應用程式，請聯絡您的業務代表。 ||||


<span id="a26cb472"></span>
## 功能

BytePlus MediaLive 廣播 SDK 支援多種串流場景，包括：


* 攝影機串流：支援將攝影機擷取的視訊與音訊串流至伺服器。

* 麥克風串流：支援擷取並串流麥克風音訊。

* 螢幕分享：支援將螢幕內容以視訊形式串流。

* 本地／線上視訊串流：支援從本地視訊檔案及線上視訊來源進行串流。

* 本地視訊混流：支援本地混合多路視訊串流，內建範本並可自訂混流參數。


<span id="bc9faa42"></span>
## 限制


* 廣播 SDK 目前尚未支援在 H5 頁面整合。

* 使用廣播 SDK 推送的串流目前不支援 LL\-HLS 播放。
