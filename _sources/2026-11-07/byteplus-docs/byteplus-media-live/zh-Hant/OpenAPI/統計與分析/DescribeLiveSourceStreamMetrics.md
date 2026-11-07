---
title: "DescribeLiveSourceStreamMetrics"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describelivesourcestreammetrics-zh-TW"
---

調用 `DescribeLiveSourceStreamMetrics` API，在指定時間範圍內查詢單一路源流的監控數據，例如音視頻幀率和碼率，以評估該路源流的健康狀態。

<span id="Requirements"></span>
## 需求


* 限制：支援查詢指定域名（包含已刪除域名）下路源流的歷史監控數據。

* 頻率限制：每個帳號每秒最多 30 次查詢

* 數據延遲：30 秒


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=DescribeLiveSourceStreamMetrics&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了需傳入各自的專屬參數外，還必須帶上 [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`DescribeLiveSourceStreamMetrics` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。當前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Domain |String |是 |`pull.example.com` |拉流域名。你可以調用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail) API，或前往 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面，查看用於直播拉流的域名。 |
|App |String |是 |`live` |直播流地址中 `AppName` 欄位的值。可由大寫及小寫字母（A\-Z, a\-z）、數字（0\-9）、底線（_）、連字號（\-）及句點（.）組成，長度為 1 至 30 個字元。 |
|Stream |String |是 |`example_stream` |直播流地址中的 `StreamName` 欄位。可由大寫及小寫字母（A\-Z, a\-z）、數字（0\-9）、底線（_）、連字號（\-）及句點（.）組成，長度為 1 至 100 個字元。 |
|StartTime |String |是 |`2021-08-16T00:00:00Z` |查詢範圍的開始時間，需使用 RFC 3339 格式，精確到秒。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">單次查詢的最大時間跨度為 1 天，最大歷史查詢範圍為 366 天。</div><br> |
|EndTime |String |是 |`2021-08-16T00:01:59Z` |查詢範圍的結束時間，需使用 RFC 3339 格式，精確到秒。 |
|Aggregation |Integer |否 |`30` |數據聚合的粒度，單位為秒，目前僅支援 `30` 秒的聚合間隔。 |


<span id="Response parameters"></span>
## 回應參數

專屬於本 API 的回應參數請參見下表。更多細節請參考 [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 章節。


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Domain |String |`pull.example.com` |拉流域名。 |
|App |String |`live` |直播流 URL 中的 AppName 欄位。 |
|Stream |String |`example_stream` |直播流 URL 中的 StreamName 欄位。 |
|StartTime |String |`2021-08-16T00:00:00Z` |查詢範圍的開始時間，需使用 RFC 3339 格式，精確到秒。 |
|EndTime |String |`2021-08-16T00:01:59Z` |查詢範圍的結束時間，需使用 RFC 3339 格式，精確到秒。 |
|Aggregation |Integer |`30` |數據粒度，單位為秒。 |
|MetricList |[MetricList](https://docs.byteplus.com/en/docs/24/107408#metriclist) 陣列 |`-` |所有粒度層級的數據。 |


<span id="metriclist"></span>
### MetricList


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|TimeStamp |String |`2022-04-13T00:00:00Z` |當以時間粒度聚合數據時，每個粒度的開始時間，格式為 RFC3339 UTC 時間，精確到秒。 |
|Bitrate |Float |`20` |目前資料彙總時間粒度內的最大視訊位元率，單位為 kbps。 |
|Framerate |Float |`20` |目前資料彙總時間粒度內的最大視訊幀率，單位為 fps。 |
|AudioFramerate |Float |`20` |目前資料彙總時間粒度內的最大音訊幀率，單位為 fps。 |
|AudioBitrate |Float |`20` |目前資料彙總時間粒度內的最大音訊位元率，單位為 kbps。 |
|AudioPts |Double |`1651831909` |目前資料彙總時間粒度內最後一個音訊幀的呈現時間戳記（PTS），單位為毫秒。 |
|VideoPts |Double |`1651831910` |目前資料彙總時間粒度內最後一個視訊幀的呈現時間戳記（PTS），單位為毫秒。 |
|PtsDelta |Float |`1` |目前資料彙總時間粒度內所有音訊與視訊幀的顯示時間戳記最大差值，即所有 Audio PTS 與 Video PTS 值的最大差異，單位為毫秒。 |
|AudioFrameGap |Float |`20` |目前資料彙總時間粒度內相鄰音訊幀顯示時間戳記的最大差值，單位為毫秒。 |
|VideoFrameGap |Float |`20` |目前資料彙總時間粒度內相鄰視訊幀顯示時間戳記的最大差值，單位為毫秒。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveSourceStreamMetrics&Version=2023-01-01
{
    "Domain": "pull.example.com",
    "App": "live",
    "Stream": "example_stream",
    "StartTime": "2021-08-16T00:00:00Z",
    "EndTime": "2021-08-16T00:01:59Z",
    "Aggregation": 30
}
```


<span id="Sample response"></span>
### 回應範例

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeLiveSourceStreamMetrics",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Domain": "pull.example.com",
        "App": "live",
        "Stream": "example_stream",
        "StartTime": "2021-08-16T00:00:00Z",
        "EndTime": "2021-08-16T00:01:59Z",
        "Aggregation": 30,
        "MetricList": [
            {
                "TimeStamp": "2022-04-13T00:00:00Z",
                "Bitrate": 20,
                "Framerate": 20,
                "AudioFramerate": 20,
                "AudioBitrate": 20,
                "AudioPts": 1651831909,
                "VideoPts": 1651831910,
                "PtsDelta": 1,
                "AudioFrameGap": 20,
                "VideoFrameGap": 20
            }
        ]
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為本操作相關的錯誤碼。其他錯誤碼請參見 [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**Status Code** |**Error Code** |**Error Message** |**Description** |
|---|---|---|---|
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參閱[請求參數](https://docs.byteplus.com/en/docs/24/107408#request-parameters)說明以進行檢查。 |
|403 |RequestForbidden |*  |因目前帳戶下無請求資源（資源包括網域名稱空間、網域名稱、App 名稱、配置與憑證），故請求被拒絕。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
