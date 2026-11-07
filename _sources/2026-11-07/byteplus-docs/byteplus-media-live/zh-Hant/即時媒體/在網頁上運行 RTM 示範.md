---
title: "在網頁上運行 RTM 示範"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-running-the-rtm-demo-for-web-zh-TW"
---

若要在網頁上測試 Real\-Time Media（RTM）串流，可使用 BytePlus MediaLive 提供的示範。本主題將帶領你完成整個流程，從生成推流與拉流地址，到推送串流並在網頁上播放串流。

<span id="0439107b"></span>
## 前提條件

你已啟用 BytePlus MediaLive。


* 若你尚未擁有推流與拉流的網域名稱，可使用 MediaLive 提供的測試推流與拉流網域名稱。

* 若要使用自己的網域名稱進行測試，需新增至少兩個網域名稱，一個用於推流，另一個用於拉流。推流與拉流的網域名稱必須配置於同一網域命名空間下。


<span id="a0cf172d"></span>
## 操作流程

<span id="b5ad8b31"></span>
### 生成推流／拉流地址


1. 在左側導覽窗格中，選擇**工具箱** \> [地址生成器](https://docs.byteplus.com/en/byteplus-media-live/docs/address-generator)。

2. 完成相關配置。請確保用於生成推流與拉流地址的`AppName`與`StreamName`一致。如需更多資訊，請參閱[產生串流位址](https://docs.byteplus.com/docs/byteplus-media-live/docs-relay-zh-TW)。

3. 點擊**生成推流地址**，即可在**結果**區域獲取 RTM 推流地址。

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7b1cdda2de8c41df99239d8d976cefb2~tplv-goo7wpa0wc-image.image" width="812px" />   </div>
   

4. 點擊**生成拉流地址**，即可在**RTM Web SDK 播放地址**於**拉流 URL**標籤下獲取原始串流的播放地址，或於**轉碼串流**標籤選擇轉碼後綴，獲取轉碼串流的**RTM Web SDK 播放地址**。

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">若無法取得<strong>RTM Web SDK 播放地址</strong>，請聯絡<a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980">技術支援</a>。   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>RTM Web SDK 播放地址</strong>支援自動轉碼，包括 B\-frame 移除及 AAC 轉 Opus 音訊轉換。如需更多資訊，請參閱<a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-generating-live-stream-addresses-zh-TW">產生直播串流地址</a>。   </div>
   


<span id="ec1aebfd"></span>
### 推送 RTM 串流

你可[透過 BytePlus MediaLive 控制台](https://docs.byteplus.com/en/byteplus-media-live/docs/web-push?version=v1.0)推送 RTM 串流，或使用如 Open Broadcaster Software（OBS）等推流工具。請使用前一步取得的地址作為推流地址。

<span id="d1b7ef3b"></span>
### 拉取 RTM 串流


1. 前往[VePlayer](https://demo.byteplus.com/common/veplayer/basic/example)，該頁為 BytePlus MediaLive Player SDK for Web 的示範。

2. 於**功能配置**標籤下點擊**RTM 拉流**。

3. 在**程式碼範例**視窗中，將`url`欄位設為前一步取得的**RTM Web SDK 播放地址**。

4. 點擊**執行**以播放直播串流。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">若你的網域名稱未啟用 SSL 憑證，請以 HTTP 地址存取<a href="http://demo.byteplus.com/common/veplayer/basic/example?tab=function-display">未加密版本</a>的 VePlayer 示範頁。請注意，使用示範頁時，切勿傳遞任何敏感資訊。</div>
