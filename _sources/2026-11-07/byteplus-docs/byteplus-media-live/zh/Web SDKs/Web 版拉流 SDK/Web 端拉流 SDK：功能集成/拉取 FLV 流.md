---
title: "拉取 FLV 流"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-flv-streaming-integration-zh-CN"
---

为在**浏览器中实现低至中延迟回放**，且**无法部署 LL\-HLS 或 RTM 协议**的场景，可以通过拉流 SDK for Web（VePlayer）集成**FLV 回放**。本文提供适用于如娱乐直播或在线教育等场景的必要配置示例。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">建议使用最新版本的拉流 SDK for Web。版本信息，请参见<a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-changelog_2-zh-CN">Web 拉流 SDK：版本说明</a>。历史版本信息，请参见<a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-web-1-x-versions-zh-CN">Web 端拉流 SDK：1.x 版本</a>。</div>


<span id="12561c10"></span>
## 环境要求

VePlayer 会检测浏览器是否支持 FLV 直播流回放。在开始集成前，请确保开发环境满足以下条件：


* **PC 和 Android 浏览器**必须支持[Media Source Extensions](https://caniuse.com/?search=Media%20Source%20Extensions) API。

* **iOS 浏览器**必须支持[ManagedMediaSource](https://caniuse.com/?search=ManagedMediaSource) API。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">对于 FLV 直播流回放，视频级别不得超过<strong>level 6</strong>。更多信息，请参考<a href="https://en.wikipedia.org/wiki/Advanced_Video_Coding#Levels">Advanced Video Coding</a>。</div>


* <div data-tips="true" data-tips-type="tip">部分不支持 MSE 的 Android 浏览器可能会使用其内置播放器播放 FLV，但无法通过程序检测。</div>



<span id="前提条件"></span>
## 前提条件

你已集成拉流 SDK for Web。更多信息，请参见[集成 Web 端拉流 SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-player-sdk-for-web_1-zh-CN)。

<span id="配置示例"></span>
## 配置示例

VePlayer 支持通过**CDN**和**NPM**两种方式集成。请根据项目需求选择合适的方式。在以下示例中，配置了多个拉流地址，并设置了**回退顺序**。若浏览器不支持 FLV 回放，播放器将自动回退至 HLS 协议。


<Tabs>
<Tab zoneid="MPqBKIh05l" title="通过 CDN">
<TabTitle>通过 CDN</TabTitle>

通过 CDN 集成时，请在 HTML 文件中引入 VePlayer 的 CDN 资源，并按如下方式配置播放器参数：

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
<Tab zoneid="DVX0cCMgoe" title="通过 NPM">
<TabTitle>通过 NPM</TabTitle>

通过 NPM 集成时，请安装 VePlayer 的 NPM 包，并按如下所示导入所需模块：

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
