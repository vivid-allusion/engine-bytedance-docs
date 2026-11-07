---
title: "Web 推流 SDK：SDK 概述"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-introduction-to-the-broadcast-sdk-for-web-zh-CN"
---

BytePlus MediaLive 推流 SDK 专为直播场景设计，帮助主播将浏览器采集的音视频内容顺畅推送至流媒体服务器。该 SDK 支持多种推流场景，包括摄像头推流、屏幕共享、在线视频推流、本地视频混流以及音频混流。借助[BytePlus MediaLive 的推流服务](https://www.byteplus.com/en/product/medialive)，您可以快速在 Web 上启用直播能力。

<span id="912d74c3"></span>
## 协议支持

推流 SDK 支持使用 RTM 协议推送 H.264 编码的内容。

<span id="7ecc10a5"></span>
## 浏览器支持

建议您使用**最新稳定版本**的网页浏览器，以提升直播体验。


|**平台** ||**Chrome 70 及以上** |**Edge 83 及以上** |**Safari 12 及以上** |**Firefox 80 及以上** |
|---|---|---|---|---|---|
|PC |Windows 10 |支持<br><br>（屏幕共享需 Chrome 74 及以上。） |支持<br><br>（屏幕共享需 Edge 99 及以上。） |不支持 |支持 |
||macOS 15 |支持<br><br>（屏幕共享需 Chrome 74 及以上。） |支持 |支持<br><br>（屏幕共享需 Safari 13 及以上。） |支持 |
|移动端 ||该 SDK 官方暂不支持移动设备。如需将 SDK 集成至您的移动应用，请联系您的销售代表。 ||||
|Electron ||该 SDK 官方暂不支持 Electron。如需将 SDK 集成至您的 Electron 应用，请联系您的销售代表。 ||||


<span id="a26cb472"></span>
## 功能

BytePlus MediaLive 推流 SDK 支持多种推流场景，包括：


* 摄像头推流：支持将摄像头采集的视频和音频推送至服务器。

* 麦克风推流：支持采集并推送麦克风音频。

* 屏幕共享：支持将屏幕内容作为视频推流。

* 本地/在线视频推流：支持从本地视频文件和在线视频源进行推流。

* 本地视频混流：支持本地混合多路视频流，内置模版并可自定义混流参数。


<span id="bc9faa42"></span>
## 限制


* 推流 SDK 当前暂不支持在 H5 页面集成。

* 使用推流 SDK 推送的流当前不支持 LL\-HLS 回放。
