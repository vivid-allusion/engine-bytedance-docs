---
title: "集成 Web 端拉流 SDK"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-integrating-the-player-sdk-for-web_1-zh-CN"
---

要将视频播放器嵌入到网页中，可以将 Web 端拉流 SDK（也称为 VePlayer）集成到您的 Web 应用中。本文介绍如何集成 Web 端拉流 SDK。

<span id="e625f8f3"></span>
## 前提条件


* 请根据 SDK 版本完成以下操作。

   * 2.11.0 及以上版本（推荐）：创建一个 SDK 应用，并获取许可证文件、许可证 URL 和应用 ID。更多信息，请参见 [获取您的 SDK 许可证](https://docs.byteplus.com/docs/byteplus-media-live/managing_sdk_licenses-zh-CN)。

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">自 2.11.0 版本起，必须通过许可证管理拉流 SDK 及其增值服务的使用权限和时长。高级许可证包含更多功能，如 <a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-adaptive-bitrate-streaming-abr-zh-CN">码率自适应</a>、<a href="https://docs.byteplus.com/en/docs/byteplus-media-live/adaptive-buffer-strategy">自适应缓冲策略</a>、<a href="https://docs.byteplus.com/en/docs/byteplus-media-live/achieving_2-3s_live_stream_latency_with_low-latency_FLV_web">低延迟 FLV 拉流</a>、<a href="https://docs.byteplus.com/en/docs/byteplus-media-live/RTM-Streaming-Integration">RTM 流播放</a>，但需付费。有关不同许可证类型和计费情况的更多信息，请参见。      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">试用许可证仅用于项目测试，且不可续期。试用许可证过期后将导致认证失败，服务会被中断。在项目上线前，请升级为正式许可证。更多信息，请参见<a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management-zh-CN#777c7de7">将试用许可证升级为基础或高级许可证</a>。      </div>
      

   * 2.11.0 以下版本：只需创建一个 SDK 应用并获取应用 ID。无需许可证。更多信息，请参见 [获取您的 SDK 许可证](https://docs.byteplus.com/docs/byteplus-media-live/managing_sdk_licenses-zh-CN)。建议升级到最新版本，以获得更丰富的功能和更优质的服务。

* 要使用拉流 SDK 拉取 BytePlus MediaLive 分发的流，请完成以下前提条件：

   * 添加域名和 CNAME 记录。更多信息，请参见 [添加域名](https://docs.byteplus.com/docs/byteplus-media-live/docs-domain-zh-CN) 和 [添加 CNAME 记录](https://docs.byteplus.com/docs/byteplus-media-live/docs-adding-a-cname-record-zh-CN)。

   * [生成拉流地址](https://docs.byteplus.com/byteplus-media-live/docs/address-generator)。如需使用 HTTPS 拉流地址，需先添加 SSL 证书并完成 HTTPS 配置。更多信息，请参见 [管理 SSL 证书](https://docs.byteplus.com/docs/byteplus-media-live/docs-managing-certificates-zh-CN) 和 [HTTPS 配置](https://docs.byteplus.com/docs/byteplus-media-live/docs-https-zh-CN)。


<span id="ceef554f"></span>
## Step 1: 导入依赖

可通过以下任一方式导入 SDK：


<Tabs>
<Tab zoneid="nh5TfzzFOL" title="CDN">
<TabTitle>CDN</TabTitle>

要通过 CDN 导入拉流 SDK 的 CSS 和 JS 文件，请将以下代码添加到本地项目的`index.html`文件中：

```HTML
<link rel="stylesheet" href="https://sf-unpkg.bytepluscdn.com/obj/byteplusfe-sg/sdk/@byteplus/veplayer/2.11.2/umd/veplayer.production.css">

<script src="https://sf-unpkg.bytepluscdn.com/obj/byteplusfe-sg/sdk/@byteplus/veplayer/2.11.2/umd/veplayer.production.js"></script>
```



</Tab>
<Tab zoneid="z0KPSOz5oP" title="NPM">
<TabTitle>NPM</TabTitle>

1. 运行以下命令安装拉流 SDK。

   ```Plain
   npm install @byteplus/veplayer@next
   npm install @byteplus/veplayer-plugin@next
   ```
   

2. 将以下代码添加到本地项目的`index.html`文件中。

   ```Plain
   import { createLivePlayer, register } from '@byteplus/veplayer';
   import '@byteplus/veplayer/style';
   ```
   

3. 按需导入并注册插件。示例代码如下。

   ```JavaScript
   // To play HLS streams
   import { hlsjs } from '@byteplus/veplayer-plugin';
   register([hlsjs]);
   
   // To play FLV streams
   import { flv } from '@byteplus/veplayer-plugin';
   register([flv]);
   
   // To play RTM streams
   import { rtm } from '@byteplus/veplayer-plugin';
   register([rtm]);
   
   // To play multiple streams in different protocols
   import { flv, hlsjs, rtm } from '@byteplus/veplayer-plugin';
   register([rtm, flv, hlsjs]);
   ```
   

   为减小包体积，可以按路径导入单个插件。例如，将`import { hlsjs } from '@byteplus/veplayer-plugin';`替换为`import * as hlsjs from '@byteplus/veplayer-plugin/hlsjs';`以导入 hlsjs 插件。同样，您可以按需导入以下插件：`flv`、`rtm`、`abr`、`drm`、`timeshift`和`ad`。


</Tab>
</Tabs>


<span id="7d0334fc"></span>
## Step 2: 添加播放器容器

在需要展示播放器的页面添加播放器容器。例如，将如下代码添加到 `index.html`：

```html
<div id="veplayer"></div>
```


<span id="f1396aa0"></span>
## Step 3: 配置许可证

从 2.11.0 版本开始，必须配置许可证才能使用拉流 SDK。请按照步骤完成配置。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">2.11.0 之前的版本无需许可证，但建议升级到最新版本以获得更好的功能和服务。</div>


* <div data-tips="true" data-tips-type="warning">请确保嵌入播放器页面的域名与您的 SDK 应用配置的通配符域名一致。否则，许可证校验将失败。例如，如果您配置了<code>*. example.com</code>作为通配符域名，则页面的域名必须为一级子域名，如<code>a.example.com</code>。</div>



许可证校验在页面级别进行，因此即使在单页面多实例场景下，也只需设置一次。为优化回放体验并提升首帧加载速度，建议在初始化播放器前配置许可证。

您可以通过以下任一方式配置许可证。


<Tabs>
<Tab zoneid="No2ShXCZXq" title="设置许可证文件内容">
<TabTitle>设置许可证文件内容</TabTitle>

调用`setLicenseConfig`并传入许可证文件内容。


* `sign`：来自许可证文件的`Signature`，用于认证。

* `content`：来自许可证文件的`Content`，包含权限等级和版本信息。

* `mainUrl`（可选但推荐）：来自许可证文件的`MainUrl`，即许可证 URL。如设置该项，SDK 会在许可证升级或续期后自动更新到最新版本，无需手动更新。有关如何获取许可证 URL 的更多信息，请参见[Step 2: Get the license file](https://docs.byteplus.com/docs/byteplus-media-live/managing_sdk_licenses-zh-CN#8a4f3efc)。


示例代码如下。


* CDN

   ```JavaScript
   VePlayer.live.setLicenseConfig({
     license: {
        sign: "xxx",
        content: "xxx",
        mainUrl: "https://example.com/obj/license-byteplus/license.lic", 
    }
   })
   ```
   

* NPM

   ```JavaScript
   import { live } from '@byteplus/veplayer';
   live.setLicenseConfig({
     license: {
        sign: "xxx",
        content: "xxx",
        mainUrl: "https://example.com/obj/license-byteplus/license.lic", 
    }
   })
   ```
   


</Tab>
<Tab zoneid="InHQKHbcZt" title="设置许可证 URL">
<TabTitle>设置许可证 URL</TabTitle>

调用`setLicenseConfig`并传入许可证 URL。有关如何获取许可证 URL 的更多信息，请参见[Step 2: Get the license file](https://docs.byteplus.com/docs/byteplus-media-live/managing_sdk_licenses-zh-CN#8a4f3efc)。

SDK 会自动处理认证逻辑并启用许可证自动更新。示例代码如下。


* CDN

   ```JavaScript
   VePlayer.setLicenseConfig({
       // The license URL.SDK 会在许可证升级或续期后自动更新至最新的许可证版本，无需手动更新。
       license: "https://example.com/obj/license-byteplus/license.lic"
   }) 
   ```
   

* NPM

   ```JavaScript
   import { live } from '@byteplus/veplayer';
   live.setLicenseConfig({
       // The license URL.SDK 会在许可证升级或续期后自动更新至最新的许可证版本，无需手动更新。
       license: "https://example.com/obj/license-byteplus/license.lic"
   }) 
   ```
   


</Tab>
</Tabs>


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">如播放器初始化并正常播放视频且无任何许可证相关错误，则校验成功。</div>


<span id="f816d63b"></span>
## Step 4: 创建 VePlayer 实例并开启日志上报

通过如下代码创建 VePlayer 实例并开启日志上报。页面加载后，播放器自动开始播放。如需播放直播流，请将 `url` 设置为拉流地址。


<Tabs>
<Tab zoneid="kmHs5oQuUS" title="CDN">
<TabTitle>CDN</TabTitle>

```javascript
VePlayer.createLivePlayer({
  width: 640,
  height: 360,
  url: 'https://livepull.example.com/appname/streamname.flv',
  logger:{
    // 启用日志上报。已开启后，SDK 会将回放相关信息发送至 BytePlus MediaLive 服务器，用于故障排查和分析，帮助提升应用的稳定性和用户体验。
    appId: 'APP_ID', // 必填项。将 APP_ID 替换为 app ID，来自你 创建的 SDK 应用。
    userId: 'USER_ID', // Optional.将 USER_ID 替换为应用用户 ID。
    deviceId: 'DEVICE_ID', // Optional.将 DEVICE_ID 替换为用户的设备 ID。
  }
}).then(function(veplayer){
  console.log('VePlayer is successfully created. The VePlayer instance is:', veplayer)
}).catch(function(err){
  console.log('Creating VePlayer failed due to:', err)
});
```



</Tab>
<Tab zoneid="e9p7V9wCyn" title="NPM">
<TabTitle>NPM</TabTitle>

```javascript
createLivePlayer({
  width: 640,
  height: 360,
  url: 'https://livepull.example.com/appname/streamname.flv',
  logger:{
    // 启用日志上报。已开启后，SDK 会将回放相关信息发送至 BytePlus MediaLive 服务器，用于故障排查和分析，帮助提升应用的稳定性和用户体验。
    appId: 'APP_ID', // Required.将 APP_ID 替换为 app ID ，来自你创建的 SDK 应用。
    userId: 'USER_ID', // Optional.将 USER_ID 替换为应用用户 ID。
    deviceId: 'DEVICE_ID', // Optional.将 DEVICE_ID 替换为用户的设备 ID。
  }
}).then(function(veplayer){
  console.log('VePlayer is successfully created. The VePlayer instance is:', veplayer)
}).catch(function(err){
  console.log('Creating VePlayer failed due to:', err)
});
```



</Tab>
</Tabs>


直播流播放过程中如出现问题，请收集相关信息（如问题发生时间、用户 ID），并 [联系技术支持](https://console.byteplus.com/workorder/create)进行排查。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">从 2.5.1 版本开始，未配置<code>appId</code>会触发控制台错误，SDK 会使用默认<code>appId</code>上报日志。</div>


* <div data-tips="true" data-tips-type="tip">强烈建议同时传递<code>userId</code>和<code>deviceId</code>。这样有助于快速定位和排查回放问题。如果未传递<code>userId</code>和<code>deviceId</code>，SDK 会根据用户浏览器生成随机值并本地存储。</div>



<span id="fa2afbea"></span>
## 后续操作

拉流 SDK 提供多种功能，覆盖多种回放场景，包括自定义封面图、画中画、进度条缩略图预览，以及自动视频分辨率降级、RTM 流播放等高级功能。更多信息，请参见 [功能集成](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-web-feature-integration)。

VePlayer 还针对不同回放场景提供了丰富的功能。体验 [Web 播放器演示](https://demo.byteplus.com/common/veplayer/basic/example?tab=function-display)，探索其功能、效果及集成方式。
