---
title: "拉取 LL-HLS 流"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-ll-hls-streaming-integration-zh-CN"
---

使用 Web 端拉流 SDK（VePlayer）播放 LL\-HLS 流，可在浏览器中实现亚秒级的超低延时直播。此功能对于延时敏感且高度互动的场景至关重要，例如直播电商和互动答题。本文介绍如何拉取 LL\-HLS 流。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">建议使用最新版本的 Web 端拉流 SDK。版本信息，请参见<a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-changelog_2-zh-CN">Web 拉流 SDK：版本说明</a>。历史版本，请参见<a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-web-1-x-versions-zh-CN">Web 端拉流 SDK：1.x 版本</a>。</div>


<span id="a7dc162d"></span>
## 前提条件


* 你已集成 Web 端拉流 SDK。更多信息，请参见[集成 Web 端拉流 SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-player-sdk-for-web_1-zh-CN)。

* 在 Android 设备上，浏览器必须支持 Media Source Extensions（MSE）。


<span id="配置示例"></span>
## 配置示例

VePlayer 支持通过**CDN 集成**和**NPM 包安装**两种方式回放 LL\-HLS。请选择最适合你项目配置的方法。


<Tabs>
<Tab zoneid="X6TuLtBnx5" title="通过 CDN">
<TabTitle>通过 CDN</TabTitle>

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
<Tab zoneid="YModzYPSUJ" title="通过 NPM">
<TabTitle>通过 NPM</TabTitle>

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
