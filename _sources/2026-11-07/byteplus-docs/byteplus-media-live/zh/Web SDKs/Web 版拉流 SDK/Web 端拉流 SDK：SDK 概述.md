---
title: "Web 端拉流 SDK：SDK 概述"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-web-sdk-overview-zh-CN"
---

BytePlus MediaLive Web 端拉流 SDK（也称为 VePlayer）结合[BytePlus MediaLive 的流媒体服务](https://www.byteplus.com/en/product/medialive)，为直播内容提供流畅、稳定且高质量的回放解决方案。该 SDK 兼容多种系统类型。您可以轻松将其集成到现有的 Web 应用中。

<span id="ff05fffc"></span>
## 许可证类型

Web 端拉流 SDK 提供三种类型的许可证：基础版、高级版和试用版。


* **基础版许可证**：适用于仅需基础拉流功能的直播场景，如体育赛事、娱乐、电商和教育。

* **高级版许可证**：适用于既需基础拉流功能，又需高级功能（如自适应码率流、自适应缓冲策略和[实时媒体（RTM）](https://docs.byteplus.com/en/byteplus-media-live/docs/introduction-to-real-time-media)）的直播场景。更多信息请参见[功能](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-web-sdk-overview-zh-CN#ba9be9fe)。

* **试用版许可证**：适用于测试等试用场景。该版本包含 Web 端拉流 SDK 的全部功能。


<span id="b49f0040"></span>
## 版本

Web 端拉流 SDK 2.x 相较于 1.x 版本进行了如下优化：


* 集成流程优化，包体积减小；

* 播放器创建流程增强；

* 播放器配置、方法、属性和事件格式优化。


这些优化显著提升了播放器性能和用户体验，同时也便于集成和使用。建议升级至 2.x 版本，以获得更佳的播放器性能和体验。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">2.x 版本为不兼容升级，不支持点播（VOD）功能。如需同时播放在线流和点播内容，请使用旧版本 SDK。更多信息请参见<a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-web-1-x-versions">Web 端拉流 SDK：1.x 版本</a>。</div>


<span id="356d2ba0"></span>
## SDK 演示

如需体验 SDK 演示，请访问[VePlayer](https://demo.byteplus.com/common/veplayer/v2/basic/example?tab=function-display)，并切换不同标签页以探索各项功能。提供示例代码，帮助您学习如何实现各项功能，并可调整代码以观察播放器行为的变化。

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ee01088a972943a385f4f2ba99ab856b~tplv-goo7wpa0wc-image.image) </span>

<span id="600333d3"></span>
## 协议支持

下表列出了 Web 端拉流 SDK 支持的流媒体协议：


|**协议** |**特性** |**H.264** ||**H.265** ||
|---|---|---|---|---|---|
|||**PC** |**移动端** |**PC** |**移动端** |
|HLS |* 兼容性强<br><br>* 延迟较高 |支持 |支持 |支持 |部分支持 |
|FLV |* 低延迟<br><br>* H5 支持较差 |支持 |部分支持 |支持 |部分支持 |
|RTM |* 低延迟<br><br>* 在网络连接较差时表现稳定 |支持 |部分支持 |不支持 |不支持 |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">使用 RTM 协议进行回放时，浏览器需支持<a href="https://caniuse.com/?search=WebRTC%20Peer-to-peer%20connections">WebRTC</a>。</div>


* <div data-tips="true" data-tips-type="tip">在 Android 设备上，部分浏览器可能会劫持播放器，导致部分功能不可用。</div>


* <div data-tips="true" data-tips-type="tip">如需播放采用 H.265 编码且通过 HLS 或 FLV 协议传输的在线流，需先确认浏览器是否支持 H.265 软件或硬解。</div>



<span id="ba9be9fe"></span>
## 功能

拉流 SDK 兼容主流浏览器。可根据系统类型自动选择最优回放方案。


|**功能** |**PC** |**移动端** |
|---|---|---|
|自定义播放器尺寸 |支持 |支持 |
|自定义封面图 |支持 |支持 |
|自动播放 |支持 |支持 |
|同一页面多播放器 |支持 |支持 |
|分辨率切换 |支持 |支持 |
|截图 |支持 |支持 |
|全屏 |支持 |支持 |
|视频旋转 |支持 |支持 |
|音量调节 |支持 |支持 |
|画中画 |支持 |不支持 |
|H.264 |支持 |支持 |
|H.265 |部分支持 |部分支持 |
|URL 鉴权 |支持 |支持 |
|Referer 白名单与 blocklist |支持 |支持 |
|IP 白名单与 blocklist |支持 |支持 |
|自定义错误消息 |支持 |支持 |
|弹幕 |支持 |支持 |
|动态降级至备流 |支持 |支持 |
|动态降级至低分辨率 |支持 |支持 |
|直播信息面板 |支持 |支持 |
|日志上传 |支持 |支持 |
|播放时移直播内容 |支持 |支持 |
|监听 SEI 消息 |支持 |支持 |
|[播放 RTM 流](https://docs.byteplus.com/en/docs/byteplus-media-live/RTM-Streaming-Integration) |仅高级版或试用版部分支持 |仅高级版或试用版部分支持 |
|[自适应码率流](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-adaptive-bitrate-streaming-abr) |仅高级版或试用版支持 |仅高级版或试用版部分支持 |
|[自适应缓冲策略](https://docs.byteplus.com/en/docs/byteplus-media-live/adaptive-buffer-strategy) |仅高级版或试用版部分支持 |仅高级版或试用版部分支持 |
|[低延迟 FLV 拉流](https://docs.byteplus.com/en/docs/byteplus-media-live/achieving_2-3s_live_stream_latency_with_low-latency_FLV_web) |仅高级版或试用版支持 |仅高级版或试用版部分支持 |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Web 端拉流 SDK 默认已开启自动播放。但部分浏览器策略可能会影响自动播放行为。例如，参见<a href="https://developer.chrome.com/blog/autoplay/">Chrome 自动播放策略</a>。</div>


* <div data-tips="true" data-tips-type="tip">画中画功能基于 Chrome 浏览器在 PC 端提供的<a href="https://www.w3.org/TR/picture-in-picture/">画中画</a>支持实现。</div>


* <div data-tips="true" data-tips-type="tip"><a href="https://caniuse.com/?search=HEVC">支持 H.265 硬解的浏览器</a>可直接播放 H.265 视频。对于其他浏览器，可以通过设置<code>degradation</code>参数启用软解。</div>
