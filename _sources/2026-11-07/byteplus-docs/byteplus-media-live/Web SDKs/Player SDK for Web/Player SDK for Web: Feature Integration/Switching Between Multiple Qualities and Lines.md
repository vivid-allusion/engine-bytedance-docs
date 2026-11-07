---
title: "Switching Between Multiple Qualities and Lines"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-switching-between-multiple-qualities-and-lines"
---

This document describes how to configure multiple streaming lines and quality levels using the Web Player SDK (VePlayer). This feature is applicable to use cases where users may need to manually switch or automatically select the playback quality or CDN line, which helps improve playback performance under varying network conditions.

<span id="适用版本"></span>
## Applicable to

This document is applicable to **the latest version** of the Web Player SDK. For version information, please refer to [Player SDK for Web: Release notes](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-changelog_2). For past versions, please refer to [Legacy versions](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-web-1-x-versions).

<span id="448c8a62"></span>
## Prerequisites

Ensure that the SDK has been integrated into your project by following the instructions provided in [Integrating the Player SDK for Web](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-player-sdk-for-web_1).

<span id="98ee379c"></span>
## Configuration Examples

You can configure multiple streaming lines and/or video qualities using the `playlist` field. The defaultSource and defaultDefinition fields define the default streaming line and default video quality, respectively. After the player is successfully created, you can use the `switch` method to change the streaming line or video quality.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When using multiple sources or quality levels, the <code>url</code> field must not be used directly.</div>


<span id="2836c6fb"></span>
### Configuring Multiple Streaming Lines

To configure multiple streaming lines, define multiple `source` items in the `playlist` array and set the `defaultSource`. The following examples demonstrate how to implement this.


<Tabs>
<Tab zoneid="e6IWlMoSh9" title="From CDN">
<TabTitle>From CDN</TabTitle>

```JavaScript
VePlayer.createLivePlayer({ 
  height: 360, 
  defaultSource: 'lineOne', 
  playlist: [ 
    { 
      name: 'lineOne', 
      text: { 'zh-cn': '线路一', en: 'lineone' }, 
      definitions: ['https://pulldomain/appname/mystream_hd.m3u8'], 
    }, 
    { 
      name: 'lineTwo', 
      text: { 'zh-cn': '线路二', en: 'linetwo' }, 
      definitions: ['https://pulldomain/appname/mystream1_hd.m3u8'], 
    }, 
  ], 
  logger: { 
    appId: '5****8', 
  }, 
}).then(function (veplayer) { 
  // Switch to lineTwo
  veplayer.switch({ source: 'lineTwo' }); 
});
```



</Tab>
<Tab zoneid="GoeHLRubuZ" title="By NPM">
<TabTitle>By NPM</TabTitle>

```JavaScript
import { createLivePlayer, register } from '@byteplus/veplayer';
import { hlsjs } from '@byteplus/veplayer-plugin';
import '@byteplus/veplayer/style'; 
register([hlsjs]);
createLivePlayer({
  height: 360,
  defaultSource: 'lineOne',
  playlist: [
    {
      name: 'lineOne',
      text: { 'zh-cn': '线路一', en: 'lineone' },
      definitions: ['https://pulldomain/appname/mystream_hd.m3u8'],
    },
    {
      name: 'lineTwo',
      text: { 'zh-cn': '线路二', en: 'linetwo' },
      definitions: ['https://pulldomain/appname/mystream1_hd.m3u8'],
    },
  ],
  logger: {
    appId: '5****8',
  },
}).then(function (veplayer) {
  // Switch to lineTwo
  veplayer.switch({ source: 'lineTwo' });
});
```



</Tab>
</Tabs>


<span id="f9f7b6d4"></span>
### Configuring Multiple Video Qualities

To enable quality switching, configure multiple `definition` items within a single source. You can set `defaultDefinition` to specify the initial quality level.


<Tabs>
<Tab zoneid="tOxe1JbT3f" title="From CDN">
<TabTitle>From CDN</TabTitle>

```JavaScript
VePlayer.createLivePlayer({
  height: 360,
  defaultDefinition: 'ld',
  playlist: [
    {
      definitions: [
        {
          url: 'https://pulldomain/appname/mystream_hd.m3u8',
          definition: 'hd',
          text: { en: 'hd', 'zh-cn': '超清' },
        },
        {
          url: 'https://pulldomain/appname/mystream_sd.m3u8',
          definition: 'sd',
          text: { en: 'sd', 'zh-cn': '高清' },
        },
        {
          url: 'https://pulldomain/appname/mystream_ld.m3u8',
          definition: 'ld',
          text: { en: 'ld', 'zh-cn': '标清' },
        },
      ],
    },
  ],
  logger: {
    appId: '5****8',
  },
}).then(function (veplayer) {
  // Switch to high quality (HD)
  veplayer.switch({ definition: 'hd' });
});
```



</Tab>
<Tab zoneid="alpKE6ZAd8" title="By NPM">
<TabTitle>By NPM</TabTitle>

```JavaScript
import { createLivePlayer, register } from '@byteplus/veplayer';
import { hlsjs } from '@byteplus/veplayer-plugin';
import '@byteplus/veplayer/style'
register([hlsjs]);
createLivePlayer({
  height: 360,
  defaultDefinition: 'ld',
  playlist: [
    {
      definitions: [
        {
          url: 'https://pulldomain/appname/mystream_hd.m3u8',
          definition: 'hd',
          text: { en: 'hd', 'zh-cn': '超清' },
        },
        {
          url: 'https://pulldomain/appname/mystream_sd.m3u8',
          definition: 'sd',
          text: { en: 'sd', 'zh-cn': '高清' },
        },
        {
          url: 'https://pulldomain/appname/mystream_ld.m3u8',
          definition: 'ld',
          text: { en: 'ld', 'zh-cn': '标清' },
        },
      ],
    },
  ],
  logger: {
    appId: '5****8',
  },
}).then(function (veplayer) {
  // Switch to high quality (HD)
  veplayer.switch({ definition: 'hd' });
});
```



</Tab>
</Tabs>


<span id="ef16d960"></span>
### Configuring Both Multiple Lines and Bitrates

To support both line and quality switching, define multiple sources and include multiple definitions in each source. Set `defaultSource` and `defaultDefinition` to specify the defaults.


<Tabs>
<Tab zoneid="hpJ2wPChPM" title="From CDN">
<TabTitle>From CDN</TabTitle>

```JavaScript
VePlayer.createLivePlayer({
  height: 360,
  defaultDefinition: 'ld',
  defaultSource: 'lineOne',
  playlist: [
    {
      name: 'lineOne',
      text: { 'zh-cn': '线路一', en: 'lineone' },
      definitions: [
        {
          url: 'https://pulldomain/appname/mystream_hd.m3u8',
          definition: 'hd',
          text: { en: 'hd', 'zh-cn': '超清' },
        },
        {
          url: 'https://pulldomain/appname/mystream_ld.m3u8',
          definition: 'ld',
          text: { en: 'ld', 'zh-cn': '标清' },
        },
      ],
    },
    {
      name: 'lineTwo',
      text: { 'zh-cn': '线路二', en: 'linetwo' },
      definitions: [
        {
          url: 'https://pulldomain/appname/mystream1_hd.m3u8',
          definition: 'hd',
          text: { en: 'hd', 'zh-cn': '超清' },
        },
        {
          url: 'https://pulldomain/appname/mystream1_sd.m3u8',
          definition: 'sd',
          text: { en: 'sd', 'zh-cn': '高清' },
        },
        {
          url: 'https://pulldomain/appname/mystream1_ld.m3u8',
          definition: 'ld',
          text: { en: 'ld', 'zh-cn': '标清' },
        },
      ],
    },
  ],
  logger: {
    appId: '5****8',
  },
}).then(function (veplayer) {
  // Switch to lineTwo with HD definition
  veplayer.switch({ definition: 'hd', source: 'lineTwo' });
});
```



</Tab>
<Tab zoneid="wVMDrWMFJW" title="By NPM">
<TabTitle>By NPM</TabTitle>

```JavaScript
import { createLivePlayer, register } from '@byteplus/veplayer';
import { hlsjs } from '@byteplus/veplayer-plugin';
import '@byteplus/veplayer/style'
register([hlsjs]);

createLivePlayer({
  height: 360,
  defaultDefinition: 'ld',
  defaultSource: 'lineOne',
  playlist: [
    {
      name: 'lineOne',
      text: { 'zh-cn': '线路一', en: 'lineone' },
      definitions: [
        {
          url: 'https://pulldomain/appname/mystream_hd.m3u8',
          definition: 'hd',
          text: { en: 'hd', 'zh-cn': '超清' },
        },
        {
          url: 'https://pulldomain/appname/mystream_ld.m3u8',
          definition: 'ld',
          text: { en: 'ld', 'zh-cn': '标清' },
        },
      ],
    },
    {
      name: 'lineTwo',
      text: { 'zh-cn': '线路二', en: 'linetwo' },
      definitions: [
        {
          url: 'https://pulldomain/appname/mystream1_hd.m3u8',
          definition: 'hd',
          text: { en: 'hd', 'zh-cn': '超清' },
        },
        {
          url: 'https://pulldomain/appname/mystream1_sd.m3u8',
          definition: 'sd',
          text: { en: 'sd', 'zh-cn': '高清' },
        },
        {
          url: 'https://pulldomain/appname/mystream1_ld.m3u8',
          definition: 'ld',
          text: { en: 'ld', 'zh-cn': '标清' },
        },
      ],
    },
  ],
  logger: {
    appId: '5****8',
  },
}).then(function (veplayer) {
  // Switch to lineTwo with HD definition
  veplayer.switch({ definition: 'hd', source: 'lineTwo' });
});
```



</Tab>
</Tabs>
