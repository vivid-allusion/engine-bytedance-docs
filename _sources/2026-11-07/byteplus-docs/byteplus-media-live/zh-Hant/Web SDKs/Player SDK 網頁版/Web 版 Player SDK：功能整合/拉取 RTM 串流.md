---
title: "拉取 RTM 串流"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/RTM-Streaming-Integration-zh-TW"
---

為了在如聯合直播或即時答題等互動場景下實現超低延遲串流，你可以透過網頁端播放器 SDK（VePlayer）整合 RTM 串流。本主題提供配置 RTM 並自動回退至 FLV 或 HLS 的詳細說明與程式碼範例，確保在所有裝置與網路環境下都能穩定播放。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">建議您使用最新版本的 Player SDK for Web。版本資訊請參見<a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-changelog_2-zh-TW">Player SDK for Web：發行說明</a>。舊版資訊請參見<a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-web-1-x-versions-zh-TW">Web 端播放器 SDK：1.x 版本</a>。</div>


<span id="自动降级机制"></span>
## 自動回退機制

RTM 串流對裝置與網路環境的相容性要求較高。為確保在各種情況下順暢播放，強烈建議於使用 RTM 串流時配置回退機制。本主題中的所有場景均包含回退配置。

播放器會在以下情況自動觸發回退機制並切換至備用串流：


* 瀏覽器或裝置環境不支援 RTM 協定播放，或不支援播放以 H.264 編碼的 RTM 串流。

* 播放過程中發生解碼異常。


如需了解播放器如何檢測 RTM 與 FLV 播放支援情況，請參見[如何檢測協定相容性](https://docs.byteplus.com/docs/byteplus-media-live/RTM-Streaming-Integration-zh-TW#%E5%A6%82%E4%BD%95%E6%A3%80%E6%B5%8B%E5%8D%8F%E8%AE%AE%E5%85%BC%E5%AE%B9%E6%80%A7%EF%BC%9F)。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">若因網路異常導致 RTM 拉流失敗，播放器會自動重試（預設為 3 次），並不會直接啟動備援。您可透過<code>retryCount</code>參數自訂重試次數。</div>


<span id="协议兼容性要求"></span>
## 協定相容性要求

RTM 播放對客戶端環境有較高要求。在某些情況下，可能因裝置或網路限制導致播放失敗。為確保一致的播放體驗，當 RTM 播放失敗時，播放器支援**自動回退**至其他協定（如 FLV 或 HLS）。各環境下的回退支援如下：


|用戶端環境 |支援的備援協議 |備援串流的音訊編碼需求 |
|---|---|---|
|PC / Android |FLV 或 HLS |AAC |
|iOS ≥ 17.1 |FLV 或 HLS ||
|iOS ≤ 17.0 |HLS ||


<span id="c10b609a"></span>
## 前置條件


* 你已整合網頁端播放器 SDK。如需更多資訊，請參見[整合 Web 端 Player SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-player-sdk-for-web_1-zh-TW)。

* 可透過以下任一方式取得 RTM 拉流地址。該地址可為原始串流地址或轉碼後的串流地址。

   * **用於除錯**：使用[地址產生器](https://console.byteplus.com/live/main/locationGenerate)取得**RTM Web SDK 播放地址**。如需更多資訊，請參見[產生串流地址](https://docs.byteplus.com/docs/byteplus-media-live/docs-address-generator)。

   * **用於生產環境**：呼叫[GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023)或使用[伺服器端 SDK](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-server-sdk)動態產生 RTM 拉流地址。請確保`Protocol`的值為`udp_websdk`。


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">若無法取得 RTM 拉流地址，請聯繫<a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980">技術支援</a>。</div>


* <div data-tips="true" data-tips-type="warning">RTM 拉流地址支援自動轉碼，包括移除 B\-frame 及 AAC 轉 Opus 音訊。更多資訊請參見<a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-generating-live-stream-addresses-zh-TW">產生直播串流地址</a>。</div>



<span id="ab524812"></span>
## 配置範例

以下範例展示如何在單一路徑及多畫質／多路線場景下配置 RTM 串流。


* **單一路徑串流**：適用於網路穩定且無需切換畫質或路線的簡單直播場景。

* **多畫質或多路線串流**：適用於需根據網路或裝置狀況切換畫質或路線，以確保播放更順暢的場景。


<span id="场景一：单地址拉流"></span>
### 場景一：單一路徑串流

在此情境下，你可以配置**RTM 失敗時自動回退**、**依錯誤類型條件回退**及**自訂回退順序**。以下章節提供配置範例。


<Tabs>
<Tab zoneid="SuC9wHQDX6" title="RTM 失敗自動備援">
<TabTitle>RTM 失敗自動備援</TabTitle>

RTM 播放失敗時，播放器可自動切換至其他協議。以下範例展示不同備援機制的配置方式。


* **CDN 來源**

   ```JavaScript
   VePlayer.createLivePlayer({
       height: 360,
       playlist: [
         {
           // The RTM stream uses the RTM address for Player SDK for Web.此地址支援自動轉碼，備援串流則使用 HLS 或 FLV 地址。
           definitions: [
             'https://pull-demo.example.com/live/st-4536521_autortm.sdp',
             'https://pull-demo.example.com/live/st-4536521.flv',
             'https://pull-demo.example.com/live/st-4536521.m3u8',
           ],
         },
       ],
       fallback: {
         // 1. Fallback to FLV if RTM is not supported or fails
         fallbackOrder: ['rtm', 'flv'],
         // 2. Fallback to HLS if RTM is not supported or fails
         // fallbackOrder: ['rtm', 'hls'],
         // 3. Fallback to FLV, then to HLS
         // fallbackOrder: ['rtm', 'flv', 'hls'],
       },
   }).then(function(veplayer) {
       veplayer.on(VePlayer.live.Events.FALLBACK_ERROR, function(){
           // Triggered when all fallback attempts have failed
       });
   })
   ```
   

* **NPM 方式**

   ```JavaScript
   import { createLivePlayer, register, live } from '@byteplus/veplayer';
   import { rtm, flv, hlsjs } from '@byteplus/veplayer-plugin';
   import '@byteplus/veplayer/style'
   register([rtm, flv, hlsjs]);
    
   createLivePlayer({
       height: 360,
       playlist: [
         {
           // The RTM stream uses the RTM address for Player SDK for Web.此地址支援自動轉碼，備援串流則使用 HLS 或 FLV 地址。
           definitions: [
             'https://pull-demo.example.com/live/st-4536521_autortm.sdp',
             'https://pull-demo.example.com/live/st-4536521.flv',
             'https://pull-demo.example.com/live/st-4536521.m3u8',
           ],
         },
       ],
       fallback: {
          // 1. Fallback to FLV if RTM is not supported or fails
         fallbackOrder: ['rtm', 'flv'],
         // 2. Fallback to HLS if RTM is not supported or fails
         // fallbackOrder: ['rtm', 'hls'],
         // 3. Fallback to FLV, then to HLS
         // fallbackOrder: ['rtm', 'flv', 'hls'],
       },
   }).then(function(veplayer) {
       veplayer.on(live.Events.FALLBACK_ERROR, function(){
           // Triggered when all fallback attempts have failed
       });
   })
   ```
   


</Tab>
<Tab zoneid="lFx7hFgayq" title="依錯誤類型條件備援">
<TabTitle>依錯誤類型條件備援</TabTitle>

您可設定播放器針對特定錯誤碼跳過備援。以下範例展示當錯誤碼為 2104（串流未找到）時如何跳過備援。


* **CDN 來源**

   ```JavaScript
   VePlayer.createLivePlayer({
       height: 360,
       playlist: [
         {
           definitions: [
             'https://pull-demo.example.com/live/st-4536521_autortm.sdp',
             'https://pull-demo.example.com/live/st-4536521.m3u8',
             'https://pull-demo.example.com/live/st-4536521.flv',
           ],
         },
       ],
       fallback: {
         fallbackOrder: ['rtm', 'flv', 'hls'],
         fallbackStrategy: {
           rtm: {
             Error: {
               // Do not fall back if the error code is 2104
               excludeList: [2104],
             },
           },
         },
       },
       rtm: {
           // Increase loadTimeout if 2104 error is not triggered
           loadTimeout: 15000,
       },
   }).then(function(veplayer) {
       veplayer.on(VePlayer.live.Events.FALLBACK_ERROR, function(){
           // All fallback attempts failed
       });
   })        
   ```
   

* **NPM 方式**

   ```JavaScript
   import { createLivePlayer, register, live } from '@byteplus/veplayer';
   import { rtm, flv, hlsjs } from '@byteplus/veplayer-plugin';
   import '@byteplus/veplayer/style'
   register([rtm, flv, hlsjs]);
    
   createLivePlayer({
       height: 360,
       playlist: [
         {
           definitions: [
             'https://pull-demo.example.com/live/st-4536521_autortm.sdp',
             'https://pull-demo.example.com/live/st-4536521.flv',
             'https://pull-demo.example.com/live/st-4536521.m3u8',
           ],
         },
       ],
       fallback: {
         fallbackOrder: ['rtm', 'flv', 'hls'],
         fallbackStrategy: {
           rtm: {
             Error: {
               // Do not fall back if the error code is 2104
               excludeList: [2104],
             },
           },
         },
       },
       rtm: {
           // Increase loadTimeout if 2104 error is not triggered
           loadTimeout: 15000,
       },
   }).then(function(veplayer) {
       veplayer.on(live.Events.FALLBACK_ERROR, function(){
           // All fallback attempts failed
       });
   })        
   ```
   


</Tab>
<Tab zoneid="KPSXfEEPoq" title="自訂備援順序">
<TabTitle>自訂備援順序</TabTitle>

預設情況下，播放器依 RTM、FLV、HLS 的順序嘗試播放。如需自訂此行為，您可定義備援順序。以下範例中，FLV 優先，其次為 RTM 和 HLS。播放器會依序嘗試各協議，直到其中一個成功或全部失敗。


* **CDN 來源**

   ```JavaScript
   VePlayer.createLivePlayer({
       height: 360,
       playlist: [
         {
           definitions: [
             'https://pull-demo.example.com/live/st-4536521_autortm.sdp',
             'https://pull-demo.example.com/live/st-4536521.m3u8',
             'https://pull-demo.example.com/live/st-4536521.flv',
           ],
         },
       ],
       fallback: {
         // Customize fallback order
         fallbackOrder: ['flv', 'rtm', 'hls'],
       },
   }).then(function(veplayer) {
       veplayer.on(VePlayer.live.Events.FALLBACK_ERROR, function(){
           // Playback failed after all protocols have been attempted
       });
   })        
   ```
   

* **NPM 方式**

   ```JavaScript
   import { createLivePlayer, register, live } from '@byteplus/veplayer';
   import { rtm, flv, hlsjs } from '@byteplus/veplayer-plugin';
   import '@byteplus/veplayer/style'
   register([rtm, flv, hlsjs]);
    
   createLivePlayer({
       height: 360,
       playlist: [
         {
           definitions: [
             'https://pull-demo.example.com/live/st-4536521_autortm.sdp',
             'https://pull-demo.example.com/live/st-4536521.flv',
             'https://pull-demo.example.com/live/st-4536521.m3u8',
           ],
         },
       ],
       fallback: {
         // Customize fallback order
         fallbackOrder: ['flv', 'rtm', 'hls'],
       },
   }).then(function(veplayer) {
       veplayer.on(live.Events.FALLBACK_ERROR, function(){
           // Playback failed after all protocols have been attempted
       });
   })        
   ```
   


</Tab>
</Tabs>


<span id="场景二：多清晰度或多线路拉流"></span>
### 場景二：多畫質或多路線串流

在較複雜的直播場景中，你可能需要提供多種畫質（品質等級）或多條路線（來自不同 CDN 節點的 URL）。你可以為每個來源指定協定及回退行為。以下為範例配置：


<Tabs>
<Tab zoneid="LPHcTqNCeY" title="依錯誤碼條件備援 RTM 失敗">
<TabTitle>依錯誤碼條件備援 RTM 失敗</TabTitle>

在多路串流場景下，RTM 播放失敗時，您可根據特定錯誤碼定義備援策略，以實現更靈活且穩定的播放。


* **CDN 來源**

   ```JavaScript
   VePlayer.createLivePlayer({
       height: 360,
       playlist: [
         {
           name: 'lineOne',
           text: 'lineOne',
           definitions: [
             {
               url: 'https://pull-demo.example.com/live/st-4536521_autortm.sdp',
               definition: 'uhd',
               text: 'uhd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536521_hd_autortm.sdp',
               definition: 'hd',
               text: 'hd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536521.m3u8',
               definition: 'uhd',
               text: 'uhd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536521_hd.m3u8',
               definition: 'hd',
               text: 'hd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536521.flv',
               definition: 'uhd',
               text: 'uhd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536521_hd.flv',
               definition: 'hd',
               text: 'hd',
             },
           ],
         },
         {
           name: 'lineTwo',
           text: 'lineTwo',
           definitions: [
             {
               url: 'https://pull-demo.example.com/live/st-4536523_autortm.sdp',
               definition: 'uhd',
               text: 'uhd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536523_hd_autortm.sdp',
               definition: 'hd',
               text: 'hd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536523.m3u8',
               definition: 'uhd',
               text: 'uhd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536523_hd.m3u8',
               definition: 'hd',
               text: 'hd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536523.flv',
               definition: 'uhd',
               text: 'uhd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536523_hd.flv',
               definition: 'hd',
               text: 'hd',
             },
           ],
         },
       ],
       fallback: {
         // Set fallback order: fallback from RTM to FLV, then to HLS
         fallbackOrder: ['rtm', 'flv', 'hls'],
         // Customize fallback strategy: do not fallback if error code is 2104 (stream offline)
         fallbackStrategy: {
           rtm: {
             Error: {
               excludeList: [2104],
             },
           },
         },
       },
   }).then(function(veplayer) {
       veplayer.on(VePlayer.live.Events.FALLBACK_ERROR, function(){
           // Playback failed after all protocols have been attempted
       });
   })
   ```
   

* **NPM 方式**

   ```JavaScript
   import { createLivePlayer, register, live } from '@byteplus/veplayer';
   import { rtm, flv, hlsjs } from '@byteplus/veplayer-plugin';
   import '@byteplus/veplayer/style'
   register([rtm, flv, hlsjs]);
    
   createLivePlayer({
       height: 360,
       playlist: [
         {
           name: 'lineOne',
           text: 'lineOne',
           definitions: [
             {
               url: 'https://pull-demo.example.com/live/st-4536521_autortm.sdp',
               definition: 'uhd',
               text: 'uhd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536521_hd_autortm.sdp',
               definition: 'hd',
               text: 'hd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536521.m3u8',
               definition: 'uhd',
               text: 'uhd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536521_hd.m3u8',
               definition: 'hd',
               text: 'hd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536521.flv',
               definition: 'uhd',
               text: 'uhd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536521_hd.flv',
               definition: 'hd',
               text: 'hd',
             },
           ],
         },
         {
           name: 'lineTwo',
           text: 'lineTwo',
           definitions: [
             {
               url: 'https://pull-demo.example.com/live/st-4536523_autortm.sdp',
               definition: 'uhd',
               text: 'uhd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536523_hd_autortm.sdp',
               definition: 'hd',
               text: 'hd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536523.m3u8',
               definition: 'uhd',
               text: 'uhd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536523_hd.m3u8',
               definition: 'hd',
               text: 'hd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536523.flv',
               definition: 'uhd',
               text: 'uhd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536523_hd.flv',
               definition: 'hd',
               text: 'hd',
             },
           ],
         },
       ],
       fallback: {
         // Set the fallback priority.若 RTM 失敗，則回退至 FLV。若 FLV 也失敗，則回退至 HLS。
         fallbackOrder: ['rtm', 'flv', 'hls'],
         // Customize fallback strategy: for example, prevent fallback on specific error codes such as "stream offline" (error code 2104)
         fallbackStrategy: {
           rtm: {
             Error: {
               excludeList: [2104],
             },
           },
         },
       },
   }).then(function(veplayer) {
       veplayer.on(live.Events.FALLBACK_ERROR, function(){
           // All protocol fallback attempts have failed
       });
   })            
   ```
   


</Tab>
<Tab zoneid="i6i7dov3ca" title="自訂備援優先順序">
<TabTitle>自訂備援優先順序</TabTitle>

預設情況下，播放器會先嘗試 RTM，然後備援至 FLV 或 HLS。如需更靈活的控制，您可配置自訂備援順序。下方範例中，FLV 優先，其次為 RTM，最後為 HLS。播放器會依序嘗試各協議，直到播放成功或全部失敗。


* **CDN 來源**

   ```JavaScript
   VePlayer.createLivePlayer({
       height: 360,
       playlist: [
         {
           name: 'lineOne',
           text: 'lineOne',
           definitions: [
             {
               url: 'https://pull-demo.example.com/live/st-4536521_autortm.sdp',
               definition: 'uhd',
               text: 'uhd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536521_hd_autortm.sdp',
               definition: 'hd',
               text: 'hd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536521.m3u8',
               definition: 'uhd',
               text: 'uhd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536521_hd.m3u8',
               definition: 'hd',
               text: 'hd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536521.flv',
               definition: 'uhd',
               text: 'uhd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536521_hd.flv',
               definition: 'hd',
               text: 'hd',
             },
           ],
         },
         {
           name: 'lineTwo',
           text: 'lineTwo',
           definitions: [
             {
               url: 'https://pull-demo.example.com/live/st-4536523_autortm.sdp',
               definition: 'uhd',
               text: 'uhd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536523_hd_autortm.sdp',
               definition: 'hd',
               text: 'hd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536523.m3u8',
               definition: 'uhd',
               text: 'uhd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536523_hd.m3u8',
               definition: 'hd',
               text: 'hd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536523.flv',
               definition: 'uhd',
               text: 'uhd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536523_hd.flv',
               definition: 'hd',
               text: 'hd',
             },
           ],
         },
       ],
       fallback: {
         // Custom fallback order
         fallbackOrder: ['flv', 'rtm', 'hls'],
       },
   }).then(function(veplayer) {
       veplayer.on(VePlayer.live.Events.FALLBACK_ERROR, function(){
           // All protocol fallback attempts have failed
       });
   })     
   ```
   

* **NPM 方式**

   ```JavaScript
   import { createLivePlayer, register, live } from '@byteplus/veplayer';
   import { rtm, flv, hlsjs } from '@byteplus/veplayer-plugin';
   import '@byteplus/veplayer/style'
   register([rtm, flv, hlsjs]);
    
   createLivePlayer({
       height: 360,
       playlist: [
         {
           name: 'lineOne',
           text: 'lineOne',
           definitions: [
             {
               url: 'https://pull-demo.example.com/live/st-4536521_autortm.sdp',
               definition: 'uhd',
               text: 'uhd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536521_hd_autortm.sdp',
               definition: 'hd',
               text: 'hd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536521.m3u8',
               definition: 'uhd',
               text: 'uhd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536521_hd.m3u8',
               definition: 'hd',
               text: 'hd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536521.flv',
               definition: 'uhd',
               text: 'uhd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536521_hd.flv',
               definition: 'hd',
               text: 'hd',
             },
           ],
         },
         {
           name: 'lineTwo',
           text: 'lineTwo',
           definitions: [
             {
               url: 'https://pull-demo.example.com/live/st-4536523_autortm.sdp',
               definition: 'uhd',
               text: 'uhd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536523_hd_autortm.sdp',
               definition: 'hd',
               text: 'hd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536523.m3u8',
               definition: 'uhd',
               text: 'uhd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536523_hd.m3u8',
               definition: 'hd',
               text: 'hd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536523.flv',
               definition: 'uhd',
               text: 'uhd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536523_hd.flv',
               definition: 'hd',
               text: 'hd',
             },
           ],
         },
       ],
       fallback: {
         // Custom fallback order
         fallbackOrder: ['flv', 'rtm', 'hls'],
       },
   }).then(function(veplayer) {
       veplayer.on(live.Events.FALLBACK_ERROR, function(){
           // All protocol fallback attempts have failed
       });
   })   
   ```
   


</Tab>
</Tabs>


<span id="常见问题"></span>
## 常見問題

<span id="如何检测协议兼容性？"></span>
### 如何檢測協定相容性

初始化播放來源時，VePlayer 會自動檢測瀏覽器是否支援 RTM 或 FLV 協定，以判斷是否觸發回退。


* 判斷 RTM 播放支援的邏輯如下：

   * `isRTMSupported()`：若瀏覽器支援 RTM 播放則回傳`true`。

   * `isRTMSupportCodec()`：若瀏覽器支援 RTM 所需的音訊與視訊編解碼器則回傳`true`。

   * 只有當兩者皆回傳`true`時，VePlayer 才會嘗試拉取 RTM 串流；否則將啟動備援機制。

* 判斷 FLV 播放支援的邏輯如下：

   `isFLVSupported()`：若瀏覽器能透過 Media Source Extensions (MSE) 播放 FLV 串流，則回傳`true`。
