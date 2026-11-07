---
title: "将服务器时间戳数据插入 SEI 消息"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/inserting-server-timestamp-data-into-SEI-messages-zh-TW"
---

为帮助您分析直播延迟，BytePlus MediaLive 支持将服务器时间戳数据插入 SEI（Supplemental Enhancement Information）消息。为推流域名启用此功能后，MediaLive 会为该推流域名所属域名空间下的所有直播流，将服务器时间戳数据插入 SEI 消息。您可以使用 BytePlus MediaLive Player SDK 或您自己的 SEI 解析器来计算和分析延迟。

## 前提条件

* 联系[技术支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)启用此功能。

* 一个推流域名。有关如何添加推流域名的更多信息，请参见[添加域名](https://docs.byteplus.com/docs/byteplus-media-live/docs-domain)。

## 操作步骤

1. 登录 [BytePlus MediaLive 控制台](https://console.byteplus.com/live/main/domain/list)。

2. 在左侧导航窗格中，单击**域名**。

3. 在**域名**页面，单击目标推流域名右侧的**设置**。

4. 在**高级设置**页签，单击**编辑**，然后开启或关闭 **SEI 插入服务器时间戳**开关。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/33a1a2a75e554c9faa5edc5b232af63b~tplv-goo7wpa0wc-topic.webp)

   * 开启：为该推流域名所属域名空间下的所有直播流，将服务器时间戳数据插入 SEI 消息。然后，您可以使用 SEI 消息分析直播延迟。有关服务器时间戳数据的更多信息，请参见 [SEI 消息中的服务器时间戳数据](https://docs.byteplus.com/docs/byteplus-media-live/119943#b312d852)。

   * 关闭：不将服务器时间戳数据插入 SEI 消息。

   > **说明**

   > 开启此功能后，MediaLive 在将服务器时间戳数据写入 SEI 消息时使用 `5` 作为 SEI `type` 值。如果您的推流工具或应用也会向流中写入自定义 SEI 消息，请避免使用相同的 SEI `type` 值。否则，播放器可能会将自定义数据识别为服务器时间戳数据。

5. 单击**确认**。

### SEI 消息中的服务器时间戳数据

开启 **SEI 插入服务器时间戳**开关后，SEI 消息可以包含以下 Unix 时间戳，单位为毫秒。每个时间戳记录流到达流媒体传输路径中某个特定 MediaLive 节点的时间。您可以使用这些时间戳计算特定维度的直播延迟。

|字段 |描述 |
|---|---|
|push_edge_ts |流到达 MediaLive 推流侧边缘节点的时间。 |
|transpush_edge_ts |流到达 MediaLive 推流侧转发节点的时间。 |
|source_ts |流到达 MediaLive 源站节点的时间。 |
|trans_src_ts |流到达 MediaLive 区域源站节点的时间。 |
|transpull_edge_ts |流到达 MediaLive 二级转发节点的时间。 |
|pull_edge_ts |流到达 MediaLive 拉流侧边缘节点的时间。 |
|hls_source_ts |流到达 MediaLive HLS 分片源站节点的时间。 |
|cmaf_source_ts |流到达 MediaLive CMAF 分片源站节点的时间。 |

## 后续操作

开启 **SEI 插入服务器时间戳**开关后，您可以：

* 使用适用于 iOS、Android 和 Web 的 BytePlus MediaLive Player SDK 从 SEI 消息获取延迟数据。

   * 适用于 iOS 和 Android 的 Player SDK：使用 Android Player SDK 1.52.100.5 或更高版本，或 iOS Player SDK 1.52.100.4\-premium 或更高版本。对于 Android，将 [enableStatisticsCallback](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerConfiguration-enablestatisticscallback) 设置为 `true`；对于 iOS，将 [enableStatisticsCallback](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerConfiguration-enablestatisticscallback) 设置为 `YES`。然后，对于 Android，从 [onStatistics](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onstatistics) 回调获取延迟统计数据；对于 iOS，从 [onStatistics:statistics:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onstatistics-statistics) 回调获取延迟统计数据。

      |字段 |计算方法 |描述 |
      |---|---|---|
      |delayS2sMs |pull_edge_ts \- push_edge_ts |服务器到服务器延迟，单位为毫秒。表示流从 MediaLive 推流侧边缘节点传输到 MediaLive 拉流侧边缘节点所需的时间。当 SEI 消息不包含流到达推流侧边缘节点和拉流侧边缘节点的服务器时间戳时，取值为 `-1`。 |
      |delayE2eMs |Player SDK 解析 SEI 消息时的本地时间戳 \- SEI 消息中的 Broadcast SDK 时间戳 |端到端延迟，单位为毫秒。表示从 Broadcast SDK 将时间戳写入 SEI 消息，到 Player SDK 在本地解析 SEI 消息所需的时间。准确计算依赖基于 NTP 的时钟同步。当 SEI 消息不包含 Broadcast SDK 写入的时间戳时，取值为 `-1`。 |
      |delayS2eMs |Player SDK 解析 SEI 消息时的本地时间戳 \- push_edge_ts |服务器到终端延迟，单位为毫秒。表示从流到达 MediaLive 推流侧边缘节点，到 Player SDK 在本地解析 SEI 消息所需的时间。准确计算依赖基于 NTP 的时钟同步。当 SEI 消息不包含流到达 MediaLive 推流侧边缘节点的服务器时间戳时，取值为 `-1`。 |

   * 适用于 Web 的 Player SDK：使用 Web Player SDK 2.13.0 或更高版本。对于 RTM 流，将 [enableSei](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-web-options#rtm) 设置为 `true`，并调用 [getRTMStats()](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-web-methods-and-properties#veplayerlive-getrtmstats) 获取延迟统计数据。对于 FLV 流，调用 [getFLVStats()](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-web-methods-and-properties#veplayerlive-getflvstats) 获取延迟统计数据。

      |字段 |计算方法 |描述 |
      |---|---|---|
      |delay_s2s |pull_edge_ts \- push_edge_ts |服务器到服务器延迟，单位为毫秒。表示流从 MediaLive 推流侧边缘节点传输到 MediaLive 拉流侧边缘节点所需的时间。当有效的服务器 SEI 数据不可用时为空。 |
      |delay_s2e |Player SDK 解析 SEI 消息时的本地时间戳 \- push_edge_ts + 本地播放器缓冲时长 |服务器到终端延迟，单位为毫秒。表示从流到达 MediaLive 推流侧边缘节点，到 Web Player SDK 播放对应帧所需的时间。由于 Player SDK 在播放对应帧之前解析 SEI 消息，因此计算中包含本地播放器缓冲时长。当有效的服务器 SEI 数据不可用时为空。 |

* 自行解析 SEI 数据。如果您使用自己的 SEI 解析器，可以解析 SEI 消息中的服务器时间戳数据，并根据业务需求计算延迟。有关 SEI 消息中的具体时间戳，请参见 [SEI 消息中的服务器时间戳数据](https://docs.byteplus.com/docs/byteplus-media-live/119943#b312d852)。
