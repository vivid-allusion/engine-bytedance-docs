---
title: "使用自適應緩衝策略降低 RTM 串流播放時的延遲與卡頓"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/adaptive-buffer-strategy-zh-TW"
---

為了降低 RTM 串流播放時的延遲與卡頓，您可以啟用自適應緩衝策略。此功能會根據每個客戶端的網路狀況動態調整抖動緩衝區，以在播放流暢度與低延遲之間取得最佳平衡。本主題將說明如何使用 Player SDK for Web（VePlayer）啟用此策略。在網路狀況良好的情況下，減少抖動緩衝區可降低延遲。相反地，在網路狀況較差時，增加抖動緩衝區可減少卡頓。此策略僅適用於 RTM 串流。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Safari 瀏覽器不支援自適應緩衝策略。</div>


* <div data-tips="true" data-tips-type="warning">自適應緩衝策略僅適用於 Player SDK for Web 2.10.0 及以上版本。</div>



<span id="45b0843b"></span>
## 先決條件


* 您已整合 Player SDK for Web。如需更多資訊，請參閱 [整合 Web 端 Player SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-player-sdk-for-web_1-zh-TW)。

* 請聯絡 [技術支援](https://console.byteplus.com/workorder/create)，並提供您的 Web 類型 SDK 應用程式的 app ID。如需建立 SDK 應用程式的詳細資訊，請參閱 [建立 SDK 應用程式](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management#creating-an-sdk-application)。

* 您正在使用 RTM 協議拉取串流。


<span id="70d12649"></span>
## 配置方法

您可以透過 CDN 或 NPM 整合方式啟用自適應緩衝策略，方法如下：


<Tabs>
<Tab zoneid="ZcWI5kW5F6" title="CDN">
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
<Tab zoneid="lFzuP0fB8B" title="NPM">
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
