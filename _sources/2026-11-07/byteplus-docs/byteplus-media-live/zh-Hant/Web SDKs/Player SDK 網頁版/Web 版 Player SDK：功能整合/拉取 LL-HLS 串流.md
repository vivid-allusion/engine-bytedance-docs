---
title: "拉取 LL-HLS 串流"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-ll-hls-streaming-integration-zh-TW"
---

使用 Player SDK for Web（VePlayer）播放 LL\-HLS 串流，可在瀏覽器中實現亞秒級、超低延遲的即時串流播放。此功能對於對延遲敏感且高度互動的場景至關重要，例如直播電商和互動問答。本主題說明如何拉取 LL\-HLS 串流。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">建議你使用最新版的 Player SDK for Web。版本資訊請參見<a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-changelog_2-zh-TW">Player SDK for Web：發行說明</a>。舊版資訊請參見<a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-web-1-x-versions-zh-TW">Web 端播放器 SDK：1.x 版本</a>。</div>


<span id="a7dc162d"></span>
## 先決條件


* 你已整合 Player SDK for Web。如需更多資訊，請參見[整合 Web 端 Player SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-player-sdk-for-web_1-zh-TW)。

* 在 Android 裝置上，瀏覽器必須支援 Media Source Extensions（MSE）。


<span id="配置示例"></span>
## 配置範例

VePlayer 支援透過**CDN 集成**和**NPM 套件安裝**兩種方式播放 LL\-HLS。請選擇最適合你專案配置的方法。


<Tabs>
<Tab zoneid="sx1yLamnFO" title="來自 CDN">
<TabTitle>來自 CDN</TabTitle>

```JavaScript
VePlayer.createLivePlayer({
  width: 640,
  height: 360,
  url: 'https://pull.example.com/live/llhls-stream.m3u8',
  logger: {
    appId: '5****8',
  },
}) 
```



</Tab>
<Tab zoneid="pPLPV28gQf" title="透過 NPM">
<TabTitle>透過 NPM</TabTitle>

```JavaScript
import { createLivePlayer, register, live, Sniffer} from '@byteplus/veplayer'
import { hlsjs } from '@byteplus/veplayer-plugin'
import '@byteplus/veplayer/style'
        
register([hlsjs]);
        
createLivePlayer({
  width: 640,
  height: 360,
  url: 'https://pull.example.com/live/llhls-stream.m3u8',
  logger: {
    appId: '5****8',
  },
})  
```



</Tab>
</Tabs>
