---
title: "DescribeLiveBatchSourceStreamMetrics"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describelivebatchsourcestreammetrics-zh-TW"
---

獲取監控數據，例如音訊與視訊的幀率和碼率，針對特定時間範圍內指定域名下全部或特定的源站拉流流。你可以利用監控數據評估源站拉流的健康狀況。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">你可以獲取已刪除域名產生的歷史源站拉流數據。</div>


<span id="Requirements"></span>
## 需求


* 頻率限制：每個帳戶每秒最多 30 次請求

* 數據延遲：15 分鐘


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=DescribeLiveBatchSourceStreamMetrics&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 必須同時帶上[通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)和 API 特定參數。

<span id="Query"></span>
### 查詢


|**參數** |**數據類型** |**是否必填** |**示例值** |**描述** |
|---|---|---|---|---|
|Action |String |是 |`DescribeLiveBatchSourceStreamMetrics` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。當前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**數據類型** |**是否必填** |**示例值** |**描述** |
|---|---|---|---|---|
|Domain |String |是 |`pull.example.com` |拉流域名。你可以調用[ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023)或在BytePlus MediaLive 控制台的**Domains**頁面查詢源站拉流所用的域名。 |
|App |String |否 |`live` |App 名稱。參數值必須與直播流地址中的`AppName`字段一致。參數值必須為 1\-30 個字符，且僅包含以下字符：<br><br><br>* 小寫字母（a\-z）<br><br>* 大寫字母（A\-Z）<br><br>* 數字（0\-9）<br><br>* 連字符（\-）<br><br>* 底線（_）<br><br>* 句點（.）<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">若需獲取特定源站拉流的監控數據，該參數為必填，且必須同時傳入<code>Stream</code>參數。</div><br> |
|Stream |String |否 |`example_stream` |流名稱。參數值必須與直播流地址中的`StreamName`字段一致。參數值必須為 1\-100 個字符，且僅包含以下字符：<br><br><br>* 小寫字母（a\-z）<br><br>* 大寫字母（A\-Z）<br><br>* 數字（0\-9）<br><br>* 連字符（\-）<br><br>* 底線（_）<br><br>* 句點（.）<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">若需獲取特定源站拉流的監控數據，該參數為必填，且必須同時傳入<code>App</code>參數。</div><br> |
|StartTime |String |是 |`2021-08-16T00:00:00+08:00` |查詢範圍的開始時間（UTC 時間，RFC 3339 格式，精確到秒）。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">最大歷史查詢範圍為 366 天。單次查詢最大時間跨度為 1 天。</div><br> |
|EndTime |String |是 |`2021-08-16T00:01:59+08:00` |查詢範圍的結束時間（UTC 時間，RFC 3339 格式，精確到秒）。 |
|Aggregation |Integer |否 |`30` |數據聚合的時間粒度，單位為秒。預設值：`60`。有效值：<br><br><br>* `30`：30 秒。<br><br>* `60`：1 分鐘。 |
|AggType |String |否 |`max` |數據聚合時間粒度內動態指標的聚合算法。預設值：`max`。有效值：<br><br><br>* `max`：計算聚合時間粒度內的最大值。<br><br>* `avg`：計算聚合時間粒度內的平均值。 |


<span id="Response parameters"></span>
## 響應參數

關於唯一的 API 特定響應參數，請參見下表。更多詳情請參考[請求響應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)部分。


|**參數** |**數據類型** |**範例值** |**說明** |
|---|---|---|---|
|Domain |String |`pull.example.com` |拉流的網域名稱。 |
|App |String |`live` |App 名稱。 |
|Stream |String |`example_stream` |串流名稱。 |
|StartTime |String |`2021-04-13T00:00:00+08:00` |查詢區間的起始時間（RFC 3339 格式的 UTC 時間，精確到秒）。 |
|EndTime |String |`2021-04-14T00:00:00+08:00` |查詢區間的結束時間（RFC 3339 格式的 UTC 時間，精確到秒）。 |
|Aggregation |Integer |`30` |資料彙總的時間粒度，單位為秒。有效值：<br><br><br>* `30`：30 秒。<br><br>* `60`：1 分鐘。 |
|StreamMetricList |[StreamMetricList](https://docs.byteplus.com/en/docs/24/107422#streammetriclist) 陣列 |`-` |源拉流的串流資訊。 |
|AggType |String |`max` |資料彙總時間粒度內動態指標的彙總演算法。有效值：<br><br><br>* `max`：計算彙總時間粒度內的最大值。<br><br>* `avg`：計算彙總時間粒度內的平均值。 |


<span id="streammetriclist"></span>
### StreamMetricList


|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Domain |String |`pull.example.com` |拉流的網域名稱。 |
|App |String |`live` |App 名稱。 |
|Stream |String |`example_stream` |串流名稱。 |
|MetricList |[MetricList](https://docs.byteplus.com/en/docs/24/107422#metriclist) 陣列 |`-` |依指定時間粒度彙總的監控資料。 |


<span id="metriclist"></span>
### MetricList


|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|TimeStamp |String |`2022-04-13T00:00:00+08:00` |依時間粒度彙總資料時，每個粒度的起始時間（RFC 3339 格式的 UTC 時間，精確到秒）。 |
|Bitrate |Float |`20` |在目前資料彙總時間粒度內，透過彙總演算法取得的視訊碼率，單位為 kbps。 |
|Framerate |Float |`20` |在目前資料彙總時間粒度內，透過彙總演算法取得的視訊幀率，單位為 fps。 |
|AudioFramerate |Float |`20` |在目前資料彙總時間粒度內，透過彙總演算法取得的音訊幀率，單位為 fps。 |
|AudioBitrate |Float |`20` |在目前資料彙總時間粒度內，透過彙總演算法取得的音訊碼率，單位為 kbps。 |
|AudioPts |Double |`1651831909` |目前資料彙總時間粒度內，最後一個音訊幀的呈現時間戳（PTS），單位為毫秒。 |
|VideoPts |Double |`1651831910` |目前資料彙總時間粒度內，最後一個視訊幀的 PTS，單位為毫秒。 |
|PtsDelta |Float |`1` |在目前資料彙總時間粒度內，透過彙總演算法取得的音訊與視訊幀 PTS 差值的最大值或平均值，即所有 `AudioPts` 與 `VideoPts` 差值的最大值或平均值，單位為毫秒。 |
|AudioFrameGap |Float |`20` |在目前資料彙總時間粒度內，透過彙總演算法取得的相鄰音訊幀 PTS 最大差值的平均值，單位為毫秒。 |
|VideoFrameGap |Float |`20` |在目前資料彙總時間粒度內，透過彙總演算法取得的相鄰視訊幀 PTS 差值的最大值或平均值，單位為毫秒。 |


<span id="Samples"></span>
## Samples

<span id="Sample request"></span>
### 示例請求

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveBatchSourceStreamMetrics&Version=2023-01-01
{
    "Domain": "pull.example.com",
    "App": "live",
    "Stream": "example_stream",
    "StartTime": "2021-08-16T00:00:00+08:00",
    "EndTime": "2021-08-16T00:01:59+08:00",
    "Aggregation": 30,
    "AggType": "max"
}
```


<span id="Sample response"></span>
### 示例響應

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeLiveBatchSourceStreamMetrics",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Domain": "pull.example.com",
        "App": "live",
        "Stream": "example_stream",
        "StartTime": "2021-04-13T00:00:00+08:00",
        "EndTime": "2021-04-14T00:00:00+08:00",
        "Aggregation": 30,
        "StreamMetricList": [
            {
                "Domain": "pull.example.com",
                "App": "live",
                "Stream": "example_stream",
                "MetricList": [
                    {
                        "TimeStamp": "2022-04-13T00:00:00+08:00",
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
        ],
        "AggType": "max"
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下是與本操作相關的錯誤碼。其他錯誤碼請參見[BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**Status Code** |**Error Code** |**Error Message** |**Description** |
|---|---|---|---|
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考 [request parameters](https://docs.byteplus.com/en/docs/24/107422#request-parameters) 說明進行驗證。 |
|403 |RequestForbidden |*  |因目前帳戶下無請求資源（資源包括網域命名空間、網域名稱、App、配置範本及憑證），請求被拒絕。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請 [聯絡客服](https://console.byteplus.com/workorder/create)。 |
