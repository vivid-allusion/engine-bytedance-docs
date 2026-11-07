---
title: "Handling Playback Errors"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-handling-playback-errors"
---

This document explains how to use the Web Player SDK (VePlayer) to listen for playback errors, helping you identify issues and enhance the player’s fault tolerance.

<span id="适用版本"></span>
## Applicable to

This document is applicable to **the latest version** of the Web Player SDK. For version information, please refer to [Player SDK for Web: Release notes](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-changelog_2). For past versions, please refer to [Legacy versions](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-web-1-x-versions).

<span id="70cf27ae"></span>
## Prerequisites

Ensure that the SDK has been integrated into your project by following the instructions provided in [Integrating the Player SDK for Web](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-player-sdk-for-web_1).

<span id="921af388"></span>
## Configuration Examples

After successfully creating a live player instance, you can listen for playback errors by binding to the `ERROR` event. You can then handle different error codes accordingly.

For a full list of error codes and their descriptions, see the [Error Code Reference](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1158675).


<Tabs>
<Tab zoneid="fBpldVT625" title="From CDN">
<TabTitle>From CDN</TabTitle>

```JavaScript
VePlayer.createLivePlayer({
  width: 640,
  height: 360,
  url: 'https://pulldomain/appname/mystream.m3u8',
  logger: {
    appId: '5****8',
  },
}).then(function (veplayer) {
  function errorHandler(error) {
    console.log('The error that occurs', error);
    console.log('The error code', error.errorCode);
    console.log('The error message', error.message);
  }
  // Listen for the ERROR event
  veplayer.on(VePlayer.live.Events.ERROR, errorHandler);
});        
```



</Tab>
<Tab zoneid="rK1aLbbWOF" title="By NPM">
<TabTitle>By NPM</TabTitle>

```JavaScript
import { createLivePlayer, register, live } from '@byteplus/veplayer';
import { hlsjs } from '@byteplus/veplayer-plugin';
import '@byteplus/veplayer/style';

register([hlsjs]);

createLivePlayer({
  width: 640,
  height: 360,
  url: 'https://pulldomain/appname/mystream.m3u8',
  logger: {
    appId: '5****8',
  },
}).then(function (veplayer) {
  function errorHandler(error) {
    console.log('The error that occurs', error);
    console.log('The error code', error.errorCode);
    console.log('The error message', error.message);
  }
  // Listen for the ERROR event
  veplayer.on(live.Events.ERROR, errorHandler);
});
```



</Tab>
</Tabs>
