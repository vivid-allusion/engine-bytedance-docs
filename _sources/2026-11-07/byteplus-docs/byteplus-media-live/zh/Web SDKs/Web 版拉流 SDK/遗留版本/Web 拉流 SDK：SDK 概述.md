---
title: "Web 拉流 SDK：SDK 概述"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-introduction-to-the-player-sdk-for-web-zh-CN"
---

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">本文适用于 BytePlus MediaLive Web 拉流 SDK 1.x 版本。强烈建议升级至最新版本，以获得更优的播放器体验。</div>


BytePlus MediaLive Web 拉流 SDK（也称为 VePlayer），结合 [BytePlus MediaLive 的流服务](https://www.byteplus.com/en/product/medialive)，为在线流提供流畅、稳定、高质量的回放解决方案。该 SDK 兼容多种系统类型。您可以轻松集成到现有的 Web 应用中。

<span id="fe6b462a"></span>
## SDK 演示

要体验 SDK 演示，请访问 [VePlayer](https://demo.byteplus.com/common/veplayer/basic/example)，并切换不同标签页以探索各项功能。提供示例代码，帮助您学习如何实现各项功能，并可调整代码以观察播放器行为的变化。

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4e7e7ac0d5984d6a88e824809da38da1~tplv-goo7wpa0wc-image.image) </span>

<span id="6e1358a3"></span>
## 协议支持

下表列出了 Web 拉流 SDK 支持的流协议：


|**协议** |**优缺点** |**H.264** ||**H.265** ||
|---|---|---|---|---|---|
|||**PC** |**移动端** |**PC** |**移动端** |
|HLS |* 兼容性广<br><br>* 延迟高 |支持 |支持 |支持 |部分支持 |
|FLV |* 低延迟<br><br>* H5 支持较差 |支持 |部分支持 |支持 |部分支持 |
|RTM |* 低延迟<br><br>* 在网络类型较差时表现稳定 |支持 |部分支持 |不支持 |不支持 |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">使用 RTM 协议进行回放时，浏览器需支持 <a href="https://caniuse.com/?search=WebRTC%20Peer-to-peer%20connections">WebRTC</a>。</div>


* <div data-tips="true" data-tips-type="tip">在 Android 设备上，部分浏览器可能会劫持播放器，导致部分功能无法使用。</div>


* <div data-tips="true" data-tips-type="tip">如需播放采用 H.265 编码并通过 HLS 或 FLV 协议推送的在线流，需先确认浏览器是否支持 H.265 软解或硬解。</div>



<span id="8af48d51"></span>
## 功能

Web 拉流 SDK 兼容主流浏览器。SDK 会根据系统类型自动选择最优回放方案。


|**功能** |**PC** |**移动端** |
|---|---|---|
|独立播放器尺寸自定义 |支持 |支持 |
|封面图自定义 |支持 |支持 |
|自动播放 |支持 |支持 |
|同页面多播放器 |支持 |支持 |
|分辨率切换 |支持 |支持 |
|全屏 |支持 |支持 |
|视频旋转 |支持 |支持 |
|音量调节 |支持 |支持 |
|画中画 |支持 |部分支持 |
|H.264 |支持 |支持 |
|H.265 |部分支持 |部分支持 |
|自定义错误信息 |支持 |支持 |
|弹幕 |支持 |支持 |
|动态降级至备流 |支持 |支持 |
|动态降级至低分辨率 |支持 |支持 |
|直播信息面板 |支持 |支持 |
|日志上传 |支持 |支持 |
|时移直播回放 |支持 |支持 |
|拉取 RTM 流 |部分支持 |部分支持 |
|监听 SEI 信息 |支持 |支持 |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Web 拉流 SDK 默认已开启自动播放。但部分浏览器策略会影响自动播放行为。例如，<a href="https://developer.chrome.com/blog/autoplay/">Chrome 的自动播放策略</a>。</div>


* <div data-tips="true" data-tips-type="tip"><a href="https://caniuse.com/?search=HEVC">支持 H.265 硬解的浏览器</a>可直接播放 H.265 编码视频，其他浏览器可通过设置 <code>useSoftDecoding</code> 为 <code>true</code>，启用软解播放 H.265 编码视频。</div>
