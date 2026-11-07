---
title: "使用自适应缓冲策略降低 RTM 流回放过程中的延迟和卡顿"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/adaptive-buffer-strategy-zh-CN"
---

为降低 RTM 流回放过程中的延迟和卡顿，可以启用自适应缓冲策略。该功能会根据每个客户端的网络状况动态调整抖动缓冲区，以实现回放流畅性与低延迟之间的最佳平衡。本文介绍如何通过 Web 端拉流 SDK（VePlayer）启用该策略。在网络状况良好的情况下，减少抖动缓冲区可以降低延迟。相反，在网络状况较差时，增加抖动缓冲区可以减少卡顿。该策略仅适用于 RTM 流。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Safari 浏览器不支持自适应缓冲策略。</div>


* <div data-tips="true" data-tips-type="warning">自适应缓冲策略仅适用于 Web 端拉流 SDK 2.10.0 及以上版本。</div>



<span id="45b0843b"></span>
## 前提条件


* 你已集成 Web 端拉流 SDK。更多信息，请参见 [集成 Web 端拉流 SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-player-sdk-for-web_1-zh-CN)。

* 请联系 [技术支持](https://console.byteplus.com/workorder/create)，并提供你的 Web 类型 SDK 应用的 app ID。关于如何创建 SDK 应用的更多信息，请参见 [创建 SDK 应用](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management#creating-an-sdk-application)。

* 你正在使用 RTM 协议拉流。


<span id="70d12649"></span>
## 配置方法

通过 CDN 或 NPM 集成方式启用自适应缓冲策略，具体如下：


<Tabs>
<Tab zoneid="lQ0d7J4Myn" title="CDN">
<TabTitle>CDN</TabTitle>

```JavaScript
        VePlayer.live.prepare({
            appId: 'APP_ID', // Replace APP_ID with the app ID from your Web-type SDK application.
            userId: 'USER_ID', // Replace USER_ID with the ID used to identify a single user.
            strategies: {
                rtmAdaptiveBuffer: true, // Set the value to true to enable the adaptive buffer strategy.
            },
        }).then(function(vestrategy){
            VePlayer.createLivePlayer({
                width: "100%",
                height: "100vh",
                logger: {
                    appId: 'APP_ID', // Replace APP_ID with the app ID from your Web-type SDK application.
                    userId: 'USER_ID', // Replace USER_ID with the ID used to identify a single user.
                },
                url: 'https://pull-demo.volcfcdnrd.com/live/st-4536521_webrtm.sdp'
            })
        })
```



</Tab>
<Tab zoneid="FwllanJl6c" title="NPM">
<TabTitle>NPM</TabTitle>

```JavaScript
import { createLivePlayer, register, live } from '@byteplus/veplayer';
import { rtm, strategy, strategyRtmAdaptiveBuffer } from '@byteplus/veplayer-plugin';
import '@byteplus/veplayer/style'

register([rtm, strategy, strategyRtmAdaptiveBuffer]); 

live.prepare({
    appId: 'APP_ID', // Replace APP_ID with the app ID from your Web-type SDK application.
    userId: 'USER_ID', // Replace USER_ID with the ID used to identify a single user.
    strategies: {
        rtmAdaptiveBuffer: true,  // Set the value to true to enable the adaptive buffer strategy.
    },
}).then(function(vestrategy){
    createLivePlayer({
        autoplay: { muted: false},
        id: videoPlayerId,
        width: "100%",
        height: "100vh",
        logger: {
            appId: 'APP_ID', // Replace APP_ID with the app ID from your Web-type SDK application.
            userId: 'USER_ID', // Replace USER_ID with the ID used to identify a single user.
        },
        url: 'https://pull-demo.volcfcdnrd.com/live/st-4536521_webrtm.sdp'
    })
})
```



</Tab>
</Tabs>
