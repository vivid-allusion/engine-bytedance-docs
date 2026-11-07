---
title: "FLV Streaming Integration"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-flv-streaming-integration"
---

This document provides integration guidance for **FLV playback** using the Web Player SDK (VePlayer). This functionality is suitable for scenarios requiring **low to medium latency playback in browsers** where **LL\-HLS or RTM protocols are not deployable**, such as in live entertainment or online education.

<span id="适用版本"></span>
## Applicable to

This document is applicable to **the latest version** of the Web Player SDK. For version information, please refer to [Player SDK for Web: Release notes](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-changelog_2). For past versions, please refer to [Legacy versions](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-web-1-x-versions).

<span id="12561c10"></span>
## Environment Requirements

VePlayer checks whether the browser supports FLV live stream playback. Before starting integration, ensure your development environment meets the following conditions:


* **PC and Android browsers** must support the [Media Source Extensions](https://caniuse.com/?search=Media%20Source%20Extensions) API.

* **iOS browsers** must support the [ManagedMediaSource](https://caniuse.com/?search=ManagedMediaSource) API.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For FLV live stream playback, the video level must not exceed <strong>level 6</strong>. For more information, refer to <a href="https://en.wikipedia.org/wiki/Advanced_Video_Coding#Levels">Advanced Video Coding</a>.</div>


* <div data-tips="true" data-tips-type="tip">Some Android browsers that do not support MSE may play FLV using their built\-in players, but this cannot be detected programmatically.</div>



<span id="前提条件"></span>
## Prerequisites

Ensure that the SDK has been integrated into your project by following the instructions provided in [Integrating the Player SDK for Web](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-player-sdk-for-web_1).

<span id="配置示例"></span>
## Configuration Examples

VePlayer supports integration via both **CDN** and **NPM**. Choose the appropriate method based on your project needs. In the following examples, multiple pull stream addresses are configured with a **fallback order**. If the browser does not support FLV playback, the player will automatically fall back to the HLS protocol.


<Tabs>
<Tab zoneid="sP5UXSd0rq" title="From CDN">
<TabTitle>From CDN</TabTitle>

When integrating via CDN, include VePlayer's CDN resources in your HTML file and configure the player parameters as follows:

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
<Tab zoneid="c9qQS8fDFl" title="By NPM">
<TabTitle>By NPM</TabTitle>

When integrating via NPM, install the VePlayer NPM packages and import the required modules as shown below:

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
