---
title: "HLS 和 LL-HLS"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/hls-and-ll-hsl-zh-CN"
---

为了降低延迟并提升您的在线流兼容性，您可以配置 HLS 和低延迟 HLS（LL\-HLS）封装设置。本文为您提供在 BytePlus MediaLive 控制台调整参数（如分片时长和数量）的详细操作步骤。

<span id="395df62c"></span>
## HLS 的工作原理

了解 HLS 如何传输直播视频的基本原理，有助于您更有效地配置相关设置。

HLS 的原理是将您的持续直播流拆分为多个较小的视频片段，称为**分片**。随后，HLS 协议会将这些分片的网络地址（URI）列在一个文本文件中，该文件称为**播放列表**（扩展名为`.m3u8`）。

对于直播流，该播放列表会持续更新：新分片生成后，其地址会被添加到列表中，旧分片的地址则会被移除。播放器会反复下载该播放列表，以获取并播放最新的分片。

正因为这种切片机制，您会看到类似**时长**的设置项。您配置的这些分片时长会直接影响回放延迟、稳定性以及观众回看能力。

<span id="a77e62f0"></span>
## 限制说明


* HLS/LL\-HLS 封装适用于推流、使用 FLV 和 RTMP 协议的拉流回源，以及使用 HLS 的拉流。但不支持基于 HLS 的拉流回源。

* HLS/LL\-HLS 封装配置不仅适用于该域名下的流，也适用于同一域名空间下关联的其他域名的流。

* 若已开启[HLS-ABR](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-configuring-an-hls-abr-task)功能，HLS/LL\-HLS 封装配置将不会生效。

* 封装配置将在 3 到 5 分钟内生效。


<span id="5291f43e"></span>
## 前提条件

需要支持 LL\-HLS 的播放器。

<span id="1b226441"></span>
## 操作步骤


1. 登录[BytePlus MediaLive 控制台](https://console.byteplus.com/live)。

2. 在左侧导航栏，点击**域名**。

3. 找到您需要配置的拉流域名，在**操作**列点击**设置**。

4. 点击**高级设置**标签页。

5. 在 HLS/LL\-HLS 区域点击**编辑**，打开弹窗并配置以下设置：

   * **S** **egment duration**：可输入 1 到 60 的整数。建议直播流的关键帧间隔（GOP）保持稳定，且时长等于或为 GOP 的整数倍。

   * **Segment number**：播放列表中包含的媒体分片数量。可输入 2 到 10 的整数。

   * **Segment number in the initial playlist**：初始播放列表中的媒体分片数量。较小的数值可加快初始回放速度。

   * **Low latency HLS**：低延迟 HLS 扩展协议，实现低延迟视频流传输并保持可扩展性。该功能默认未开启。

   * **Partial segment duration**：低延迟 HLS 会将每个媒体分片拆分为更多更小的文件。这些更小的文件称为 Partial Segments。常规媒体分片可能每个为 6 秒，而 Partial Segment 示例可能仅为 200 毫秒。

   * **Insert PDT**：指定是否在 M3U8 播放列表中插入 #EXT\-X\-PROGRAM\-DATE\-TIME 标签。

   * **PDT Interval**：若启用 PDT 插入，则设置插入间隔（单位：秒）。该数值的范围可以是 0 到 3600。

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">如果 PDT 间隔设置为 0 或小于分段时长，则每个分段都会插入一个 PDT 标签。      </div>
