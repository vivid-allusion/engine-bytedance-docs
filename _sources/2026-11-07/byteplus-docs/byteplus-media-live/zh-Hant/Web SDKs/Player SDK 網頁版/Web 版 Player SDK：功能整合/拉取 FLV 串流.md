---
title: "拉取 FLV 串流"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-flv-streaming-integration-zh-TW"
---

為了在**低至中延遲播放的瀏覽器**中，且**LL\-HLS 或 RTM 協議無法部署**時，您可以使用 Player SDK for Web（VePlayer）整合**FLV 播放**。本主題提供適用於如娛樂直播或線上教育等場景所需的配置範例。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">建議您使用最新版本的 Player SDK for Web。版本資訊請參閱<a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-changelog_2-zh-TW">Player SDK for Web：發行說明</a>。舊版本請參閱<a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-web-1-x-versions-zh-TW">Web 端播放器 SDK：1.x 版本</a>。</div>


<span id="12561c10"></span>
## 環境需求

VePlayer 會檢查瀏覽器是否支援 FLV 直播串流播放。在開始整合前，請確保您的開發環境符合以下條件：


* **PC 與 Android 瀏覽器**必須支援[Media Source Extensions](https://caniuse.com/?search=Media%20Source%20Extensions) API。

* **iOS 瀏覽器**必須支援[ManagedMediaSource](https://caniuse.com/?search=ManagedMediaSource) API。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">對於 FLV 直播串流播放，影片等級不得超過<strong>level 6</strong>。詳情請參閱<a href="https://en.wikipedia.org/wiki/Advanced_Video_Coding#Levels">Advanced Video Coding</a>。</div>


* <div data-tips="true" data-tips-type="tip">部分不支援 MSE 的 Android 瀏覽器可能會使用其內建播放器播放 FLV，但此情況無法以程式方式偵測。</div>



<span id="前提条件"></span>
## 先決條件

您已整合 Player SDK for Web。如需更多資訊，請參閱[整合 Web 端 Player SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-player-sdk-for-web_1-zh-TW)。

<span id="配置示例"></span>
## 配置範例

VePlayer 支援透過**CDN**與**NPM**兩種方式整合。請根據您的專案需求選擇合適的方法。在以下範例中，配置了多個拉流地址並設置**備援順序**。若瀏覽器不支援 FLV 播放，播放器將自動切換至 HLS 協議。


<Tabs>
<Tab zoneid="xJ7NWqiesF" title="來自 CDN">
<TabTitle>來自 CDN</TabTitle>

透過 CDN 整合時，請在 HTML 檔案中引入 VePlayer 的 CDN 資源，並按如下方式配置播放器參數：

```JavaScript
VePlayer.createLivePlayer({
    playlist: [
      {
        definitions: [
          'https://xxx.flv',
          'https://xxx.m3u8',
        ],
      },
    ],
    fallback: {
      fallbackOrder: ['flv', 'hls'],
    },
})
```



</Tab>
<Tab zoneid="dlb0IMPtDm" title="透過 NPM">
<TabTitle>透過 NPM</TabTitle>

透過 NPM 整合時，請安裝 VePlayer 的 NPM 套件並依下方所示匯入所需模組：

```JavaScript
import { createLivePlayer, register } from '@byteplus/veplayer';
import { hlsjs, flv } from '@byteplus/veplayer-plugin';
import '@byteplus/veplayer/style'
register([hlsjs, flv]);
 
createLivePlayer({
    playlist: [
      {
        definitions: [
          'https://xxx.flv',
          'https://xxx.m3u8',
        ],
      },
    ],
    fallback: {
      fallbackOrder: ['flv', 'hls'],
    },
})
```



</Tab>
</Tabs>
