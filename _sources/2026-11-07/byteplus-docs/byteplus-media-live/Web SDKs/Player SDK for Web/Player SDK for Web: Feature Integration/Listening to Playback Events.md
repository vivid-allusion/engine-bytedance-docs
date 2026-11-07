---
title: "Listening to Playback Events"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listening-to-playback-events"
---

This document describes how to use the Web Player SDK (VePlayer) to listen for playback\-related events. These event listeners can be used to support features such as player status monitoring, log reporting, and dynamic UI updates.

<span id="适用版本"></span>
## Applicable to

This document is applicable to **the latest version** of the Web Player SDK. For version information, please refer to [Player SDK for Web: Release notes](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-changelog_2). For past versions, please refer to [Legacy versions](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-web-1-x-versions).

<span id="前提条件"></span>
## Prerequisites

Ensure that the SDK has been integrated into your project by following the instructions provided in [Integrating the Player SDK for Web](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-player-sdk-for-web_1).

<span id="89738846"></span>
## Configuration Examples

The Web Player SDK supports a wide range of playback events such as:


* `PLAY` – Playback started

* `ERROR` – Playback error occurred

* `PAUSE` – Playback paused


These events can be used to trigger UI updates or handle exceptional playback scenarios. For a full list of supported events, refer to the [Event Reference](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1158676).

After successfully creating a live player instance, use the `on`, `once`, and `off` methods to bind and remove event listeners.


<Tabs>
<Tab zoneid="CwZCQ1rXKq" title="From CDN">
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
  function eventHandler(data) {
    console.log('Event callback data:', data);
  }

  // Bind an event listener
  veplayer.on(VePlayer.live.Events.PLAY, eventHandler);

  // Bind a one-time event listener
  veplayer.once(VePlayer.live.Events.PLAY, eventHandler);

  // Remove a specific event listener
  veplayer.off(VePlayer.live.Events.PLAY, eventHandler);

  // Remove all event listeners
  veplayer.offAll();
});
```



</Tab>
<Tab zoneid="qIMCt9yJ0x" title="By NPM">
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
  function eventHandler(data) {
    console.log('Event callback data:', data);
  }

  // Bind an event listener
  veplayer.on(live.Events.PLAY, eventHandler);

  // Bind a one-time event listener
  veplayer.once(live.Events.PLAY, eventHandler);

  // Remove a specific event listener
  veplayer.off(live.Events.PLAY, eventHandler);

  // Remove all event listeners
  veplayer.offAll();
});
```



</Tab>
</Tabs>
