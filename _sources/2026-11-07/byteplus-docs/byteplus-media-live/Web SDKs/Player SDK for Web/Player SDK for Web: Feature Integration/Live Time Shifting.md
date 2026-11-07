---
title: "Live Time Shifting"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-live-time-shifting"
---

This document describes how to enable live time shifting using the Web Player SDK (VePlayer). This feature allows users to rewind and replay recent live content by dragging the timeline during a live stream. It is useful in scenarios such as lecture replays, meeting reviews, and other time\-sensitive content, enhancing the overall viewing experience.

<span id="适用版本"></span>
## Applicable to

This document is applicable to **the latest version** of the Web Player SDK. For version information, please refer to [Player SDK for Web: Release notes](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-changelog_2). For past versions, please refer to [Legacy versions](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-web-1-x-versions).

<span id="前提条件"></span>
## Prerequisites

Ensure that the SDK has been integrated into your project by following the instructions provided in [Integrating the Player SDK for Web](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-player-sdk-for-web_1).

<span id="集成步骤"></span>
## Integration Steps


1. Configure a time shifting task in the BytePlus MediaLive console. Refer to [Configuring a time shifting task](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-time-shifting) for detailed instructions on the configurations.

2. Generate an M3U8\-format pull stream address using the domain name and `appName` configured in the previous step, see [Generating live-stream addresses](https://docs.byteplus.com/docs/byteplus-media-live/docs-generating-live-stream-addresses).

3. Pass the address that you have prepared in the previous step to the player. See [TimeShiftConfig](https://docs.byteplus.com/en/byteplus-media-live/docs/1155423#timeshiftconfig).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Specify the <code>liveStartTime</code> with the current time from the local browser.   </div>
   

4. Introduce the time shifting plugin. The sample code is given below:

   
   <Tabs>
   <Tab zoneid="HFLKu52lGr" title="From CDN">
   <TabTitle>From CDN</TabTitle>
   
   ```HTML
   <script src="https://sf-unpkg.bytepluscdn.com/obj/byteplusfe-sg/sdk/@byteplus/veplayer/2.8.2/umd/veplayer.plugin.time.shift.production.js"></script><link rel="stylesheet" href="https://sf-unpkg.bytepluscdn.com/obj/byteplusfe-sg/sdk/@byteplus/veplayer/2.8.2/umd/veplayer.plugin.time.shift.production.css">
   ```
   
   
   
   </Tab>
   <Tab zoneid="yf377PUrHR" title="By NPM">
   <TabTitle>By NPM</TabTitle>
   
   ```JavaScript
   import { timeShift } from '@byteplus/veplayer-plugin';
   import '@byteplus/veplayer-plugin/time-shift/style';
   ```
   
   
   
   </Tab>
   </Tabs>
   

5. Pass in the time\-shifting plugin as a configuration in the VePlayer object. Refer to [TimeShiftConfig](https://docs.byteplus.com/docs/byteplus-media-live/docs-1155423#timeshiftconfig) for the parameter description relating to time shifting.

   
   <Tabs>
   <Tab zoneid="mKKpRXfMx9" title="From CDN">
   <TabTitle>From CDN</TabTitle>
   
   ```JavaScript
   VePlayer.createLivePlayer({
     width: 640,
     height: 360,
     url: 'https://testpull.mycloud.com/live/mystream.m3u8',
     timeShift: {
       liveStartTime: Date.now() / 1000 - 60,
     },
     plugins: [window.VePlayerTimeShift],
     logger: {
       appId: '5****8',
     },
   });
   ```
   
   
   
   </Tab>
   <Tab zoneid="DnTbzhlEbt" title="By NPM">
   <TabTitle>By NPM</TabTitle>
   
   ```JavaScript
   register([hls]);
   
   createLivePlayer({
     width: 640,
     height: 360,
     url: 'https://testpull.mycloud.com/live/mystream.m3u8',
     timeShift: {
       liveStartTime: Date.now() / 1000 - 60,
     },
     plugins: [timeShift],
     logger: {
       appId: '5****8',
     },
   });
   ```
   
   
   
   </Tab>
   </Tabs>
