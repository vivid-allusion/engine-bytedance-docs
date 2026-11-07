---
title: "Inserting server timestamp data into SEI messages"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/inserting-server-timestamp-data-into-SEI-messages"
---

To help you analyze live streaming latency, BytePlus MediaLive supports inserting server timestamp data into SEI (Supplemental Enhancement Information) messages. After you enable this feature for a domain name for stream pushing, MediaLive inserts server timestamp data into SEI messages for all live streams under the domain name space to which the domain name for stream pushing belongs. You can use BytePlus MediaLive Player SDKs or your own SEI parser to calculate and analyze latency.

## Prerequisites

* Contact [technical support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) to enable this feature.

* A domain name for stream pushing. For more information on how to add a domain name for stream pushing, see [Adding a domain name](https://docs.byteplus.com/docs/byteplus-media-live/docs-domain).

## Procedure

1. Log in to the [BytePlus MediaLive console](https://console.byteplus.com/live/main/domain/list).

2. In the left\-side navigation pane, click **Domains**.

3. On the **Domains** page, click **Settings** to the right of the target domain name for stream pushing.

4. On the **Advanced settings** tab, click **Edit** and then turn on or off the **SEI insert server timestamp** switch.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/33a1a2a75e554c9faa5edc5b232af63b~tplv-goo7wpa0wc-topic.webp)

   * Turn on: Insert server timestamp data into SEI messages for all live streams under the domain name space to which the domain name for stream pushing belongs. You can then use the SEI messages to analyze live streaming latency. For more information about the server timestamp data, see [Server timestamp data in SEI messages](https://docs.byteplus.com/docs/byteplus-media-live/119943#b312d852).

   * Turn off: Do not insert server timestamp data into SEI messages.

5. Click **Confirm**.

### Server timestamp data in SEI messages

After you turn on the **SEI insert server timestamp** switch, SEI messages can include the following Unix timestamps, in milliseconds. Each timestamp records when the stream reaches a specific MediaLive node in the streaming path. You can use these timestamps to calculate live streaming latency in specific dimensions.

|Field |Description |
|---|---|
|push_edge_ts |The time when the stream reaches the MediaLive push\-side edge node. |
|transpush_edge_ts |The time when the stream reaches the MediaLive push\-side forwarding node. |
|source_ts |The time when the stream reaches the MediaLive origin node. |
|trans_src_ts |The time when the stream reaches a MediaLive regional origin node. |
|transpull_edge_ts |The time when the stream reaches the MediaLive second\-level forwarding node. |
|pull_edge_ts |The time when the stream reaches the MediaLive pull\-side edge node. |
|hls_source_ts |The time when the stream reaches the MediaLive HLS segment origin node. |
|cmaf_source_ts |The time when the stream reaches the MediaLive CMAF segment origin node. |

## What to do next

After you turn on the **SEI insert server timestamp** switch, you can:

* Use BytePlus MediaLive Player SDKs for iOS, Android, and Web to get latency data from SEI messages.

   * Player SDKs for iOS and Android: Use Player SDK for Android 1.52.100.5 or later, or Player SDK for iOS 1.52.100.4\-premium or later. Set [enableStatisticsCallback](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerConfiguration-enablestatisticscallback) to `true` for Android or [enableStatisticsCallback](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerConfiguration-enablestatisticscallback) to `YES` for iOS. Then, get latency statistics from the [onStatistics](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onstatistics) callback for Android or the [onStatistics:statistics:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onstatistics-statistics) callback for iOS.

      |Field |Calculation method |Description |
      |---|---|---|
      |delayS2sMs |pull_edge_ts \- push_edge_ts |Server\-to\-server delay, in milliseconds. Indicates the time taken for the stream to travel from the MediaLive push\-side edge node to the MediaLive pull\-side edge node. The value is `-1` when the SEI message does not contain the server timestamps for when the stream reaches the push\-side edge node and the pull\-side edge node. |
      |delayE2eMs |Player SDK local timestamp when parsing the SEI message \- Broadcast SDK timestamp in the SEI message |End\-to\-end delay, in milliseconds. Indicates the time taken from when the Broadcast SDK writes the timestamp into the SEI message to when the Player SDK parses the SEI message locally. Accurate calculation depends on NTP\-based clock synchronization. The value is `-1` when the SEI message does not contain the timestamp written by the Broadcast SDK. |
      |delayS2eMs |Player SDK local timestamp when parsing the SEI message \- push_edge_ts |Server\-to\-end delay, in milliseconds. Indicates the time taken from when the stream reaches the MediaLive push\-side edge node to when the Player SDK parses the SEI message locally. Accurate calculation depends on NTP\-based clock synchronization. The value is `-1` when the SEI message does not contain the server timestamp for when the stream reaches the MediaLive push\-side edge node. |

   * Player SDK for Web: Use Player SDK for Web 2.13.0 or later. For RTM streams, set [enableSei](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-web-options#rtm) to `true` and call [getRTMStats()](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-web-methods-and-properties#veplayerlive-getrtmstats) to get latency statistics. For FLV streams, call [getFLVStats()](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-web-methods-and-properties#veplayerlive-getflvstats) to get latency statistics.

      |Field |Calculation method |Description |
      |---|---|---|
      |delay_s2s |pull_edge_ts \- push_edge_ts |Server\-to\-server delay, in milliseconds. Indicates the time taken for the stream to travel from the MediaLive push\-side edge node to the MediaLive pull\-side edge node. Empty when valid server SEI data is unavailable. |
      |delay_s2e |Player SDK local timestamp when parsing the SEI message \- push_edge_ts + local player buffer duration |Server\-to\-end delay, in milliseconds. Indicates the time taken from when the stream reaches the MediaLive push\-side edge node to when the Player SDK for Web plays the corresponding frame. Because the Player SDK parses the SEI message before playing the corresponding frame, the local player buffer duration is included in the calculation. Empty when valid server SEI data is unavailable. |

* Parse the SEI data yourself. If you use your own SEI parser, you can parse the server timestamp data in SEI messages and calculate latency based on your business needs. For specific timestamps in SEI messages, see [Server timestamp data in SEI messages](https://docs.byteplus.com/docs/byteplus-media-live/119943#b312d852).
