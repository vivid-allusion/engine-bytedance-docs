---
title: "在 Web 上实现媒体上下滑动"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/docs-interactive-video-solution-web-zh-CN"
---

要构建具有垂直滚动、评论和点赞等功能的媒体上下滑动信息流，您可以从提供的 Demo 入手。本指南将说明如何自定义 Demo 的播放器、语言设置和部署配置，以高效地在您的 Web 项目中实现类似解决方案。

<span id="7dd1b50a"></span>
# 前提条件


* 已开通 BytePlus VOD 的有效 BytePlus 账号。请参考 BytePlus VOD 入门中的[步骤 1：启用 BytePlus VOD 服务](https://docs.byteplus.com/en/docs/byteplus-vod/docs-getting-started#b4e9d150)。

* 按照[运行 Demo (Web/H5)](https://docs.byteplus.com/docs/byteplus-vos/docs-running-the-demo-web-zh-CN)中的流程成功运行 Demo 项目。


<span id="5f2dd2d3"></span>
# 实现

项目成功运行后，您可以通过修改几个关键配置文件，自定义属于自己的 Feed 流网站。

<span id="d49ff281"></span>
## 播放器配置

本节将概述 Demo 中的播放器配置。

> 如需更详细的配置，请参阅 BytePlus VOD [Web Player SDK API 参考](https://docs.byteplus.com/en/docs/byteplus-vod/docs-web-api-reference)。



|参数 |数据类型 |默认值 |说明 |
|---|---|---|---|
|el |HTMLElement |\- |VePlayer 插入用于展示和交互的 HTML 元素。 |
|getVideoByToken |[getVideoByToken](https://docs.byteplus.com/en/docs/byteplus-vod/docs-web-api-reference#getvideobytoken) |\- |用于获取所需播放视频的配置。详细说明请参阅[getVideoByToken](https://docs.byteplus.com/en/docs/byteplus-vod/docs-web-api-reference#getvideobytoken)。 |
|poster |string |\- |封面图片的 URL。 |
|mobile |```JSON```<br>```{```<br>```   gradient: string```<br>```}```<br> |\- |移动端 Web 播放器的交互插件。<br><br>`gradient`：是否启用渐变阴影。支持的取值：<br><br><br>* normal：正常阴影效果<br><br>* none：无阴影<br><br>* top：顶部阴影<br><br>* bottom：底部阴影 |
|autoplay |boolean |false |是否启用自动播放。<br><br><br>* true：是<br><br>* false：否<br><br>> 由于浏览器策略，自动播放可能无法始终成功，具体取决于浏览器环境、用户行为及浏览器配置等因素。 |
|loop |boolean |false |是否启用循环播放。<br><br><br>* true：是<br><br>* false：否 |
|enableDegradeMuteAutoplay |boolean |false |当带声音自动播放失败时，是否降级为静音自动播放。支持的取值：<br><br><br>* true：是<br><br>* false：否<br><br><br>当 `enableDegradeMuteAutoplay` 和 `autoplay` 均设置为 `true` 时，若当前浏览器不支持带音频自动播放，播放器将降级为静音自动播放。请注意，静音自动播放也可能失败。 |
|closeVideoClick |boolean |false |* 桌面端：是否通过点击播放器区域切换播放/暂停。<br><br>* 移动端：是否通过关闭视频的点击/touchend 行为切换播放/暂停。 |
|closeVideoDblclick |boolean |false |* 桌面端：是否禁用通过双击播放器进入全屏模式的功能。<br><br>* 移动端：是否禁用通过双击切换播放/暂停的功能。 |
|controls |boolean |true |控制栏插件，默认注册。 |
|ignores |string[] |[] |用于禁用插件。VePlayer 内置了多种常用功能的插件。如需禁用某个内置插件，可将插件名称（不区分大小写）作为参数传入。 |
|start |```JSON```<br>```{```<br>```  disableAnimate: boolean,```<br>```  isShowPause: boolean,```<br>```}```<br> |false |播放器中央用于切换播放/暂停的按钮。<br><br>`disableAnimate`: 是否禁用点击动画效果。<br><br><br>* true：是<br><br>* false：否（默认）<br><br><br>`isShowPause`: 暂停时是否保持界面可见。<br><br><br>* true：是<br><br>* false：否（默认） |


<span id="84c261da"></span>
## 多语言配置

如需修改翻译或添加多语言，可修改 `translation.ts` 文件中的配置，或使用实现国际化功能的库，如[@formatjs/intl](https://www.npmjs.com/package/@formatjs/intl)。

<span id="383ec30e"></span>
## 部署

生成构建产物，只需运行 `pnpm run build`。在部署阶段，请注意 `vite.config.ts` 文件中的 `base` 和 `build` 配置。以下是需要关注的两个关键点：


* 构建输出目录默认设置为“output”。如需调整，可在 `build` 配置下修改 `outDir` 属性。

* 配置静态资源的公共基础路径：如果您的资源直接托管在同一服务器上，可保持默认根路径(`/`)。但如果使用 CDN，请获取您的加速域名，并将配置中的\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*占位符替换为实际域名。


```JavaScript
export default defineConfig({
  base: isProd ? '***************' : '/',
  server: {
    port: 8000,
  },
  build: {
    outDir: 'output',
  },
});
```
