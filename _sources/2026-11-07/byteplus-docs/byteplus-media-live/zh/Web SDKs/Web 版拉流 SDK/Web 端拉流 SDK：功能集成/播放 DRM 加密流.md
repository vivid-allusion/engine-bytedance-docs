---
title: "播放 DRM 加密流"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-drm-streaming-support-zh-CN"
---

为防止未经授权访问您的直播流内容，本文介绍如何使用 Web 端拉流 SDK（VePlayer）进行 DRM 加密回放。本文提供 CDN 和 NPM 两种方式的配置示例，帮助您实现内容保护，适用于按次付费服务、授权内容分发以及防止未经授权下载等场景。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">建议您使用最新版本的 Web 端拉流 SDK。版本信息，请参见 <a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-changelog_2-zh-CN">Web 拉流 SDK：版本说明</a>。历史版本，请参见 <a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-web-1-x-versions-zh-CN">Web 端拉流 SDK：1.x 版本</a>。</div>


<span id="适用平台"></span>
## 支持的平台

Web 端拉流 SDK 当前支持以下平台的 DRM 加密流回放：


* **桌面端：** Safari 浏览器

* **iOS：** Safari 和 Chrome 浏览器


<span id="前提条件"></span>
## 前提条件


* 您已集成 Web 端拉流 SDK。更多信息，请参见 [集成 Web 端拉流 SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-player-sdk-for-web_1-zh-CN)。

* 完成 [使用 DRM 加密您的直播流](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-ht0g9lqto0) 中描述的必要设置，包括：

   * 获取 DRM 加密流的 M3U8 URL

   * 获取 FairPlay DRM 许可证服务器 URL

   * 获取 FairPlay 证书服务器 URL


<span id="b0f8afb5"></span>
## 配置示例

您可以通过 CDN 或 NPM 包播放 DRM 加密流。以下示例展示了两种方式配置 DRM 参数的方法。


<Tabs>
<Tab zoneid="b2YcwQRL9f" title="通过 CDN">
<TabTitle>通过 CDN</TabTitle>

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
<Tab zoneid="mY1Gbl40e4" title="通过 NPM">
<TabTitle>通过 NPM</TabTitle>

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
