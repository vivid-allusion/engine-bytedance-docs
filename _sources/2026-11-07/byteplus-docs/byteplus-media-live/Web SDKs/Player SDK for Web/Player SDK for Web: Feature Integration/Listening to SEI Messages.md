---
title: "Listening to SEI Messages"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listening-to-sei-messages"
---

This document describes how to use the Web Player SDK (VePlayer) to listen for and handle SEI (Supplemental Enhancement Information) messages embedded in the video stream. SEI messages provide a synchronized data channel alongside video frames, commonly used to trigger interactive features at specific time points—such as quizzes, bullet comments, or virtual items—enhancing audience engagement.

<span id="适用版本"></span>
## Applicable to

This document is applicable to **the latest version** of the Web Player SDK. For version information, please refer to [Player SDK for Web: Release notes](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-changelog_2). For past versions, please refer to [Legacy versions](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-web-1-x-versions).

<span id="c6282244"></span>
## SEI Message Format

When the player receives an SEI message, it emits a `SEI` event containing the following data:

```javascript
interface Data {
  originPts: number; // Original PTS. Timestamp of the video frame in the push stream.
  pts: number; // Adjusted PTS. In live scenarios, the player resets the display timestamp to start from 0 based on the viewer's join time.
  time: number; // The time (in seconds) at which the SEI message occurs in the current live stream.
  data: {
    payload: Uint8Array; // The SEI payload.
    type: number;        // Type of the SEI message.
    size: number;        // Size of the SEI payload.
    uuid: string;        // UUID of the SEI message. Empty if not present.
  }
}
```


<span id="前提条件"></span>
## Prerequisites

Ensure that the SDK has been integrated into your project by following the instructions provided in [Integrating the Player SDK for Web](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-player-sdk-for-web_1).

<span id="022c49f2"></span>
## Configuration Examples

After creating a VePlayer instance, you can listen to SEI messages by subscribing to the `VePlayer.live.Events.SEI` event, as shown in the examples below.


<Tabs>
<Tab zoneid="BmLDZlBHjc" title="From CDN">
<TabTitle>From CDN</TabTitle>

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
<Tab zoneid="nLVhJwASRN" title="By NPM">
<TabTitle>By NPM</TabTitle>

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
