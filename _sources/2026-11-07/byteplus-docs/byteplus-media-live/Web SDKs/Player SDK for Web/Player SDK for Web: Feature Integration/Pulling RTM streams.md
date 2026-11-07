---
title: "Pulling RTM streams"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/RTM-Streaming-Integration"
---

To achieve ultra\-low latency streaming for interactive scenarios like co\-hosted sessions or real\-time quizzes, you can integrate RTM streaming using the Player SDK for Web (VePlayer). This topic provides detailed instructions and code examples for configuring RTM with automatic fallback to FLV or HLS, ensuring a stable playback experience across all devices and network conditions.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">We recommend that you use the latest version of the Player SDK for Web. For version information, see <a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-changelog_2">Player SDK for Web: Release notes</a>. For legacy versions, see <a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-web-1-x-versions">Player SDK for Web: 1.x versions</a>.</div>


<span id="自动降级机制"></span>
## Automatic fallback mechanism

RTM streaming requires high compatibility across device and network environments. To ensure smooth playback under all conditions, we strongly recommend configuring a fallback mechanism when using RTM streaming. All scenarios in this topic include fallback configurations.

The player automatically triggers the fallback mechanism and switches to a backup stream when:


* The browser or device environment does not support RTM protocol playback, or playback of RTM streams encoded with H.264.

* A decoding exception occurs during playback.


To understand how the player detects support for RTM and FLV playback, refer to [How to detect protocol compatibility](https://docs.byteplus.com/docs/byteplus-media-live/RTM-Streaming-Integration#%E5%A6%82%E4%BD%95%E6%A3%80%E6%B5%8B%E5%8D%8F%E8%AE%AE%E5%85%BC%E5%AE%B9%E6%80%A7%EF%BC%9F).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For RTM stream pulling failures caused by network exceptions, the player triggers automatic retries (3 by default) and does not fall back directly. You can customize the number of retries using the <code>retryCount</code> parameter.</div>


<span id="协议兼容性要求"></span>
## Protocol compatibility requirements

RTM playback has high requirements for the client environment. In some cases, playback may fail due to device or network limitations. To ensure a consistent playback experience, the player supports **automatic fallback** to other protocols (such as FLV or HLS) when RTM playback fails. Fallback support by environment is as follows:


|Client Environment |Supported Fallback Protocols |Audio Codec Requirements for Fallback Streams |
|---|---|---|
|PC / Android |FLV or HLS |AAC |
|iOS ≥ 17.1 |FLV or HLS ||
|iOS ≤ 17.0 |HLS ||


<span id="c10b609a"></span>
## Prerequisites


* You have integrated the Player SDK for Web. For more information, see [Integrating the Player SDK for Web](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-player-sdk-for-web_1).

* Get the RTM pull stream address in one of the following ways. The address can be either a source stream address or a transcoded stream address.

   * **For debugging**: Use the [Address generator](https://console.byteplus.com/live/main/locationGenerate) to get the **RTM Web SDK playback address**. For more information, see [Generating stream addresses](https://docs.byteplus.com/docs/byteplus-media-live/docs-address-generator).

   * **For production**: Call [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) or use the [server-side SDK](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-server-sdk) to dynamically generate the RTM pull stream address. Make sure the value of `Protocol` is `udp_websdk`.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">If you cannot get the RTM pull stream address, contact <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980">technical support</a>.</div>


* <div data-tips="true" data-tips-type="warning">The RTM pull stream address supports automatic transcoding, including B\-frame removal and AAC\-to\-Opus audio conversion. For more information, see <a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-generating-live-stream-addresses">Generating live\-stream addresses</a>.</div>



<span id="ab524812"></span>
## Configuration examples

The following examples show how to configure RTM streaming in both single\-source and multi\-definition/multi\-line scenarios.


* **Single\-source streaming**: Suitable for simple live scenarios with stable network conditions and no need to switch between definitions or lines.

* **Multi\-definition or multi\-line streaming**: Suitable for scenarios where switching definitions or lines is needed based on network or device conditions to ensure a smoother playback experience.


<span id="场景一：单地址拉流"></span>
### Scenario 1: Single\-source streaming

In this case, you can configure **automatic fallback on RTM failure**, **conditional fallback based on error type**, and **custom fallback order**. The following sections provide configuration examples.


<Tabs>
<Tab zoneid="K7gCCa1VKY" title="Automatic fallback on RTM failure">
<TabTitle>Automatic fallback on RTM failure</TabTitle>

When RTM playback fails, the player can automatically switch to other protocols. The following examples show different ways to configure this fallback mechanism.


* **From CDN**

   ```JavaScript
   VePlayer.createLivePlayer({
       height: 360,
       playlist: [
         {
           // The RTM stream uses the RTM address for Player SDK for Web. This address supports automatic transcoding, while the fallback stream uses HLS or FLV addresses.
           definitions: [
             'https://pull-demo.example.com/live/st-4536521_autortm.sdp',
             'https://pull-demo.example.com/live/st-4536521.flv',
             'https://pull-demo.example.com/live/st-4536521.m3u8',
           ],
         },
       ],
       fallback: {
         // 1. Fallback to FLV if RTM is not supported or fails
         fallbackOrder: ['rtm', 'flv'],
         // 2. Fallback to HLS if RTM is not supported or fails
         // fallbackOrder: ['rtm', 'hls'],
         // 3. Fallback to FLV, then to HLS
         // fallbackOrder: ['rtm', 'flv', 'hls'],
       },
   }).then(function(veplayer) {
       veplayer.on(VePlayer.live.Events.FALLBACK_ERROR, function(){
           // Triggered when all fallback attempts have failed
       });
   })
   ```
   

* **By NPM**

   ```JavaScript
   import { createLivePlayer, register, live } from '@byteplus/veplayer';
   import { rtm, flv, hlsjs } from '@byteplus/veplayer-plugin';
   import '@byteplus/veplayer/style'
   register([rtm, flv, hlsjs]);
    
   createLivePlayer({
       height: 360,
       playlist: [
         {
           // The RTM stream uses the RTM address for Player SDK for Web. This address supports automatic transcoding, while the fallback stream uses HLS or FLV addresses.
           definitions: [
             'https://pull-demo.example.com/live/st-4536521_autortm.sdp',
             'https://pull-demo.example.com/live/st-4536521.flv',
             'https://pull-demo.example.com/live/st-4536521.m3u8',
           ],
         },
       ],
       fallback: {
          // 1. Fallback to FLV if RTM is not supported or fails
         fallbackOrder: ['rtm', 'flv'],
         // 2. Fallback to HLS if RTM is not supported or fails
         // fallbackOrder: ['rtm', 'hls'],
         // 3. Fallback to FLV, then to HLS
         // fallbackOrder: ['rtm', 'flv', 'hls'],
       },
   }).then(function(veplayer) {
       veplayer.on(live.Events.FALLBACK_ERROR, function(){
           // Triggered when all fallback attempts have failed
       });
   })
   ```
   


</Tab>
<Tab zoneid="iazGdczxwV" title="Conditional fallback based on error type">
<TabTitle>Conditional fallback based on error type</TabTitle>

You can configure the player to skip fallback for specific error codes. The following example shows how to skip fallback when the error code is 2104 (stream not found).


* **From CDN**

   ```JavaScript
   VePlayer.createLivePlayer({
       height: 360,
       playlist: [
         {
           definitions: [
             'https://pull-demo.example.com/live/st-4536521_autortm.sdp',
             'https://pull-demo.example.com/live/st-4536521.m3u8',
             'https://pull-demo.example.com/live/st-4536521.flv',
           ],
         },
       ],
       fallback: {
         fallbackOrder: ['rtm', 'flv', 'hls'],
         fallbackStrategy: {
           rtm: {
             Error: {
               // Do not fall back if the error code is 2104
               excludeList: [2104],
             },
           },
         },
       },
       rtm: {
           // Increase loadTimeout if 2104 error is not triggered
           loadTimeout: 15000,
       },
   }).then(function(veplayer) {
       veplayer.on(VePlayer.live.Events.FALLBACK_ERROR, function(){
           // All fallback attempts failed
       });
   })        
   ```
   

* **By NPM**

   ```JavaScript
   import { createLivePlayer, register, live } from '@byteplus/veplayer';
   import { rtm, flv, hlsjs } from '@byteplus/veplayer-plugin';
   import '@byteplus/veplayer/style'
   register([rtm, flv, hlsjs]);
    
   createLivePlayer({
       height: 360,
       playlist: [
         {
           definitions: [
             'https://pull-demo.example.com/live/st-4536521_autortm.sdp',
             'https://pull-demo.example.com/live/st-4536521.flv',
             'https://pull-demo.example.com/live/st-4536521.m3u8',
           ],
         },
       ],
       fallback: {
         fallbackOrder: ['rtm', 'flv', 'hls'],
         fallbackStrategy: {
           rtm: {
             Error: {
               // Do not fall back if the error code is 2104
               excludeList: [2104],
             },
           },
         },
       },
       rtm: {
           // Increase loadTimeout if 2104 error is not triggered
           loadTimeout: 15000,
       },
   }).then(function(veplayer) {
       veplayer.on(live.Events.FALLBACK_ERROR, function(){
           // All fallback attempts failed
       });
   })        
   ```
   


</Tab>
<Tab zoneid="gDuBQUJEwJ" title="Custom fallback order">
<TabTitle>Custom fallback order</TabTitle>

By default, the player attempts playback in the order of RTM, FLV, and then HLS. To customize this behavior, you can define a fallback sequence. In the following example, FLV takes priority, followed by RTM and HLS. The player will try each protocol in order until one succeeds or all attempts fail.


* **From CDN**

   ```JavaScript
   VePlayer.createLivePlayer({
       height: 360,
       playlist: [
         {
           definitions: [
             'https://pull-demo.example.com/live/st-4536521_autortm.sdp',
             'https://pull-demo.example.com/live/st-4536521.m3u8',
             'https://pull-demo.example.com/live/st-4536521.flv',
           ],
         },
       ],
       fallback: {
         // Customize fallback order
         fallbackOrder: ['flv', 'rtm', 'hls'],
       },
   }).then(function(veplayer) {
       veplayer.on(VePlayer.live.Events.FALLBACK_ERROR, function(){
           // Playback failed after all protocols have been attempted
       });
   })        
   ```
   

* **By NPM**

   ```JavaScript
   import { createLivePlayer, register, live } from '@byteplus/veplayer';
   import { rtm, flv, hlsjs } from '@byteplus/veplayer-plugin';
   import '@byteplus/veplayer/style'
   register([rtm, flv, hlsjs]);
    
   createLivePlayer({
       height: 360,
       playlist: [
         {
           definitions: [
             'https://pull-demo.example.com/live/st-4536521_autortm.sdp',
             'https://pull-demo.example.com/live/st-4536521.flv',
             'https://pull-demo.example.com/live/st-4536521.m3u8',
           ],
         },
       ],
       fallback: {
         // Customize fallback order
         fallbackOrder: ['flv', 'rtm', 'hls'],
       },
   }).then(function(veplayer) {
       veplayer.on(live.Events.FALLBACK_ERROR, function(){
           // Playback failed after all protocols have been attempted
       });
   })        
   ```
   


</Tab>
</Tabs>


<span id="场景二：多清晰度或多线路拉流"></span>
### Scenario 2: Multi\-definition or multi\-line streaming

In more complex live streaming scenarios, you may want to provide multiple definitions (quality levels) or lines (URLs from different CDN nodes). You can specify the protocol and fallback behavior for each source. The following is an example configuration:


<Tabs>
<Tab zoneid="QMdjNOdloz" title="Conditional fallback for RTM failure by error code">
<TabTitle>Conditional fallback for RTM failure by error code</TabTitle>

In multi\-line streaming scenarios, when RTM playback fails, you can define fallback strategies based on specific error codes to achieve more flexible and stable playback.


* **From CDN**

   ```JavaScript
   VePlayer.createLivePlayer({
       height: 360,
       playlist: [
         {
           name: 'lineOne',
           text: 'lineOne',
           definitions: [
             {
               url: 'https://pull-demo.example.com/live/st-4536521_autortm.sdp',
               definition: 'uhd',
               text: 'uhd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536521_hd_autortm.sdp',
               definition: 'hd',
               text: 'hd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536521.m3u8',
               definition: 'uhd',
               text: 'uhd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536521_hd.m3u8',
               definition: 'hd',
               text: 'hd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536521.flv',
               definition: 'uhd',
               text: 'uhd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536521_hd.flv',
               definition: 'hd',
               text: 'hd',
             },
           ],
         },
         {
           name: 'lineTwo',
           text: 'lineTwo',
           definitions: [
             {
               url: 'https://pull-demo.example.com/live/st-4536523_autortm.sdp',
               definition: 'uhd',
               text: 'uhd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536523_hd_autortm.sdp',
               definition: 'hd',
               text: 'hd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536523.m3u8',
               definition: 'uhd',
               text: 'uhd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536523_hd.m3u8',
               definition: 'hd',
               text: 'hd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536523.flv',
               definition: 'uhd',
               text: 'uhd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536523_hd.flv',
               definition: 'hd',
               text: 'hd',
             },
           ],
         },
       ],
       fallback: {
         // Set fallback order: fallback from RTM to FLV, then to HLS
         fallbackOrder: ['rtm', 'flv', 'hls'],
         // Customize fallback strategy: do not fallback if error code is 2104 (stream offline)
         fallbackStrategy: {
           rtm: {
             Error: {
               excludeList: [2104],
             },
           },
         },
       },
   }).then(function(veplayer) {
       veplayer.on(VePlayer.live.Events.FALLBACK_ERROR, function(){
           // Playback failed after all protocols have been attempted
       });
   })
   ```
   

* **By NPM**

   ```JavaScript
   import { createLivePlayer, register, live } from '@byteplus/veplayer';
   import { rtm, flv, hlsjs } from '@byteplus/veplayer-plugin';
   import '@byteplus/veplayer/style'
   register([rtm, flv, hlsjs]);
    
   createLivePlayer({
       height: 360,
       playlist: [
         {
           name: 'lineOne',
           text: 'lineOne',
           definitions: [
             {
               url: 'https://pull-demo.example.com/live/st-4536521_autortm.sdp',
               definition: 'uhd',
               text: 'uhd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536521_hd_autortm.sdp',
               definition: 'hd',
               text: 'hd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536521.m3u8',
               definition: 'uhd',
               text: 'uhd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536521_hd.m3u8',
               definition: 'hd',
               text: 'hd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536521.flv',
               definition: 'uhd',
               text: 'uhd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536521_hd.flv',
               definition: 'hd',
               text: 'hd',
             },
           ],
         },
         {
           name: 'lineTwo',
           text: 'lineTwo',
           definitions: [
             {
               url: 'https://pull-demo.example.com/live/st-4536523_autortm.sdp',
               definition: 'uhd',
               text: 'uhd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536523_hd_autortm.sdp',
               definition: 'hd',
               text: 'hd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536523.m3u8',
               definition: 'uhd',
               text: 'uhd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536523_hd.m3u8',
               definition: 'hd',
               text: 'hd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536523.flv',
               definition: 'uhd',
               text: 'uhd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536523_hd.flv',
               definition: 'hd',
               text: 'hd',
             },
           ],
         },
       ],
       fallback: {
         // Set the fallback priority. If RTM fails, it falls back to FLV. If FLV also fails, it falls back to HLS.
         fallbackOrder: ['rtm', 'flv', 'hls'],
         // Customize fallback strategy: for example, prevent fallback on specific error codes such as "stream offline" (error code 2104)
         fallbackStrategy: {
           rtm: {
             Error: {
               excludeList: [2104],
             },
           },
         },
       },
   }).then(function(veplayer) {
       veplayer.on(live.Events.FALLBACK_ERROR, function(){
           // All protocol fallback attempts have failed
       });
   })            
   ```
   


</Tab>
<Tab zoneid="SsWIC3oDd5" title="Customize fallback priority">
<TabTitle>Customize fallback priority</TabTitle>

By default, the player first tries RTM, then falls back to FLV or HLS. If you need more flexible control, you can configure a custom fallback order. In the example below, FLV is given the highest priority, followed by RTM, and finally HLS. The player will try each protocol in order until playback succeeds or all attempts fail.


* **From CDN**

   ```JavaScript
   VePlayer.createLivePlayer({
       height: 360,
       playlist: [
         {
           name: 'lineOne',
           text: 'lineOne',
           definitions: [
             {
               url: 'https://pull-demo.example.com/live/st-4536521_autortm.sdp',
               definition: 'uhd',
               text: 'uhd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536521_hd_autortm.sdp',
               definition: 'hd',
               text: 'hd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536521.m3u8',
               definition: 'uhd',
               text: 'uhd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536521_hd.m3u8',
               definition: 'hd',
               text: 'hd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536521.flv',
               definition: 'uhd',
               text: 'uhd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536521_hd.flv',
               definition: 'hd',
               text: 'hd',
             },
           ],
         },
         {
           name: 'lineTwo',
           text: 'lineTwo',
           definitions: [
             {
               url: 'https://pull-demo.example.com/live/st-4536523_autortm.sdp',
               definition: 'uhd',
               text: 'uhd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536523_hd_autortm.sdp',
               definition: 'hd',
               text: 'hd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536523.m3u8',
               definition: 'uhd',
               text: 'uhd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536523_hd.m3u8',
               definition: 'hd',
               text: 'hd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536523.flv',
               definition: 'uhd',
               text: 'uhd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536523_hd.flv',
               definition: 'hd',
               text: 'hd',
             },
           ],
         },
       ],
       fallback: {
         // Custom fallback order
         fallbackOrder: ['flv', 'rtm', 'hls'],
       },
   }).then(function(veplayer) {
       veplayer.on(VePlayer.live.Events.FALLBACK_ERROR, function(){
           // All protocol fallback attempts have failed
       });
   })     
   ```
   

* **By NPM**

   ```JavaScript
   import { createLivePlayer, register, live } from '@byteplus/veplayer';
   import { rtm, flv, hlsjs } from '@byteplus/veplayer-plugin';
   import '@byteplus/veplayer/style'
   register([rtm, flv, hlsjs]);
    
   createLivePlayer({
       height: 360,
       playlist: [
         {
           name: 'lineOne',
           text: 'lineOne',
           definitions: [
             {
               url: 'https://pull-demo.example.com/live/st-4536521_autortm.sdp',
               definition: 'uhd',
               text: 'uhd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536521_hd_autortm.sdp',
               definition: 'hd',
               text: 'hd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536521.m3u8',
               definition: 'uhd',
               text: 'uhd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536521_hd.m3u8',
               definition: 'hd',
               text: 'hd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536521.flv',
               definition: 'uhd',
               text: 'uhd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536521_hd.flv',
               definition: 'hd',
               text: 'hd',
             },
           ],
         },
         {
           name: 'lineTwo',
           text: 'lineTwo',
           definitions: [
             {
               url: 'https://pull-demo.example.com/live/st-4536523_autortm.sdp',
               definition: 'uhd',
               text: 'uhd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536523_hd_autortm.sdp',
               definition: 'hd',
               text: 'hd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536523.m3u8',
               definition: 'uhd',
               text: 'uhd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536523_hd.m3u8',
               definition: 'hd',
               text: 'hd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536523.flv',
               definition: 'uhd',
               text: 'uhd',
             },
             {
               url: 'https://pull-demo.example.com/live/st-4536523_hd.flv',
               definition: 'hd',
               text: 'hd',
             },
           ],
         },
       ],
       fallback: {
         // Custom fallback order
         fallbackOrder: ['flv', 'rtm', 'hls'],
       },
   }).then(function(veplayer) {
       veplayer.on(live.Events.FALLBACK_ERROR, function(){
           // All protocol fallback attempts have failed
       });
   })   
   ```
   


</Tab>
</Tabs>


<span id="常见问题"></span>
## FAQ

<span id="如何检测协议兼容性？"></span>
### How to detect protocol compatibility

When initializing the playback source, VePlayer automatically detects if the browser supports the RTM or FLV protocols to determine whether to trigger a fallback.


* The logic for determining RTM playback support is as follows:

   * `isRTMSupported()`: Returns `true` if the browser supports RTM playback.

   * `isRTMSupportCodec()`: Returns `true` if the browser supports the audio and video codecs required for RTM.

   * Only if both return `true` will VePlayer attempt to pull the RTM stream; otherwise, fallback will be triggered.

* The logic for determining FLV playback support is as follows:

   `isFLVSupported()`: Returns `true` if the browser can play FLV streams using Media Source Extensions (MSE).
