---
title: "在 Web 上运行 RTM 演示"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-running-the-rtm-demo-for-web-zh-CN"
---

要在 Web 上测试实时媒体（RTM）流，可以使用 BytePlus MediaLive 提供的演示。本主题将带你完整了解整个流程，包括生成推流和拉流地址、推送流以及在 Web 上播放流。

<span id="0439107b"></span>
## 前提条件

你已开通 BytePlus MediaLive。


* 如果你没有推流和拉流域名，可以使用 MediaLive 提供的测试推流和拉流域名。

* 若需使用自有域名进行测试，你需要至少添加两个域名，一个用于推流，另一个用于拉流。推流和拉流域名必须配置在同一域名命名空间下。


<span id="a0cf172d"></span>
## 操作流程

<span id="b5ad8b31"></span>
### 生成推流/拉流地址


1. 在左侧导航栏，选择**工具箱** \> [地址生成器](https://docs.byteplus.com/en/byteplus-media-live/docs/address-generator)。

2. 完成配置。确保用于生成推流和拉流地址的`AppName` 和 `StreamName`一致。更多信息，请参见[生成流地址](https://docs.byteplus.com/docs/byteplus-media-live/docs-relay-zh-CN)。

3. 点击**生成推流地址**，即可在**结果**区域获取 RTM 推流地址。

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7b1cdda2de8c41df99239d8d976cefb2~tplv-goo7wpa0wc-image.image" width="812px" />   </div>
   

4. 点击**生成拉流地址**，然后可在**拉流地址**标签页获取源流的**RTM Web SDK 回放地址**，或在**转码流**标签页选择转码后缀，获取转码流的**RTM Web SDK 回放地址**。

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">如无法获取<strong>RTM Web SDK 回放地址</strong>，请联系<a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980">技术支持</a>。   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>RTM Web SDK 回放地址</strong>支持自动转码，包括 B帧移除和 AAC 到 Opus 音频转换。更多信息，请参见<a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-generating-live-stream-addresses-zh-CN">生成直播流地址</a>。   </div>
   


<span id="ec1aebfd"></span>
### 推送 RTM 流

你可以[通过 BytePlus MediaLive 控制台](https://docs.byteplus.com/en/byteplus-media-live/docs/web-push?version=v1.0)推送 RTM 流，或使用如 Open Broadcaster Software（OBS）等推流工具。请使用上一步获取的地址作为推流地址。

<span id="d1b7ef3b"></span>
### 拉取 RTM 流


1. 进入[VePlayer](https://demo.byteplus.com/common/veplayer/basic/example)，该页面为 BytePlus MediaLive 拉流 SDK for Web 的演示。

2. 在**功能配置**标签页点击**RTM 拉流**。

3. 在**代码示例**窗口，将`url`字段设置为上一步获取的**RTM Web SDK 回放地址**。

4. 点击**运行**以播放直播流。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">如果你的域名未已开启 SSL 证书，请通过 HTTP 地址访问<a href="http://demo.byteplus.com/common/veplayer/basic/example?tab=function-display">未加密版本</a>的 VePlayer 演示页面。请注意，使用演示时不应传递任何敏感信息。</div>
