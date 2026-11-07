---
title: "集成 Web 观播 SDK"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-integrating-the-viewer-sdk-for-web-zh-CN"
---

Web 观播 SDK 使您的 Web 应用在 PC 或移动平台上具备互动功能，例如观看直播流、发送评论以及参与抽奖。本指南提供集成 SDK 的分步说明，并详细介绍所需的参数、事件和 API，帮助您快速上手。

<span id="Prerequisite"></span>
## 前提条件

由于 Web 观播 SDK 的 API 不支持跨域调用，请联系 BytePlus Live 技术支持，将您的域名添加至 BytePlus Live 的白名单。

<span id="Demo"></span>
## 演示

BytePlus Live 为 PC 和移动平台均提供演示 playground。您可以在下方查看效果，并访问 [BytePlus Live aPaaS Solution Web SDK Demo](https://live.byteplus.com/demo/sdk/index.html) 进行在线调试和实时预告。


<Tabs>
<Tab zoneid="or7KpS8Wg0" title="PC 效果">
<TabTitle>PC 效果</TabTitle>

在 PC 演示 playground 中，点击 **View Code** 可编辑代码并预告结果。

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9d6e24c8579c455c9d15cdd99e5a2b63~tplv-goo7wpa0wc-image.image) </span>


</Tab>
<Tab zoneid="zSxzQNQwUc" title="移动端效果">
<TabTitle>移动端效果</TabTitle>

在移动端的演示区中，你可以直接编辑右侧的代码以查看结果。

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/94c477739a434b97aa40f44ffa4da243~tplv-goo7wpa0wc-image.image) </span>


</Tab>
</Tabs>


<span id="Features"></span>
## 功能

有关 Web SDK 功能列表，请参见 *Web 观播 SDK* 在 [SaaS 与 aPaaS 功能对比](https://docs.byteplus.com/docs/byteplus-livesaas/docs-feature-comparison-between-saas-and-apaas-zh-CN) 文档表格中的对应列。

<span id="855885cc"></span>
## 集成方式

完成以下步骤，将 Web 观播 SDK 集成到您的 Web 应用中。

<span id="7f20b494"></span>
### Step 1: 导入 CSS 和 JS 资源

根据您的平台和功能需求选择合适的集成方式，然后使用 `link` 和 `script` 标签导入 CSS 和 JS 资源。

<span id="80ac0262"></span>
#### **PC 集成资源**

要将 SDK 集成到基于 PC 的 Web 应用中，请选择下方描述的资源之一。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">对于平板设备，建议集成 PC Web SDK，以获得更好的视觉体验。</div>


* <div data-tips="true" data-tips-type="tip">直接修改 URL 中的版本号即可更新版本。请确保为每个平台使用匹配的 CSS 和 JS 版本。</div>




<Tabs>
<Tab zoneid="QI2mYSHmWE" title="模块化集成">
<TabTitle>模块化集成</TabTitle>

当需要完整的直播间功能时使用，例如聊天、商品卡片和签到。

```HTML
// Modular integration on PC
<link rel="stylesheet" href="https://res.gcloudcache.com/bp-fe/livesaas-client/pc/css/index.2.0.31.css">
<script src="https://res.gcloudcache.com/bp-fe/livesaas-client/pc/js/index.2.0.31.js"></script>
```



</Tab>
<Tab zoneid="aN9tHdw5O3" title="仅播放器集成">
<TabTitle>仅播放器集成</TabTitle>

当只需回放功能时使用，包括点播、直播流、清晰度切换、播放速度和多线路选项。

此方法相比模块化集成具有更好的性能。

```HTML
// Player-only integration on PC
<link rel="stylesheet" href="https://res.gcloudcache.com/bp-fe/livesaas-client/player-pc/css/index.2.0.31.css">
<script src="https://res.gcloudcache.com/bp-fe/livesaas-client/player-pc/js/index.2.0.31.js"></script>
```



</Tab>
</Tabs>


<span id="a7cb4e3d"></span>
#### 移动**集成资源**

要将 SDK 集成到移动端 Web 应用中，请选择下方描述的资源之一。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">直接修改 URL 中的版本号即可更新版本。请确保为每个平台使用匹配的 CSS 和 JS 版本。</div>



<Tabs>
<Tab zoneid="vXphtjmnLm" title="模块化与全页集成">
<TabTitle>模块化与全页集成</TabTitle>

当需要完整的直播间功能时使用，例如聊天、商品卡片和签到。

```HTML
// Modular or full-page integration on Mobile
<link rel="stylesheet" href="https://res.gcloudcache.com/bp-fe/livesaas-client/mobile/css/index.2.0.31.css">
<script src="https://res.gcloudcache.com/bp-fe/livesaas-client/mobile/js/index.2.0.31.js"></script>
```



</Tab>
<Tab zoneid="KgFDjhejEp" title="仅全页集成">
<TabTitle>仅全页集成</TabTitle>

当需要集成不属于特定模块的功能时使用，如直播活动预约、主播账号或页头图。

此方法相比模块化与全页集成具有更好的性能。

```HTML
// Full-page integration on Mobile
<link rel="stylesheet" href="https://res.gcloudcache.com/bp-fe/livesaas-client/mobile-all/css/index.2.0.31.css">
<script src="https://res.gcloudcache.com/bp-fe/livesaas-client/mobile-all/js/index.2.0.31.js"></script>
```



</Tab>
<Tab zoneid="HYKymoeP5n" title="仅播放器集成">
<TabTitle>仅播放器集成</TabTitle>

在以下情况下必须使用此集成方式：


* 需要在观看页展示点播播放器。

* 需要在同一页面展示多个直播或点播播放器。


此方法相比模块化与全页集成具有更好的性能。

```HTML
// Player-only integration on Mobile
<link rel="stylesheet" href="https://res.gcloudcache.com/bp-fe/livesaas-client/player-mobile/css/index.2.0.31.css">
<script src="https://res.gcloudcache.com/bp-fe/livesaas-client/player-mobile/js/index.2.0.31.js"></script>
```



</Tab>
</Tabs>


域名：`https://res.gcloudcache.com/bp-fe`

最新版本：2.0.31

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">从版本<strong>2.0.30</strong>开始，域名已从<code>https://res.bytepluscdn.com/obj/bp-console-fe-sg</code>变更为<code>https://res.gcloudcache.com/bp-fe</code>。集成 SDK 版本<strong>2.0.30</strong>及以上时，请确保使用新的域名<code>https://res.gcloudcache.com/bp-fe</code>。</div>


* <div data-tips="true" data-tips-type="warning">从版本 1.3.8 开始，URL 中<code>byteplus</code>在<code>mobile/</code>或<code>pc/</code>后已被移除。例如，<code>https://mediaservice-fe.bytepluscdn.com/obj/vcloud-fe-sgcomm/livesaas-client/pc/byteplus/css/index.VERSIONNUMBER.css"></code>已变更为<code>https://mediaservice-fe.bytepluscdn.com/obj/vcloud-fe-sgcomm/livesaas-client/pc/css/index. VERSIONNUMBER.css""></code>。</div>



<span id="829352b2"></span>
### Step 2: 集成 Web 观播 SDK


1. 资源导入后，ByteLiveWebSDK 会挂载到全局 `window` 对象。请使用以下方法将 Web 观播 SDK 集成到您的 Web 应用中。

   ```JavaScript
   var webSDK = new window.ByteLiveWebSDK({
     activityId: 173312069231****,
     token: 'ZQ****',
     service: '',
     mode: 1,
     modules: [
       {
         id: "player",
         mode: "player", 
       }, 
       {
         id: "menu", 
         mode: "menu",
         menu: ["comment"],
       }
     ],
     options: {}
   })
   
   webSDK.emit('player.pause'); // Trigger events
   webSDK.on('player.pause', () => {}); // Listen for events
   ```
   

   有关代码中参数配置的详细信息，请参见 [Web 观播 SDK：参数](https://docs.byteplus.com/docs/byteplus-livesaas/docs-parameter-the-viewer-sdk-for-web-zh-CN)。有关事件监听与触发的详细信息，请参见 [Web 观播 SDK：事件](https://docs.byteplus.com/docs/byteplus-livesaas/docs-bdlliveengine-zh-CN)。有关 API 调用的详细信息，请参见 [API](https://docs.byteplus.com/docs/byteplus-livesaas/docs-api-the-viewer-sdk-for-web-zh-CN)。

2. （可选）覆盖样式。SDK 元素的 `class` 属性值不可更改。您可以更改样式属性及 `class` 属性对应的值，以覆盖对应元素的样式。


<span id="dc1eff46"></span>
### Step 3: 调试

请使用以下方法之一进行调试。


* 在线调试：建议您在 PC 上使用 SDK 演示 playground 进行在线调试。通过 playground，您可以配置不同版本的直播间和 SDK，修改模版中的代码，并实时预告结果。更多信息请参见 [Web 观播 SDK 演示 playground](https://live.byteplus.com/demo/sdk/index.playground.html?mode=pc)。

* 本地调试：在本地端口 `localhost:8080` 上调试。此方法无法进行预告或回放。

   1. 下载并解压包 [byte-live-sdk-demo-master-plus.zip](https://lf6-cdn-tos.douyinstatic.com/obj/livesaas/byte-live-sdk-demo-master-plus.zip)。

   2. 打开终端并运行 `cd` 命令，进入解压后的文件夹目录。例如，`cd C:\Users\Admin\Downloads\byte-live-sdk-demo-master-plus`。

   3. 运行 `yarn` 命令安装依赖。

   4. 启动服务时，Mac 运行 `yarn start` 命令，Windows 运行 `yarn start-win` 命令。

   5. 打开 [http://localhost:8080/demo/sdk/index.html](http://localhost:8080/demo/sdk/index.html) 进行调试。


<span id="1164a8f8"></span>
## 常见问题

[Web 观播 SDK 常见问题](https://docs.byteplus.com/docs/byteplus-livesaas/docs-faqs-about-web-viewer-sdk-zh-CN)
