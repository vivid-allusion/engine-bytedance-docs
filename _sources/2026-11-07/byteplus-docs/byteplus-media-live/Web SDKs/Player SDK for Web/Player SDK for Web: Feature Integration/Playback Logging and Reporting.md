---
title: "Playback Logging and Reporting"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-playback-logging-and-reporting"
---

This document describes how to enable playback logging and reporting using the Web Player SDK (VePlayer). This feature allows you to collect playback data for troubleshooting and analysis, helping improve the stability and user experience of your application. Once enabled, the SDK sends playback\-related information to BytePlus MediaLive servers.

<span id="适用版本"></span>
## Applicable to

This document is applicable to **the latest version** of the Web Player SDK. For version information, please refer to [Player SDK for Web: Release notes](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-changelog_2). For past versions, please refer to [Legacy versions](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-web-1-x-versions).

<span id="前提条件"></span>
## Prerequisites

Ensure that the SDK has been integrated into your project by following the instructions provided in [Integrating the Player SDK for Web](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-player-sdk-for-web_1).

<span id="集成步骤"></span>
## Integration Steps


1. Log in to the [BytePlus MediaLive console](https://console.byteplus.com/live/main/sdk), go to the **App Management** page, and locate the **AppID** of your existing Web application.

2. Pass the `appId` to the `logger` field in the player configuration to enable logging. See the code examples below.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><code>appId</code> uniquely identifies your Web application and <strong>must be configured correctly</strong>.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Starting from version 2.5.1, failure to configure <code>appId</code> will trigger a console error and the SDK will report logs using a default <code>appId</code>.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">It is <strong>strongly recommended</strong> to pass both <code>userId</code> and <code>deviceId</code>. These identifiers help pinpoint playback issues more efficiently.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If <code>userId</code> and <code>deviceId</code> are not provided, the SDK will generate random values based on the user's browser and store them locally.   </div>
   

   
   <Tabs>
   <Tab zoneid="zIuueHVFhd" title="From CDN">
   <TabTitle>From CDN</TabTitle>
   
   ```JavaScript
   VePlayer.createLivePlayer({
     width: 640,
     height: 360,
     url: 'https://pulldomain/appname/mystream.flv',
     logger: {
       appId: '2****4',
       userId: '1********6',
       deviceId: '3********7',
     },
   });
   ```
   
   
   
   </Tab>
   <Tab zoneid="Mb9CbgR0Lc" title="By NPM">
   <TabTitle>By NPM</TabTitle>
   
   ```JavaScript
   import { createLivePlayer, register } from '@byteplus/veplayer';
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
   });
   ```
   
   
   
   </Tab>
   </Tabs>
   

3. If playback issues occur during a live stream, collect relevant information such as the playback time and observed symptoms, and please [contact support](https://console.byteplus.com/workorder/create).
