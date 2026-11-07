---
title: "將伺服器時間戳記資料插入 SEI 訊息"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/inserting-server-timestamp-data-into-SEI-messages--zh-TW"
---

為協助您分析直播延遲，BytePlus MediaLive 支援將伺服器時間戳記資料插入 SEI（Supplemental Enhancement Information，補充增強資訊）訊息。為推流網域名稱啟用此功能後，MediaLive 會為該推流網域名稱所屬網域名稱空間下的所有直播流，在 SEI 訊息中插入伺服器時間戳記資料。您可以使用 BytePlus MediaLive Player SDK 或自己的 SEI 解析器計算並分析延遲。

## 前提條件

* 聯絡[技術支援](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)以啟用此功能。

* 推流網域名稱。如需瞭解如何新增推流網域名稱，請參閱[新增網域名稱](https://docs.byteplus.com/docs/byteplus-media-live/docs-domain)。

## 操作步驟

1. 登入 [BytePlus MediaLive 控制台](https://console.byteplus.com/live/main/domain/list)。

2. 在左側導覽窗格中，按一下 **Domains**。

3. 在 **Domains** 頁面上，按一下目標推流網域名稱右側的 **Settings**。

4. 在 **Advanced settings** 索引標籤上，按一下 **Edit**，然後開啟或關閉 **SEI 插入伺服器時間戳記**開關。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/33a1a2a75e554c9faa5edc5b232af63b~tplv-goo7wpa0wc-topic.webp)

   * 開啟：為推流網域名稱所屬網域名稱空間下的所有直播流，將伺服器時間戳記資料插入 SEI 訊息。之後，您可以使用 SEI 訊息分析直播延遲。如需伺服器時間戳記資料的詳細資訊，請參閱 [SEI 訊息中的伺服器時間戳記資料](https://docs.byteplus.com/docs/byteplus-media-live/119943#b312d852)。

   * 關閉：不要將伺服器時間戳記資料插入 SEI 訊息。

   > **說明**

   > 開啟此功能後，MediaLive 在將伺服器時間戳記資料寫入 SEI 訊息時，會使用 `5` 作為 SEI `type` 值。如果您的推流工具或應用程式也會將自訂 SEI 訊息寫入串流，請避免使用相同的 SEI `type` 值。否則，播放器可能會將自訂資料識別為伺服器時間戳記資料。

5. 按一下 **Confirm**。

### SEI 訊息中的伺服器時間戳記資料

開啟 **SEI 插入伺服器時間戳記**開關後，SEI 訊息可包含下列 Unix 時間戳記，單位為毫秒。每個時間戳記記錄串流到達串流路徑中特定 MediaLive 節點的時間。您可以使用這些時間戳記，計算特定維度的直播延遲。

|欄位 |描述 |
|---|---|
|push_edge_ts |串流到達 MediaLive 推流端邊緣節點的時間。 |
|transpush_edge_ts |串流到達 MediaLive 推流端轉發節點的時間。 |
|source_ts |串流到達 MediaLive 源站節點的時間。 |
|trans_src_ts |串流到達 MediaLive 區域源站節點的時間。 |
|transpull_edge_ts |串流到達 MediaLive 二級轉發節點的時間。 |
|pull_edge_ts |串流到達 MediaLive 拉流端邊緣節點的時間。 |
|hls_source_ts |串流到達 MediaLive HLS 分片源站節點的時間。 |
|cmaf_source_ts |串流到達 MediaLive CMAF 分片源站節點的時間。 |

## 後續步驟

開啟 **SEI 插入伺服器時間戳記**開關後，您可以：

* 使用適用於 iOS、Android 和 Web 的 BytePlus MediaLive Player SDK，從 SEI 訊息取得延遲資料。

   * 適用於 iOS 和 Android 的 Player SDK：使用 Android Player SDK 1.52.100.5 或更新版本，或 iOS Player SDK 1.52.100.4\-premium 或更新版本。針對 Android，將 [enableStatisticsCallback](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-keytype#VeLivePlayerConfiguration-enablestatisticscallback) 設為 `true`；針對 iOS，將 [enableStatisticsCallback](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-type-definition#VeLivePlayerConfiguration-enablestatisticscallback) 設為 `YES`。然後，針對 Android，從 [onStatistics](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-callback#VeLivePlayerObserver-onstatistics) 回呼取得延遲統計資料；針對 iOS，從 [onStatistics:statistics:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-callback#VeLivePlayerObserver-onstatistics-statistics) 回呼取得延遲統計資料。

      |欄位 |計算方法 |描述 |
      |---|---|---|
      |delayS2sMs |pull_edge_ts \- push_edge_ts |伺服器到伺服器延遲，單位為毫秒。表示串流從 MediaLive 推流端邊緣節點傳輸到 MediaLive 拉流端邊緣節點所需的時間。當 SEI 訊息不包含串流到達推流端邊緣節點和拉流端邊緣節點時的伺服器時間戳記時，該值為 `-1`。 |
      |delayE2eMs |Player SDK local timestamp when parsing the SEI message \- Broadcast SDK timestamp in the SEI message |端對端延遲，單位為毫秒。表示從 Broadcast SDK 將時間戳記寫入 SEI 訊息，到 Player SDK 在本機解析 SEI 訊息所需的時間。準確計算取決於以 NTP 為基礎的時鐘同步。當 SEI 訊息不包含 Broadcast SDK 寫入的時間戳記時，該值為 `-1`。 |
      |delayS2eMs |Player SDK local timestamp when parsing the SEI message \- push_edge_ts |伺服器到終端延遲，單位為毫秒。表示從串流到達 MediaLive 推流端邊緣節點，到 Player SDK 在本機解析 SEI 訊息所需的時間。準確計算取決於以 NTP 為基礎的時鐘同步。當 SEI 訊息不包含串流到達 MediaLive 推流端邊緣節點時的伺服器時間戳記時，該值為 `-1`。 |

   * 適用於 Web 的 Player SDK：使用 Web Player SDK 2.13.0 或更新版本。對於 RTM 串流，將 [enableSei](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-web-options#rtm) 設為 `true`，並呼叫 [getRTMStats()](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-web-methods-and-properties#veplayerlive-getrtmstats) 以取得延遲統計資料。對於 FLV 串流，呼叫 [getFLVStats()](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-web-methods-and-properties#veplayerlive-getflvstats) 以取得延遲統計資料。

      |欄位 |計算方法 |描述 |
      |---|---|---|
      |delay_s2s |pull_edge_ts \- push_edge_ts |伺服器到伺服器延遲，單位為毫秒。表示串流從 MediaLive 推流端邊緣節點傳輸到 MediaLive 拉流端邊緣節點所需的時間。沒有可用的有效伺服器 SEI 資料時為空。 |
      |delay_s2e |Player SDK local timestamp when parsing the SEI message \- push_edge_ts + local player buffer duration |伺服器到終端延遲，單位為毫秒。表示從串流到達 MediaLive 推流端邊緣節點，到 Web Player SDK 播放對應影格所需的時間。由於 Player SDK 會在播放對應影格前解析 SEI 訊息，因此計算時會包含本機播放器緩衝時間長度。沒有可用的有效伺服器 SEI 資料時為空。 |

* 自行解析 SEI 資料。如果使用自己的 SEI 解析器，您可以解析 SEI 訊息中的伺服器時間戳記資料，並根據業務需求計算延遲。如需 SEI 訊息中的特定時間戳記，請參閱 [SEI 訊息中的伺服器時間戳記資料](https://docs.byteplus.com/docs/byteplus-media-live/119943#b312d852)。
