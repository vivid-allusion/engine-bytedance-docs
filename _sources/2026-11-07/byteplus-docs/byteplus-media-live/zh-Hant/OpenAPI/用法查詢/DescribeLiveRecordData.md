---
title: "DescribeLiveRecordData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describeliverecorddata-zh-TW"
---

調用 `DescribeLiveRecordData` API 查詢指定直播域名在指定時間範圍內的錄製用量，包括最大併發錄製數。

<span id="Requirements"></span>
## 需求


* 計費：有關錄製價格，請參見 [錄製計費](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-transcoding_2)。

* 限制：支持查詢已刪除域名產生的錄製用量數據。

* 頻率限制：每個帳號每秒最多 30 次查詢。

* 數據延遲：7 小時。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=DescribeLiveRecordData&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 調用除需傳入 API 專屬參數外，還必須傳入 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**數據類型** |**是否必填** |**示例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`DescribeLiveRecordData` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本號。當前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**數據類型** |**是否必填** |**示例值** |**說明** |
|---|---|---|---|---|
|DomainList |Array of String |否 |`["push.example.com"]` |域名列表。預設為空，表示查詢你 BytePlus MediaLive 下所有域名的帶寬用量數據。你可以調用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail) API 或前往 BytePlus MediaLive 控制台的 [域名](https://console.byteplus.com/live/main/domain/list) 頁面獲取待查詢的域名。 |
|StartTime |String |是 |`2021-04-13T00:00:00Z` |查詢範圍的開始時間，需使用 RFC 3339 格式，精確到秒。 |
|EndTime |String |是 |`2021-04-14T00:00:00Z` |查詢範圍的結束時間，需使用 RFC 3339 格式，精確到秒。 |
|Aggregation |Integer |否 |`300` |數據聚合的粒度，單位為秒，支持以下選項：<br><br><br>* `300`（預設）：5 分鐘。以 5 分鐘為粒度聚合時，單次查詢的最大時間跨度為 31 天，歷史查詢的最大時間範圍為 366 天。<br><br>* `3600`：1 小時。以 1 小時為粒度聚合時，單次查詢的最大時間跨度為 93 天，歷史查詢的最大時間範圍為 366 天。<br><br>* `86400`：1 天。以 1 天為粒度聚合時，單次查詢的最大時間跨度為 93 天，歷史查詢的最大時間範圍為 366 天。 |
|DetailField |Array of String |否 |`["Domain"]` |數據分組維度預設為空，表示不分組。目前僅支持以 `Domain` 為維度進行數據分組。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">僅當 <code>DetailField</code> 參數設為 <code>Domain</code> 且 <code>DomainList</code> 參數包含多個值時，才會以 <code>Domain</code> 維度分組數據。</div><br> |
|App |String |否 |`live` |直播流 URL 中的 AppName 欄位。可包含大寫字母（A\-Z）、小寫字母（a\-z）、數字（0\-9）、底線（_）、連字號（\-）及句點（.），長度為 1 至 30 個字元。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">查詢流粒度數據時，需同時傳入 <code>App</code> 及 <code>Stream</code> 參數。</div><br> |
|Stream |String |否 |`example_stream` |直播流 URL 中的 StreamName 欄位。可包含大寫和小寫字母（A\-Z, a\-z）、數字（0\-9）、底線（_）、連字號（\-）以及句點（.），長度範圍為1至100個字元。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">查詢串流粒度資料時，必須同時提供<code>App</code>和<code>Stream</code>參數。</div><br> |


<span id="Response parameters"></span>
## 響應參數

有關唯一的 API 專屬響應參數，請參見下表。更多詳情請參見 [請求響應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 章節。


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|DomainList |字串陣列 |`["push.example.com"]` |網域名稱列表。 |
|StartTime |字串 |`2021-04-13T00:00:00Z` |查詢範圍的起始時間，採RFC 3339格式，精確到秒。 |
|EndTime |字串 |`2021-04-14T00:00:00Z` |查詢範圍的結束時間，採RFC 3339格式，精確到秒。 |
|Aggregation |整數 |`300` |資料粒度，以秒為單位。 |
|DetailField |字串陣列 |`["Domain"]` |資料拆分維度目前僅限於`Domain`，代表網域名稱。 |
|RecordPeak |整數 |`2` |在目前查詢條件下允許的最大同時錄製串流數。 |
|RecordDataList |[RecordDataList](https://docs.byteplus.com/en/docs/24/107441#recorddatalist)陣列 |`-` |所有時間粒度層級的資料。 |
|RecordDetailDataList |[RecordDetailDataList](https://docs.byteplus.com/en/docs/24/107441#recorddetaildatalist)陣列 |`-` |根據特定維度分類後的資料。 |
|App |字串 |`live` |查詢串流粒度資料時的串流AppName欄位。 |
|Stream |字串 |`example_stream` |查詢串流粒度資料時的串流StreamName欄位。 |


<span id="recorddatalist"></span>
### RecordDataList


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|TimeStamp |字串 |`2022-04-13T00:00:00Z` |以時間粒度聚合資料時，每個時間粒度的起始時間，採RFC3339 UTC時間格式，精確到秒。 |
|Value |整數 |`1` |在目前資料聚合時間粒度內的最大同時錄製串流數。 |


<span id="recorddetaildatalist"></span>
### RecordDetailDataList


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Domain |字串 |`push.example.com` |以網域維度拆分資料時的網域名稱資訊。 |
|RecordPeak |整數 |`2` |以維度拆分資料後，當前維度的最大同時錄製串流數。 |
|RecordDataList |[RecordDataList](https://docs.byteplus.com/en/docs/24/107441#recorddatalist)陣列 |`-` |以維度拆分資料後，當前維度下所有粒度層級的資料。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveRecordData&Version=2023-01-01
{
    "DomainList": [
        "push.example.com"
    ],
    "StartTime": "2021-04-13T00:00:00Z",
    "EndTime": "2021-04-13T00:10:00Z",
    "Aggregation": 300,
    "DetailField": [
        "Domain"
    ]
}
```


<span id="Sample response"></span>
### 響應範例

```json
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100***",
        "Action": "DescribeLiveRecordData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "DomainList": [
            "push.example.com"
        ],
        "StartTime": "2021-04-13T00:00:00Z",
        "EndTime": "2021-04-13T00:10:00Z",
        "Aggregation": 300,
        "DetailField": [
            "Domain"
        ],
        "RecordPeak": 2,
        "RecordDataList": [
            {
                "TimeStamp": "2021-04-13T00:00:00Z",
                "Value": 1
            },
            {
                "TimeStamp": "2021-04-13T00:05:00Z",
                "Value": 2
            }
        ],
        "RecordDetailDataList": [
            {
                "Domain": "push.example.com",
                "RecordPeak": 2,
                "RecordDataList": [
                    {
                        "TimeStamp": "2021-04-13T00:00:00Z",
                        "Value": 1
                    },
                    {
                        "TimeStamp": "2021-04-13T00:05:00Z",
                        "Value": 2
                    }
                ]
            }
        ]
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為本操作相關的錯誤碼。其他錯誤碼請參見 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**說明** |
|---|---|---|---|
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考[Request Parameters](https://docs.byteplus.com/en/docs/24/107441#request-parameters)說明進行檢查。 |
|403 |RequestForbidden |*  |因目前帳戶下無請求資源（資源包括網域名稱空間、網域名稱、App名稱、配置及憑證），請求被拒絕。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
