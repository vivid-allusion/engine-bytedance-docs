---
title: "DASH 和 LL-DASH"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/dash-and-ll-dash-zh-CN"
---

在基于 HTTP 的动态自适应流媒体（DASH）和低延迟 DASH（LL\-DASH）中，直播流会被切分为 Common Media Application Format（CMAF）分段。您可以调整时长和分段数量设置，以有效降低延迟并提升直播流的兼容性。

<span id="a77e62f0"></span>
## 限制


* DASH 封装适用于推流、拉流回源（支持 HLS、FLV 和 RTMP 协议），以及通过 DASH over CMAF 进行拉流。

* DASH 封装配置适用于指定域名及同一域名空间下的所有其他域名。

* 封装配置将在 3 到 5 分钟内生效。


<span id="5291f43e"></span>
## 前提条件


* 需要支持 DASH 的播放器。

* iOS 10.0、macOS 10.12 和 tvOS 10.0 或更高版本操作系统支持 CMAF 内容。


<span id="1b226441"></span>
## 操作流程


1. 进入 [BytePlus MediaLive 控制台 > 域名](https://console.byteplus.com/live/main/domain/list)。

2. 找到您要配置拉流的拉流域名，在 **操作**栏点击 **设置**。

3. 点击 **高级设置**标签页。

4. 在 DASH 区域点击 **编辑**，打开对话框并配置以下设置：

   * **CMAF** **S** **egment duration**：您可以输入 1 到 60 的整数。为获得最佳性能，请确保直播流的关键帧间隔稳定，并将分段时长设置为等于或为关键帧间隔的整数倍。

   * **Segment number**：播放列表中包含的媒体分段数量。您可以输入 3 到 10 的整数。

   * **Low\-Latency DASH**：Low\-Latency DASH 扩展协议，实现低延迟视频流，同时保持可扩展性。
