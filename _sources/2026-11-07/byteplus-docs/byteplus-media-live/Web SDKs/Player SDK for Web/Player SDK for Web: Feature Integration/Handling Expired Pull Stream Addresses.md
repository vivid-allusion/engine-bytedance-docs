---
title: "Handling Expired Pull Stream Addresses"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-handling-expired-pull-stream-addresses"
---

This document provides guidance on how to identify and handle playback failures caused by expired pull stream addresses when using the Web Player SDK (VePlayer) to access live streaming systems with URL authentication enabled. This helps ensure a smooth viewing experience for your audience.

<span id="适用版本"></span>
## Applicable to

This document is applicable to **the latest version** of the Web Player SDK. For version information, please refer to [Player SDK for Web: Release notes](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-changelog_2). For past versions, please refer to [Legacy versions](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-web-1-x-versions).

<span id="7af6b48c"></span>
## Use Cases

If your live streaming system has [URL authentication](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-url-authentication) enabled, the generated pull stream address typically has an expiration time. When a viewer stays on the page for too long or due to other reasons the pull stream address expires, the following issues may occur:


* The player fails to fetch the stream, interrupting playback.

* Viewers see an error message and are unable to continue watching the live stream.


To prevent interruptions, you must **retrieve a new pull stream address** and **switch the player source** in time—either before the current address expires or immediately after a failure is detected.

<span id="实现流程"></span>
## Workflow


1. Use a valid authenticated pull stream address when initializing the player.

2. Set up error listeners or timers to detect expiration proactively.

3. Use your backend server to call the [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) API to obtain a new valid pull stream address.

4. Switch the stream source using the `veplayer.switch()` method.


<span id="前提条件"></span>
## Prerequisites


* Ensure that the SDK has been integrated into your project by following the instructions provided in [Integrating the Player SDK for Web](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-player-sdk-for-web_1).

* [URL authentication](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-url-authentication) is enabled in your streaming setup.

* Your system supports calling the [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) API to dynamically generate new authenticated pull stream addresses.


<span id="配置示例"></span>
## Configuration Examples

You can use the `veplayer.switch(newUrl)` method to dynamically update the pull stream address. The following examples show how to implement this using both CDN and NPM integration methods:


<Tabs>
<Tab zoneid="XYVcTYmCQw" title="From CDN">
<TabTitle>From CDN</TabTitle>

```JavaScript
VePlayer.createLivePlayer({
  width: 640,
  height: 360,
  url: 'https://testpull.mycloud.com/live/mystream.m3u8?{authParams}',
  logger: {
    appId: '5****8',
  },
}).then(function (veplayer) {
  // New pull stream address with refreshed authentication
  const newUrl =
    'https://testpull.mycloud.com/live/mystream.m3u8?{newAuthParams}';
  // Update the stream source
  veplayer.switch(newUrl);
});
```



</Tab>
<Tab zoneid="N0TTrQAGfx" title="By NPM">
<TabTitle>By NPM</TabTitle>

```JavaScript
import { createLivePlayer, register } from '@byteplus/veplayer';
import { hlsjs } from '@byteplus/veplayer-plugin';
import '@byteplus/veplayer/style'
register([hlsjs]);

createLivePlayer({
  width: 640,
  height: 360,
  url: 'https://testpull.mycloud.com/live/mystream.m3u8?{authParams}',
  logger: {
    appId: '5****8',
  },
}).then(function (veplayer) {
  // New pull stream address with refreshed authentication
  const newUrl =
    'https://testpull.mycloud.com/live/mystream.m3u8?{newAuthParams}';
  // Update the stream source
  veplayer.switch(newUrl);
});
```



</Tab>
</Tabs>
