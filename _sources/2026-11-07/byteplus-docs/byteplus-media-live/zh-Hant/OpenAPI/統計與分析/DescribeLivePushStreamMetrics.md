---
title: "DescribeLivePushStreamMetrics"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describelivepushstreammetrics-zh-TW"
---

調用 `DescribeLivePushStreamMetrics` API，以查詢指定時間範圍內單一推流的監控數據，例如音視頻幀率和碼率，評估直播流的健康狀態。

<span id="Requirements"></span>
## 需求


* 限制：支持查詢由特定域名（包含已刪除域名）產生的歷史推流數據。

* 頻率限制：每個帳戶每秒最多 30 次查詢

* 數據延遲：30 秒


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=DescribeLivePushStreamMetrics&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 必須帶上 [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)，以及 API 專屬參數。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`DescribeLivePushStreamMetrics` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Domain |String |是 |`push.example.com` |推流域名。你可以調用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail) API，或在 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面查看用於直播推流的域名。 |
|App |String |是 |`live` |直播流地址中的 `AppName` 欄位。可包含大寫及小寫字母（A\-Z, a\-z）、數字（0\-9）、底線（_）、連字號（\-）及點（.），長度為 1 到 30 字元。 |
|Stream |String |是 |`example_stream` |直播流地址中的 `StreamName` 欄位。可包含大寫及小寫字母（A\-Z, a\-z）、數字（0\-9）、底線（_）、連字號（\-）及點（.），長度為 1 到 100 字元。 |
|StartTime |String |是 |`2021-08-16T00:00:00Z` |查詢範圍的起始時間，格式為 RFC 3339，精確到秒。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">單次查詢的最大時間跨度為 1 天，最大歷史查詢範圍為 366 天。</div><br> |
|EndTime |String |是 |`2021-04-14T00:00:00Z` |查詢範圍的結束時間，格式為 RFC 3339，精確到秒。 |
|Aggregation |Integer |否 |`5` |數據聚合粒度（以秒為單位），支持以下粒度選項：<br><br><br>* `5`：5 秒；<br><br>* `30`：（預設）30 秒。 |


<span id="Response parameters"></span>
## 回應參數

專屬於 API 的回應參數請參見下表。更多詳情請參考 [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 章節。


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Domain |String |`example.com` |推流域名。 |
|App |String |`live` |直播流 URL 中的 AppName 欄位。 |
|Stream |String |`example_stream` |直播流 URL 中的 StreamName 欄位。 |
|StartTime |String |`2021-08-16T00:00:00Z` |查詢範圍的起始時間，格式為 RFC 3339，精確到秒。 |
|EndTime |String |`2021-08-16T00:00:00Z` |查詢範圍的結束時間，格式為 RFC 3339，精確到秒。 |
|Aggregation |Integer |`5` |數據聚合粒度（以秒為單位），支持以下粒度選項：<br><br><br>* `5`：5 秒；<br><br>* `30`：30 秒。 |
|MetricList |[MetricList](https://docs.byteplus.com/en/docs/24/107442#metriclist) 陣列 |`-` |所有粒度層級的數據。 |


<span id="metriclist"></span>
### MetricList


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|TimeStamp |String |`2022-04-13T00:00:00Z` |按時間粒度聚合數據時，每個粒度的起始時間，格式為 RFC3339 UTC 時間，精確到秒。 |
|Bitrate |Float |`20` |當前資料彙總時間粒度內的最大視訊位元率，單位為 kbps。 |
|幀率 |浮點數 |`20` |當前資料彙總時間粒度內的最大視訊幀率，單位為 fps。 |
|音訊幀率 |浮點數 |`20` |當前資料彙總時間粒度內的最大音訊幀率，單位為 fps。 |
|音訊位元率 |浮點數 |`20` |當前資料彙總時間粒度內的最大音訊位元率，單位為 kbps。 |
|音訊 PTS |雙精度 |`9558439` |當前資料彙總時間粒度內最後一個音訊幀的呈現時間戳記 (PTS)，單位為毫秒。 |
|視訊 PTS |雙精度 |`9558430` |當前資料彙總時間粒度內最後一個視訊幀的呈現時間戳記 (PTS)，單位為毫秒。 |
|PTS 差值 |浮點數 |`9` |當前資料彙總時間粒度內所有音訊與視訊幀的顯示時間戳記最大差值，即所有音訊 PTS 與視訊 PTS 的最大差異，單位為毫秒。 |
|音訊幀間隔 |浮點數 |`20` |當前資料彙總時間粒度內相鄰音訊幀的顯示時間戳記最大差值，單位為毫秒。 |
|視訊幀間隔 |浮點數 |`20` |當前資料彙總時間粒度內相鄰視訊幀的顯示時間戳記最大差值，單位為毫秒。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://open.byteplusapi.com/?Action=DescribeLivePushStreamMetrics&Version=2023-01-01
{
    "Domain": "push.example.com",
    "App": "live",
    "Stream": "example_stream",
    "StartTime": "2021-08-16T00:00:00Z",
    "EndTime": "2021-04-14T00:00:00Z",
    "Aggregation": 5
}
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeLivePushStreamMetrics",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Domain": "example.com",
        "App": "live",
        "Stream": "example_stream",
        "StartTime": "2021-08-16T00:00:00Z",
        "EndTime": "2021-08-16T00:00:00Z",
        "Aggregation": 5,
        "MetricList": [
            {
                "TimeStamp": "2022-04-13T00:00:00Z",
                "Bitrate": 20,
                "Framerate": 20,
                "AudioFramerate": 20,
                "AudioBitrate": 20,
                "AudioPts": 9558439,
                "VideoPts": 9558430,
                "PtsDelta": 9,
                "AudioFrameGap": 20,
                "VideoFrameGap": 20
            }
        ]
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為本操作相關的錯誤碼。其他錯誤碼請參見 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**描述** |
|---|---|---|---|
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參閱[請求參數](https://docs.byteplus.com/en/docs/24/107442#request-parameters)說明以進行檢查。 |
|403 |RequestForbidden |*  |因當前帳戶下無請求資源（資源包括網域名稱空間、網域名稱、應用名稱、配置及憑證），請求被拒絕。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
