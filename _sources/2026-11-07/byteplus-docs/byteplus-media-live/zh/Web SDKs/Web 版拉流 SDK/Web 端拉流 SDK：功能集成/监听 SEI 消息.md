---
title: "监听 SEI 消息"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listening-to-sei-messages-zh-CN"
---

SEI（Supplemental Enhancement Information，补充增强信息）消息作为嵌入在视频流中的数据通道。这为自定义数据与特定视频帧的同步提供了一种方式，常用于在特定时间点展示交互内容，如答题、弹幕或虚拟道具。这为观众带来了更丰富、更具互动性的观看体验。本主题介绍如何使用拉流 SDK for Web（VePlayer）监听并处理来自视频流的 SEI 消息。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">建议你使用最新版本的拉流 SDK for Web。版本信息，请参见 <a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-changelog_2-zh-CN">Web 拉流 SDK：版本说明</a>。历史版本，请参见 <a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-web-1-x-versions-zh-CN">Web 端拉流 SDK：1.x 版本</a>。</div>


<span id="c6282244"></span>
## SEI 消息格式

当播放器接收到 SEI 消息时，会触发 `SEI` 事件，并包含以下数据：

```javascript
interface Data {
  originPts: number; // Original PTS.源流中视频帧的时间戳。
  pts: number; // Adjusted PTS.在直播场景下，播放器会根据观众的加入时间将显示时间戳重置为从 0 开始。
  time: number; // The time (in seconds) at which the SEI message occurs in the current live stream.
  data: {
    payload: Uint8Array; // The SEI payload.
    type: number;        // Type of the SEI message.
    size: number;        // Size of the SEI payload.
    uuid: string;        // UUID of the SEI message.若无则为空。
  }
}
```


<span id="前提条件"></span>
## 前提条件

你已集成拉流 SDK for Web。更多信息，请参见 [集成 Web 端拉流 SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-player-sdk-for-web_1-zh-CN)。

<span id="022c49f2"></span>
## 配置示例

创建 VePlayer 实例后，你可以通过订阅 `VePlayer.live.Events.SEI` 事件来监听 SEI 消息，具体示例如下。


<Tabs>
<Tab zoneid="WpGjkp8ake" title="通过 CDN">
<TabTitle>通过 CDN</TabTitle>

```JavaScript
VePlayer.createLivePlayer({
  width: 640,
  height: 360,
  url: 'https://pull.example.com/live/stream1.flv',
  logger: {
    appId: '5****8',
  },
}).then(function (veplayer) {
  veplayer.on(VePlayer.live.Events.SEI, function (data) {
    console.info('SEI message', data);
  });
});        
```



</Tab>
<Tab zoneid="FWuRNGlGJ0" title="通过 NPM">
<TabTitle>通过 NPM</TabTitle>

```JavaScript
import { createLivePlayer, register, live } from '@byteplus/veplayer';
import { flv } from '@byteplus/veplayer-plugin';
import '@byteplus/veplayer/style'

register([flv]);

createLivePlayer({
  width: 640,
  height: 360,
  url: 'https://pulldomain/appname/mystream.flv',
  logger: {
    appId: '2****4',
    userId: '1********6',
    deviceId: '3********7',
  },
}).then(function (veplayer) {
  veplayer.on(live.Events.SEI, function (data) {
    console.info('SEI message', data);
  });
}); 
```



</Tab>
</Tabs>
