---
title: "LL-HLS Streaming Integration"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-ll-hls-streaming-integration"
---

This document describes how to use the Web Player SDK (VePlayer) to play live streams using the **Low\-Latency HLS (LL\-HLS)**  protocol. LL\-HLS enables sub\-second latency playback in the browser, making it suitable for scenarios such as live commerce and interactive quizzes, where low latency is essential.

<span id="适用版本"></span>
## Applicable to

This document is applicable to **the latest version** of the Web Player SDK. For version information, please refer to [Player SDK for Web: Release notes](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-changelog_2). For past versions, please refer to [Legacy versions](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-web-1-x-versions).

<span id="a7dc162d"></span>
## Prerequisites


* Ensure that the SDK has been integrated into your project by following the instructions provided in [Integrating the Player SDK for Web](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-player-sdk-for-web_1).

* On Android devices, the browser must support and enable Media Source Extensions (MSE).


<span id="配置示例"></span>
## Configuration Examples

VePlayer supports LL\-HLS playback via both **CDN integration** and **NPM package installation**. Choose the method that best fits your project setup.


<Tabs>
<Tab zoneid="PbKjFj6OJ5" title="From CDN">
<TabTitle>From CDN</TabTitle>

```JavaScript
VePlayer.createLivePlayer({
  width: 640,
  height: 360,
  url: 'https://pull.example.com/live/llhls-stream.m3u8',
  hls: {
    enableMSE: VePlayer.Sniffer.os.isAndroid ? true : false
  },
  logger: {
    appId: '5****8',
  },
}) 
```



</Tab>
<Tab zoneid="Xa7vLfDdzp" title="By NPM">
<TabTitle>By NPM</TabTitle>

```JavaScript
import { createLivePlayer, register, live, Sniffer} from '@byteplus/veplayer'
import { hls } from '@byteplus/veplayer-plugin'
import '@byteplus/veplayer/style'
        
register([hls]);
        
createLivePlayer({
  width: 640,
  height: 360,
  url: 'https://pull.example.com/live/llhls-stream.m3u8',
  hls: {
    enableMSE: Sniffer.os.isAndroid ? true : false
  },
  logger: {
    appId: '5****8',
  },
})  
```



</Tab>
</Tabs>
