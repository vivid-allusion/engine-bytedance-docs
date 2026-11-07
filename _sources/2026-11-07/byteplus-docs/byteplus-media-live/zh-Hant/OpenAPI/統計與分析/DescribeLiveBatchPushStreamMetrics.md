---
title: "DescribeLiveBatchPushStreamMetrics"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelivebatchpushstreammetrics-2023-zh-TW"
---

調用 `DescribeLiveBatchPushStreamMetrics` API，可查詢某個推流域名下的一條或多條流的推流統計數據，包括幀率、碼率、展示時間戳（PTS）等。你可以利用這些統計數據來監控推流會話的健康狀態。你可以查詢已刪除域名的數據。

<span id="Requirements"></span>
## 需求


* 限制：支持查詢已刪除域名產生的歷史推流數據。

* 頻率限制：每個帳號每秒最多 30 次查詢。

* 數據延遲：30 秒。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=DescribeLiveBatchPushStreamMetrics&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 必須同時傳入通用參數和 API 專屬參數。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`DescribeLiveBatchPushStreamMetrics` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。當前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Domain |String |是 |`push.example.com` |推流域名。你可以調用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或在 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面獲取要查詢的推流域名。 |
|App |String |否 |`live` |直播流 URL 中的 AppName 欄位。可包含大寫字母（A\-Z）、小寫字母（a\-z）、數字（0\-9）、底線（_）、連字號（\-）及句點（.），長度為 1~30 個字元。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">查詢指定直播流的監控數據時，App 與 Stream 需同時指定。</div><br> |
|Stream |String |否 |`example_stream` |直播流 URL 中的 StreamName 欄位。可包含大寫字母（A\-Z）、小寫字母（a\-z）、數字（0\-9）、底線（_）、連字號（\-）及句點（.），長度為 1~100 個字元。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">查詢指定直播流的監控數據時，App 與 Stream 需同時指定。</div><br> |
|StartTime |String |是 |`2021-08-16T00:00:00Z` |查詢範圍的開始時間，需為 RFC 3339 格式，精確到秒。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">單次查詢的最大時間跨度為 24 小時，歷史查詢時間範圍為 366 天；</div><br> |
|EndTime |String |是 |`2021-08-16T00:01:59Z` |查詢範圍的結束時間，需為 RFC 3339 格式，精確到秒。 |
|Aggregation |Integer |否 |`5` |回傳數據的時間粒度，單位為秒。有效值包括：<br><br><br>* `5`<br><br>* `30`<br><br>* `60`（預設值） |
|AggType |String |否 |`max` |聚合演算法，數據聚合時間粒度內動態指標的值及含義如下。<br><br><br>* `max`：（預設值）計算聚合時間粒度內的最大值；<br><br>* `avg`：計算聚合時間粒度內的平均值。 |


<span id="Response parameters"></span>
## 回應參數

有關 API 專屬回應參數，請參見下表。更多詳情請參考 [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 章節。


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Domain |String |`push.example.com` |推流域名。 |
|App |String |`live` |直播流 URL 中的 AppName 欄位。 |
|Stream |String |`example_stream` |直播流 URL 中的 StreamName 欄位。 |
|StartTime |String |`2021-08-16T00:00:00Z` |查詢範圍的起始時間，採用 RFC 3339 格式，精確到秒。 |
|EndTime |String |`2021-08-16T00:01:59Z` |查詢範圍的結束時間，採用 RFC 3339 格式，精確到秒。 |
|Aggregation |Integer |`5` |返回資料的時間粒度，單位為秒。有效值包括：<br><br><br>* `5`<br><br>* `30`<br><br>* `60`（預設值） |
|StreamMetricList |[StreamMetricList](https://docs.byteplus.com/en/docs/24/107417#streammetriclist) 陣列 |`-` |依指定時間粒度彙總的監控資料。 |
|AggType |String |`max` |彙總演算法，資料彙總時間粒度內動態指標的值及意義如下。<br><br><br>* `max`：（預設值）計算彙總時間粒度內的最大值；<br><br>* `avg`：計算彙總時間粒度內的平均值。 |


<span id="streammetriclist"></span>
### StreamMetricList


|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Domain |String |`push.example.com` |推流的網域名稱。 |
|App |String |`live` |直播串流 URL 中的 AppName 欄位。 |
|Stream |String |`example_stream` |直播串流 URL 中的 StreamName 欄位。 |
|MetricList |[MetricList](https://docs.byteplus.com/en/docs/24/107417#metriclist) 陣列 |`-` |依指定時間粒度彙總的監控資料。 |
|SessionID |String |`1961227fe2ab4da7a3f28` |單次推流的唯一 ID。 |


<span id="metriclist"></span>
### MetricList


|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|TimeStamp |String |`2022-04-13T00:00:00+08:00` |按時間粒度彙總資料時，每個時間粒度的起始時間，採用 RFC3339 UTC 時間格式，精確到秒。 |
|Bitrate |Float |`20` |彙總演算法取得的資料彙總時間粒度內的視訊位元率，單位為 kbps。 |
|Framerate |Float |`20` |彙總演算法取得的資料彙總時間粒度內的視訊幀率，單位為 fps。 |
|AudioFramerate |Float |`20` |彙總演算法取得的資料彙總時間粒度內的音訊幀率（每秒傳輸的音訊資料包數）。 |
|AudioBitrate |Float |`20` |彙總演算法取得的資料彙總時間粒度內的音訊位元率，單位為 kbps。 |
|AudioPts |Double |`9558439` |目前資料彙總時間粒度內最後一個音訊幀的顯示時間戳（PTS），單位為毫秒。 |
|VideoPts |Double |`9558438` |目前資料彙總時間粒度內最後一個視訊幀的顯示時間戳（PTS），單位為毫秒。 |
|PtsDelta |Float |`1` |彙總演算法取得的目前資料彙總時間粒度內所有音訊與視訊幀的顯示時間戳差異，即所有 Audio PTS 與 Video PTS 值的最大差異，單位為毫秒。 |
|AudioFrameGap |Float |`20` |彙總演算法取得的目前資料彙總時間粒度內相鄰音訊幀的顯示時間戳差異，單位為毫秒。 |
|VideoFrameGap |Float |`20` |彙總演算法取得的目前資料彙總時間粒度內相鄰視訊幀的顯示時間戳差異，單位為毫秒。 |
|StreamBeginTime |Long |`1723726121000` |推流起始時間，以 Unix 時間戳表示，單位為毫秒。 |
|FirstFrameTime |Integer |`10` |推流連線建立至收到第一幀的耗時，單位為毫秒。 |
|ClientIp |String |`127.0.0.1` |推流客戶端的 IP 位址。 |
|ServerIp |String |`127.0.0.1` |推流伺服器的 IP 位址。 |
|Resolution |String |`1280x720` |推流畫面解析度。 |
|VCodec |String |`H264` |視訊編碼器。 |
|ACodec |String |`AAC` |音訊編碼器。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveBatchPushStreamMetrics&Version=2023-01-01
{
    "Domain": "push.example.com",
    "App": "live",
    "Stream": "example_stream",
    "StartTime": "2021-08-16T00:00:00Z",
    "EndTime": "2021-08-16T00:01:59Z",
    "Aggregation": 5,
    "AggType": "max"
}
```


<span id="Sample response"></span>
### 回應範例

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeLiveBatchPushStreamMetrics",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Domain": "push.example.com",
        "App": "live",
        "Stream": "example_stream",
        "StartTime": "2021-08-16T00:00:00Z",
        "EndTime": "2021-08-16T00:01:59Z",
        "Aggregation": 5,
        "StreamMetricList": [
            {
                "Domain": "push.example.com",
                "App": "live",
                "Stream": "example_stream",
                "MetricList": [
                    {
                        "TimeStamp": "2022-04-13T00:00:00Z",
                        "Bitrate": 20,
                        "Framerate": 20,
                        "AudioFramerate": 20,
                        "AudioBitrate": 20,
                        "AudioPts": 9558439,
                        "VideoPts": 9558438,
                        "PtsDelta": 1,
                        "AudioFrameGap": 20,
                        "VideoFrameGap": 20,
                        "FirstFrameTime": 10,
                        "ClientIp": "127.0.0.1",
                        "ServerIp": "127.0.0.1",
                        "Resolution": "1280x720",
                        "StreamBeginTime": 1723726121000,
                        "VCodec": "H264",
                        "ACodec": "AAC"
                    }
                ],
                "SessionID": "1961227fe2ab4da7a3f28"
            }
        ],
        "AggType": "max"
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為本操作相關的錯誤碼。其他錯誤碼請參見 [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**Status Code** |**Error Code** |**錯誤訊息** |**說明** |
|---|---|---|---|
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考[請求參數](https://docs.byteplus.com/en/docs/24/107417#request-parameters)說明進行檢查。 |
|403 |RequestForbidden |*  |因目前帳戶下沒有請求的資源（資源包括域名空間、域名、應用名稱、配置及憑證），請求被拒絕。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡技術支援](https://console.byteplus.com/workorder/create)。 |
