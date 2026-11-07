---
title: "拉取 RTM 流"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/RTM-Streaming-Integration-zh-CN"
---

为实现如连麦或实时答题等互动场景下的超低延迟流媒体播放，可通过拉流 SDK for Web（VePlayer）集成 RTM 流。本文档提供了配置 RTM 及自动回退至 FLV 或 HLS 的详细说明和代码示例，确保在所有设备和网络类型下都能获得稳定的回放体验。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">建议您使用 Web 端最新版本的拉流 SDK。关于版本信息，请参见<a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-changelog_2-zh-CN">Web 拉流 SDK：版本说明</a>。关于历史版本，请参见<a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-web-1-x-versions-zh-CN">Web 端拉流 SDK：1.x 版本</a>。</div>


<span id="自动降级机制"></span>
## 自动回退机制

RTM 流对设备和网络类型环境的兼容性要求较高。为确保在各种条件下流畅回放，强烈建议在使用 RTM 流时配置回退机制。本文档中的所有场景均包含回退配置。

播放器会在以下情况下自动触发回退机制并切换至备流：


* 浏览器或设备环境不支持 RTM 协议回放，或不支持播放采用 H.264 编码的 RTM 流。

* 回放过程中发生解码异常。


关于播放器如何检测 RTM 和 FLV 回放支持情况，参见[如何检测协议兼容性](https://docs.byteplus.com/docs/byteplus-media-live/RTM-Streaming-Integration-zh-CN#%E5%A6%82%E4%BD%95%E6%A3%80%E6%B5%8B%E5%8D%8F%E8%AE%AE%E5%85%BC%E5%AE%B9%E6%80%A7%EF%BC%9F)。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">对于因网络异常导致的 RTM 拉流失败，播放器会自动重试（默认 3 次），不会直接回退。您可通过<code>retryCount</code>参数自定义重试次数。</div>


<span id="协议兼容性要求"></span>
## 协议兼容性要求

RTM 回放对客户端环境要求较高。在某些情况下，可能因设备或网络类型限制导致回放失败。为确保一致的回放体验，播放器支持在 RTM 回放失败时**自动回退**到其他协议（如 FLV 或 HLS）。各环境下的回退支持如下：


|客户端环境 |支持的回退协议 |回退流的音频编解码要求 |
|---|---|---|
|PC / Android |FLV 或 HLS |AAC |
|iOS ≥ 17.1 |FLV 或 HLS ||
|iOS ≤ 17.0 |HLS ||


<span id="c10b609a"></span>
## 前提条件


* 你已集成拉流 SDK for Web。更多信息，参见[集成 Web 端拉流 SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-player-sdk-for-web_1-zh-CN)。

* 可通过以下任一方式获取 RTM 拉流地址。该地址可以是源流地址或转码流地址。

   * **调试用**：使用[地址生成器](https://console.byteplus.com/live/main/locationGenerate)获取**RTM Web SDK 回放地址**。更多信息，参见[生成流地址](https://docs.byteplus.com/docs/byteplus-media-live/docs-address-generator)。

   * **生产环境**：调用[GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023)或使用[服务端 SDK](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-server-sdk)动态生成 RTM 拉流地址。确保`Protocol`的值为`udp_websdk`。


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">若无法获取 RTM 拉流地址，请联系<a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980">技术支持</a>。</div>


* <div data-tips="true" data-tips-type="warning">RTM 拉流地址支持自动转码，包括 B帧移除和 AAC 转 Opus。更多信息，请参见<a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-generating-live-stream-addresses-zh-CN">生成直播流地址</a>。</div>



<span id="ab524812"></span>
## 配置示例

以下示例展示了在单路源和多清晰度/多线路场景下如何配置 RTM 流。


* **单路源流**：适用于网络类型稳定且无需切换清晰度或线路的简单直播场景。

* **多清晰度或多线路流**：适用于需根据网络类型或设备条件切换清晰度或线路，以确保更流畅回放体验的场景。


<span id="场景一：单地址拉流"></span>
### 场景 1：单路源流

在此场景下，可配置**RTM 故障自动回退**、**基于错误类型的条件回退**和**自定义回退顺序**。以下章节提供配置示例。


<Tabs>
<Tab zoneid="ariitRWseR" title="RTM 失败自动回退">
<TabTitle>RTM 失败自动回退</TabTitle>

RTM 回放失败时，播放器可自动切换至其他协议。以下示例展示了配置回退机制的不同方式。


* **通过 CDN**

   ```JavaScript
   VePlayer.createLivePlayer({
       height: 360,
       playlist: [
         {
           // The RTM stream uses the RTM address for Player SDK for Web.该地址支持自动转码，回退流则使用 HLS 或 FLV 地址。
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
   

* **通过 NPM**

   ```JavaScript
   import { createLivePlayer, register, live } from '@byteplus/veplayer';
   import { rtm, flv, hlsjs } from '@byteplus/veplayer-plugin';
   import '@byteplus/veplayer/style'
   register([rtm, flv, hlsjs]);
    
   createLivePlayer({
       height: 360,
       playlist: [
         {
           // The RTM stream uses the RTM address for Player SDK for Web.该地址支持自动转码，回退流则使用 HLS 或 FLV 地址。
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
<Tab zoneid="HL0ppHfhrk" title="基于错误类型的条件回退">
<TabTitle>基于错误类型的条件回退</TabTitle>

您可配置播放器针对特定错误码跳过回退。以下示例展示当错误码为 2104（流未找到）时跳过回退的方式。


* **通过 CDN**

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
   

* **通过 NPM**

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
<Tab zoneid="dHgzH61S4O" title="自定义回退顺序">
<TabTitle>自定义回退顺序</TabTitle>

默认情况下，播放器按 RTM、FLV、HLS 的顺序尝试回放。如需自定义该行为，可定义回退顺序。在以下示例中，FLV 优先，其次为 RTM 和 HLS。播放器将按顺序尝试每种协议，直至某一协议成功或全部失败。


* **通过 CDN**

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
   

* **通过 NPM**

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
### 场景 2：多清晰度或多线路流

在更复杂的直播场景中，你可能需要提供多种清晰度（画质等级）或多条线路（不同 CDN 节点的 URL）。你可以为每个源指定协议及回退行为。以下为配置示例：


<Tabs>
<Tab zoneid="i2qXNFJvQ9" title="按错误码进行 RTM 失败条件回退">
<TabTitle>按错误码进行 RTM 失败条件回退</TabTitle>

在多线路拉流场景下，RTM 回放失败时，您可基于特定错误码定义回退策略，实现更灵活、稳定的回放。


* **通过 CDN**

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
   

* **通过 NPM**

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
         // Set the fallback priority.如果 RTM 失败，则回退到 FLV。如果 FLV 也失败，则回退到 HLS。
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
<Tab zoneid="tMWtnl9RQx" title="自定义回退优先级">
<TabTitle>自定义回退优先级</TabTitle>

默认情况下，播放器先尝试 RTM，随后回退至 FLV 或 HLS。如需更灵活的控制，可配置自定义回退顺序。在下方示例中，FLV 优先，其次为 RTM，最后为 HLS。播放器将按顺序尝试每种协议，直至回放成功或全部失败。


* **通过 CDN**

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
   

* **通过 NPM**

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
## 常见问题

<span id="如何检测协议兼容性？"></span>
### 如何检测协议兼容性

初始化回放源时，VePlayer 会自动检测浏览器是否支持 RTM 或 FLV 协议，以决定是否触发回退。


* 判断 RTM 回放支持的逻辑如下：

   * `isRTMSupported()`：若浏览器支持 RTM 回放，则返回`true`。

   * `isRTMSupportCodec()`：若浏览器支持 RTM 所需的音视频编码格式，则返回`true`。

   * 仅当两者均返回`true`时，VePlayer 才会尝试拉取 RTM 流；否则将触发回退机制。

* 判断 FLV 回放支持的逻辑如下：

   `isFLVSupported()`：如果浏览器可通过 Media Source Extensions (MSE) 播放 FLV 流，则返回`true`。
