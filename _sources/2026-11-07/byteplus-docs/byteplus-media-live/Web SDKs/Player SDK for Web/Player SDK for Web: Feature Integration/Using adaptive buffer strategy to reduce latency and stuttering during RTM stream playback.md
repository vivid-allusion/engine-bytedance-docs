---
title: "Using adaptive buffer strategy to reduce latency and stuttering during RTM stream playback"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/adaptive-buffer-strategy"
---

This topic describes how to enable the adaptive buffer strategy. The adaptive buffer strategy dynamically adjusts jitter buffers based on each client's network conditions, ensuring an optimal balance between latency and stuttering during RTM stream playback. Under good network conditions, decreasing jitter buffers can reduce latency. Conversely, under poor network conditions, increasing jitter buffers can reduce stuttering. The strategy only applies to RTM streams.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">The Safari browser does not support the adaptive buffer strategy.</div>


* <div data-tips="true" data-tips-type="warning">The adaptive buffer strategy only applies to the Player SDK for Web versions 2.10.0 and later.</div>



<span id="45b0843b"></span>
## Prerequisites


* You have integrated the Player SDK for Web. For more information, see [Integrating the Player SDK for Web](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-player-sdk-for-web_1).

* Contact [technical support](https://console.byteplus.com/workorder/create) to provide your app ID that you get after creating the Web\-type SDK application. For more information on how to create the SDK application, see [Creating an SDK application](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management#creating-an-sdk-application).

* You are pulling streams in RTM protocol.


<span id="70d12649"></span>
## Configuration method

Enable the adaptive buffer strategy using either CDN or NPM integration method as follows:


<Tabs>
<Tab zoneid="H2nqsN3spS" title="CDN">
<TabTitle>CDN</TabTitle>

```JavaScript
        VePlayer.live.prepare({
            appId: 'APP_ID', // Replace APP_ID with the app ID that you get after creating the Web-type SDK application.  
            userId: 'USER_ID', // Replace USER_ID with the ID used to identify a single user.
            strategies: {
                rtmAdaptiveBuffer: true, // Set the value to true to enable the adaptive buffer strategy.
            },
        }).then(function(vestrategy){
            VePlayer.createLivePlayer({
                width: "100%",
                height: "100vh",
                logger: {
                    appId: 'APP_ID', // Replace APP_ID with the app ID that you get after creating the Web-type SDK application.  
                    userId: 'USER_ID', // Replace USER_ID with the ID used to identify a single user.
                },
                url: 'https://pull-demo.volcfcdnrd.com/live/st-4536521_webrtm.sdp'
            })
        })
```



</Tab>
<Tab zoneid="XYXPMtOJ6t" title="NPM">
<TabTitle>NPM</TabTitle>

```JavaScript
import { createLivePlayer, register, live } from '@byteplus/veplayer';
import { rtm, strategy, strategyRtmAdaptiveBuffer } from '@byteplus/veplayer-plugin';
import '@byteplus/veplayer/style'

register([rtm, strategy, strategyRtmAdaptiveBuffer]); 

live.prepare({
    appId: 'APP_ID', // Replace APP_ID with the app ID that you get after creating the Web-type SDK application.  
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
            appId: 'APP_ID', // Replace APP_ID with the app ID that you get after creating the Web-type SDK application.
            userId: 'USER_ID', // Replace USER_ID with the ID used to identify a single user.
        },
        url: 'https://pull-demo.volcfcdnrd.com/live/st-4536521_webrtm.sdp'
    })
})
```



</Tab>
</Tabs>
