---
title: "DescribeLiveStorageSpaceData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describelivestoragespacedata-zh-TW"
---

調用 `DescribeLiveStorageSpaceData` API，以查詢指定時間範圍內直播時移功能每日的儲存空間使用情況。

<span id="Requirements"></span>
## 需求


* 頻率限制：每個帳戶每秒最多 100 次查詢

* 資料延遲：每日 8:00 AM 後可查詢前一天的資料。

* 資料度量：儲存容量資料以二進位 1024 倍數計算，例如 1 GB = 1024 MB。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=DescribeLiveStorageSpaceData&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 必須同時帶上 [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) 及 API 專屬參數。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`DescribeLiveStorageSpaceData` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Aggregation |Integer |否 |`86400` |時間粒度參數，以秒為單位，支援設為 86400，代表一天的時間間隔。單次查詢的時間跨度為 93 天，歷史查詢時間範圍為 366 天。 |
|StartTime |String |是 |`2022-02-11T00:00:00Z` |查詢範圍的起始時間，採 RFC 3339 格式，精確到秒。 |
|EndTime |String |是 |`2022-02-17T23:59:59Z` |查詢範圍的結束時間，採 RFC 3339 格式，精確到秒。 |
|Buckets |Array of String |否 |`["example"]` |桶列表，若未指定，預設為查詢帳戶下所有儲存桶。 |


<span id="Response parameters"></span>
## 回應參數

如需唯一的 API 專屬回應參數，請參閱下表。更多細節請參考 [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 章節。


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Buckets |Array of String |`["example"]` |桶列表。 |
|StartTime |String |`2022-02-16T00:00:00Z` |查詢範圍的起始時間，採 RFC 3339 格式，精確到秒。 |
|EndTime |String |`2022-02-17T23:59:59Z` |查詢範圍的結束時間，採 RFC 3339 格式，精確到秒。 |
|Aggregation |Boolean |`86400` |資料粒度，以秒為單位。 |
|StorageDataList |Array of [StorageDataList](https://docs.byteplus.com/en/docs/24/107338#storagedatalist) |`-` |直播時移儲存資料。 |


<span id="storagedatalist"></span>
### StorageDataList


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|TimeStamp |String |`2022-02-16T00:00:00Z` |時間戳，預設為每日結束時間。例如，回傳 2022\-02\-16T00:00:00Z 表示該時刻的儲存用量作為 2 月 16 日的計費金額。 |
|Storage |Float |`4503380.1` |直播時移儲存用量，以 GB 為單位。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveStorageSpaceData&Version=2023-01-01
{
    "Aggregation": 86400,
    "EndTime": "2022-02-17T23:59:59Z",
    "StartTime": "2022-02-11T00:00:00Z",
    "Buckets": [
        "example"
    ]
}
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "20180604110420010010****",
        "Action": "DescribeLiveStorageSpaceData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Buckets": [
            "example"
        ],
        "StartTime": "2022-02-16T00:00:00Z",
        "EndTime": "2022-02-17T23:59:59Z",
        "TimeShiftDataList": [
            {
                "TimeStamp": "2022-02-16T00:00:00Z",
                "Storage": 4503380
            },
            {
                "TimeStamp": "2022-02-16T00:05:00Z",
                "Storage": 4503380
            }
        ]
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為與本操作相關的錯誤碼。其他錯誤碼請參閱 [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**Status Code** |**Error Code** |**Error Message** |**說明** |
|---|---|---|---|
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考 [Request Parameters](https://docs.byteplus.com/en/docs/24/107338#request-parameters) 說明進行檢查。 |
|403 |RequestForbidden |*  |請求被拒絕，因為當前帳戶下無請求資源（資源包括域名空間、域名、應用名稱、配置及憑證）。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請 [contact support](https://console.byteplus.com/workorder/create)。 |
