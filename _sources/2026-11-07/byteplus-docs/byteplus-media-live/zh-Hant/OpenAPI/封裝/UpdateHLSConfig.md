---
title: "UpdateHLSConfig"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/updatehlsconfig-zh-TW"
---

呼叫 `UpdateHLSConfig` API，以新增或更新特定網域空間的 HLS 設定，包括分段大小與分段數量，有效降低延遲並提升直播相容性。在 HTTP Live Streaming（HLS）及低延遲 HLS（LL\-HLS）中，直播串流會被切分為 Transport Stream（TS）。每個 TS 都有對應的 URL，使用 HLS 協議進行直播拉流時，地址會持續變動。

<span id="Requirements"></span>
## 需求


* 先決條件：需要支援 LL\-HLS 的播放器。

* 限制：

   * HLS/LL\-HLS 封裝適用於推流、使用 FLV 和 Real\-Time Messaging Protocol（RTMP）進行源站拉流，以及使用 HLS 進行拉流。請注意，該功能不適用於使用 HLS 進行源站拉流。

   * HLS/LL\-HLS 封裝設定不僅適用於此網域下的串流，也適用於同一網域空間（Vhost）下其他關聯網域的串流。

   * HLS/LL\-HLS 封裝設定不適用於啟用 [HLS-ABR](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-configuring-an-hls-abr-task) 功能的應用。

   * 封裝設定於 3 至 5 分鐘內生效。

      限制：適用於推流、使用 HLS 拉流，以及使用 FLV 和 Real\-Time Messaging Protocol（RTMP）進行源站拉流。但不適用於使用 HLS 進行源站拉流。

* 頻率限制：每個帳戶每秒最多 10 次查詢。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=UpdateHLSConfig&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 必須同時帶上 [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) 和 API 專屬參數來呼叫。

<span id="Query"></span>
### 查詢


|**參數** |**資料型態** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`UpdateHLSConfig` |API 操作。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型態** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |網域空間。你可以呼叫 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或在 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面查詢該網域所屬的網域空間。 |
|App |String |否 |`live` |直播串流 URL 中的 AppName 欄位。若未指定，設定將適用於所有 AppName。可包含大寫字母（A\-Z）、小寫字母（a\-z）、數字（0\-9）、底線（_）、連字號（\-）及句點（.），長度為 1 至 30 字元。 |
|Interval |Float |否 |`3` |HLS 分段時長範圍為 1 至 60 秒。<br><br>預設值為 3。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">建議直播串流的 GOP（Group of Pictures）大小保持穩定，且分段時長等於或為 GOP 大小的整數倍。</div><br> |
|PlaylistLength |Integer |否 |`3` |m3u8 播放清單中的媒體分段數量。預設值為 3。 |
|FirstPlaylistLength |Integer |否 |`2` |初始播放清單包含的媒體分段數量。你可以輸入 `3` 到 `10` 的整數。預設值為 `2`。 |
|PartTargetDuration |Float |否 |`1` |每個媒體分段拆分出的部分分段時長。<br><br><br>* 以秒為單位。<br><br>* 預設值為 `1`。<br><br>* `0` 表示停用低延遲 HLS。 |
|InsertPDT |Boolean |否 |`true` |是否在播放檔案中插入 PDT 時間標籤，預設為不插入，具體值及其含義如下。<br><br><br>* `true`：插入；<br><br>* `false`：不插入。 |
|PDTInterval |浮點數 |否 |`3` |在播放檔案中插入 PDT（#EXT\-X\-PROGRAM\-DATE\-TIME）時間標籤的間隔，單位為秒，取值範圍為 [0,3600]，預設值為 0。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">若 PDT 間隔設為 0 或小於分段時長，則每個分段都會插入一個 PDT 標籤。</div><br> |


<span id="Response parameters"></span>
## 回應參數

此 API 僅在回應中返回 [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://open.byteplusapi.com/?Action=UpdateHLSConfig&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "App": "live",
    "Interval": 2.6,
    "PlaylistLength": 6,
    "FirstPlaylistLength": 4,
    "PartTargetDuration": 1
}
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "2024041106585435BA3A27F267D68D449F",
        "Action": "UpdateCMAFConfig",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```
