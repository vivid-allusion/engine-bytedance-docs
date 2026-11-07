---
title: "播放 DRM 加密串流"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-drm-streaming-support-zh-TW"
---

為了防止未經授權存取你的直播內容，本主題說明如何使用 Player SDK for Web（VePlayer）進行 DRM 加密播放。本主題提供 CDN 與 NPM 兩種方式的配置範例，協助你在按次付費服務、授權內容分發、防止未經授權下載等場景中實現內容保護。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">建議你使用最新版的 Player SDK for Web。版本資訊請參見 <a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-changelog_2-zh-TW">Player SDK for Web：發行說明</a>。舊版資訊請參見 <a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-web-1-x-versions-zh-TW">Web 端播放器 SDK：1.x 版本</a>。</div>


<span id="适用平台"></span>
## 支援的平台

Web Player SDK 目前支援在以下平台播放 DRM 加密串流：


* **桌面端：** Safari 瀏覽器

* **iOS：** Safari 與 Chrome 瀏覽器


<span id="前提条件"></span>
## 先決條件


* 你已整合 Player SDK for Web。如需更多資訊，請參見 [整合 Web 端 Player SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-player-sdk-for-web_1-zh-TW)。

* 完成 [使用 DRM 加密你的直播串流](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-ht0g9lqto0) 中描述的必要設置，包括：

   * 取得 DRM 加密串流的 M3U8 URL

   * 取得 FairPlay DRM 授權伺服器 URL

   * 取得 FairPlay 憑證伺服器 URL


<span id="b0f8afb5"></span>
## 配置範例

你可以透過 CDN 部署或 NPM 套件播放 DRM 加密串流。以下範例展示如何用這兩種方式配置 DRM 參數。


<Tabs>
<Tab zoneid="Edv7eP5PFx" title="來自 CDN">
<TabTitle>來自 CDN</TabTitle>

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
// Verify that the certificate and license URLs are correct.
    console.log(error.errorCode);
  });
});
```



</Tab>
<Tab zoneid="oGk70cmcYq" title="透過 NPM">
<TabTitle>透過 NPM</TabTitle>

```JavaScript
import { createLivePlayer, register } from '@byteplus/veplayer';
import { hlsjs, drm } from '@byteplus/veplayer-plugin';
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
// Verify that the certificate and license URLs are correct.
    console.log(error.errorCode);
  });
});
```



</Tab>
</Tabs>
