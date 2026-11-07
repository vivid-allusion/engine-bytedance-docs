---
title: "DRM Streaming Support"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-drm-streaming-support"
---

This document describes how to use the Web Player SDK (VePlayer) to play DRM\-encrypted live streams. This feature is designed for scenarios that require content protection, including:


* Pay\-per\-view or subscription\-based content

* Licensed or restricted content distribution

* Prevention of unauthorized downloads or content tampering


<span id="适用版本"></span>
## Applicable to

This document is applicable to **the latest version** of the Web Player SDK. For version information, please refer to [Player SDK for Web: Release notes](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-changelog_2). For past versions, please refer to [Legacy versions](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-web-1-x-versions).

<span id="适用平台"></span>
## Supported Platforms

The Web Player SDK currently supports DRM\-encrypted stream playback on the following platforms:


* **Desktop:**  Safari browser

* **iOS:**  Safari and Chrome browsers


<span id="前提条件"></span>
## Prerequisites


* Ensure that the SDK has been integrated into your project by following the instructions provided in [Integrating the Player SDK for Web](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-player-sdk-for-web_1).

* Complete the required setup described in [Encrypting your live streams using DRM](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-ht0g9lqto0), including:

   * Obtaining an M3U8 URL for a DRM\-encrypted stream

   * Acquiring the FairPlay DRM license server URL

   * Acquiring the FairPlay certificate server URL


<span id="b0f8afb5"></span>
## Configuration Examples

You can play DRM\-encrypted streams using either a CDN\-based setup or an NPM package. The following examples show how to configure DRM parameters using both methods.


<Tabs>
<Tab zoneid="unZUume43i" title="From CDN">
<TabTitle>From CDN</TabTitle>

```JavaScript
VePlayer.createLivePlayer({
  url: 'https://xxx.m3u8',
  height: 360,
  drm: {
    fairplay: {
      getDrmConfig: async ({ url }) => {
        return {
          // URL of the FairPlay certificate service
          serverCertificatePath: 'https://xxx',
          // URL of the FairPlay license service
          serverProcessSPCPath: 'https://xxx',
        };
      },
    },
  },
}).then(function (veplayer) {
  veplayer.on('error', function (error) {
    // Error code 7100 indicates DRM license validation failed.
    // Please verify that the certificate and license URLs are correct.
    console.log(error.errorCode);
  });
});
```



</Tab>
<Tab zoneid="O73dy1QXZo" title="By NPM">
<TabTitle>By NPM</TabTitle>

```JavaScript
import { createLivePlayer, register } from '@byteplus/veplayer';
import { hls, drm } from '@byteplus/veplayer-plugin';
import '@byteplus/veplayer/style';

register([hls, drm]);

createLivePlayer({
  url: 'https://xxx.m3u8',
  height: 360,
  drm: {
    fairplay: {
      getDrmConfig: async ({ url }) => {
        return {
          // URL of the FairPlay certificate service
          serverCertificatePath: 'https://xxx',
          // URL of the FairPlay license service
          serverProcessSPCPath: 'https://xxx',
        };
      },
    },
  },
}).then(function (veplayer) {
  veplayer.on('error', function (error) {
    // Error code 7100 indicates DRM license validation failed.
    // Please verify that the certificate and license URLs are correct.
    console.log(error.errorCode);
  });
});
```



</Tab>
</Tabs>
