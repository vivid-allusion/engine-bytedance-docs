---
title: "集成 Web 端拉流 SDK"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-integrating-the-player-sdk-for-web-zh-CN"
---

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">本文适用于 BytePlus MediaLive 拉流 SDK for Web 的 1.x 版本。强烈建议升级至最新版本，以获得更优的播放器体验。</div>


本文介绍如何将 BytePlus MediaLive 拉流 SDK for Web（也称为 VePlayer）集成到您的 Web 应用程序中。集成流程包括以下步骤：


1. 导入依赖

2. 添加播放器容器

3. 创建 VePlayer 实例

4. 实现更多功能


<span id="Prerequisites"></span>
## 前提条件

要让拉流 SDK 拉取通过 BytePlus MediaLive 分发的流，请在开始前完成以下操作：


* 添加域名和 CNAME 记录。更多信息请参见[添加域名](https://docs.byteplus.com/docs/byteplus-media-live/docs-domain#bb9e1337)和[添加 CNAME 记录](https://docs.byteplus.com/docs/byteplus-media-live/docs-adding-a-cname-record)。

* [生成拉流地址](https://docs.byteplus.com/byteplus-media-live/docs/address-generator)。如需使用 HTTPS 拉流地址，需先添加证书并完成 HTTPS 配置。更多信息请参见[管理 SSL 证书](https://docs.byteplus.com/docs/byteplus-media-live/docs-managing-certificates)和[添加 SSL 证书](https://docs.byteplus.com/docs/byteplus-media-live/docs-https)。


<span id="Importing dependencies"></span>
## 导入依赖

<span id="6298ac53"></span>
### 通过 CDN 导入

要通过 CDN 导入拉流 SDK 的 CSS 和 JS 文件，请在本地项目的`index.html`文件中添加如下代码：

```HTML
<link rel="stylesheet" href="//sf-unpkg.bytepluscdn.com/obj/byteplusfe-sg/sdk/@byteplus/veplayer/1.6.3/index.min.css">
<script src="//sf-unpkg.bytepluscdn.com/obj/byteplusfe-sg/sdk/@byteplus/veplayer/1.6.3/index.min.js"></script>
```


<span id="6b8a8eb3"></span>
### 通过 NPM 导入


1. 要通过 NPM 安装 SDK 依赖，请运行以下命令：


```Bash
npm install @byteplus/veplayer
```



2. 安装完成后，按如下方式将 VePlayer 及其 CSS 文件导入到您的项目中：


```Bash
import VePlayer from '@byteplus/veplayer';
import '@byteplus/veplayer/dist/index.min.css';
```


<span id="Adding a container for the player"></span>
## 添加播放器容器

在需要展示播放器的页面添加播放器容器。例如，在`index.html`中添加如下代码：

```html
<div id="video"></div>
```


<span id="Creating a VePlayer instance"></span>
## 创建 VePlayer 实例

使用如下代码创建 VePlayer 实例。页面加载后，播放器会自动开始播放。如需播放直播流，请将`isLive`设置为`true`，并将`url`设置为拉流地址。有关参数详情，请参见[API 参考](https://docs.byteplus.com/byteplus-media-live/docs/api-reference)。

```javascript
const playerSdk = new VePlayer({
  id: 'video',
  isLive: true,
  url: '//livepull.example.com/appname/streamname.flv'
});
```


<span id="Implementing more features"></span>
## 实现更多功能

拉流 SDK 提供多种功能，覆盖多种回放场景，包括自定义封面图、画中画、进度条悬停预告缩略图，以及自动视频分辨率降级、基于 RTM 协议播放直播流等高级功能。

有关拉流 SDK 提供的参数、方法和回调的详细说明，请参见[API 参考](https://docs.byteplus.com/byteplus-media-live/docs/api-reference)。
