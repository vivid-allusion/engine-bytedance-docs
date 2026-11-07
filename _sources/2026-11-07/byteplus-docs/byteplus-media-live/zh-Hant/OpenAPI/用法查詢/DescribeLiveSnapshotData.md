---
title: "DescribeLiveSnapshotData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describelivesnapshotdata-zh-TW"
---

調用 `DescribeLiveSnapshotData` API 以檢索指定直播網域在指定時間範圍內由截圖功能產生的快照數量。

<span id="Requirements"></span>
## 需求


* 計費：有關截圖價格，請參閱 [截圖](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-screenshot-capturing)。

* 限制：支援查詢指定網域（包含已刪除網域）下所有直播截圖任務產生的截圖數量。

* 頻率限制：每個帳號每秒 30 次查詢。

* 數據延遲：15 分鐘。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=DescribeLiveSnapshotData&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了需帶入 API 專屬參數外，還必須帶入 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`DescribeLiveSnapshotData` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本號。當前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|DomainList |Array of String |否 |`["push.example.com","push2.example.com"]` |網域清單。預設為空，表示查詢您 BytePlus MediaLive 下所有網域的快照用量數據。您可調用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail) API 或前往 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面獲取待查詢的網域。 |
|StartTime |String |是 |`2021-04-13T00:00:00Z` |查詢範圍的起始時間，需符合 RFC 3339 格式，精確到秒。 |
|EndTime |String |是 |`2021-04-14T00:00:00Z` |查詢範圍的結束時間，需符合 RFC 3339 格式，精確到秒。 |
|Aggregation |Integer |否 |`86400` |數據聚合的粒度，單位為秒，支援以下選項：<br><br><br>* `300`：5 分鐘。以 5 分鐘為粒度聚合時，單次查詢最大時間跨度為 31 天，歷史查詢最大時間範圍為 366 天。<br><br>* `3600`：1 小時。以 1 小時為粒度聚合時，單次查詢最大時間跨度為 93 天，歷史查詢最大時間範圍為 366 天。<br><br>* `86400`（預設）：1 天。以 1 天為粒度聚合時，單次查詢最大時間跨度為 93 天，歷史查詢最大時間範圍為 366 天。 |
|DetailField |Array of String |否 |`["Domain"]` |數據分割維度預設為空，表示不進行數據分割。目前僅支援以 `Domain` 為維度進行數據分割。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">僅當 <code>DetailField</code> 參數設為 <code>Domain</code> 且 <code>DomainList</code> 參數包含多個值時，才會以 <code>Domain</code> 維度進行數據分割。</div><br> |
|App |String |否 |`live` |直播串流 URL 中的 AppName 欄位。可包含大寫字母（A\-Z）、小寫字母（a\-z）、數字（0\-9）、底線（_）、連字號（\-）及句點（.），長度為 1 至 30 個字元。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">查詢串流粒度數據時，需同時傳入 <code>App</code> 與 <code>Stream</code> 參數。</div><br> |
|Stream |String |否 |`example_stream` |直播串流 URL 中的 StreamName 欄位。它可以包含大寫和小寫字母（A\-Z, a\-z）、數字（0\-9）、底線（_）、連字號（\-）以及句點（.），長度範圍為1至100個字元。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">查詢串流粒度資料時，必須同時提供<code>App</code>和<code>Stream</code>參數。</div><br> |


<span id="Response parameters"></span>
## 回應參數

有關 API 專屬回應參數，請參見下表。更多詳情請參閱 [請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 章節。


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|DomainList |字串陣列 |`["push.example.com","push.example.com"]` |網域名稱列表。 |
|StartTime |字串 |`2021-04-13T00:00:00Z` |查詢範圍的起始時間，採RFC 3339格式，精確到秒。 |
|EndTime |字串 |`2021-04-14T00:00:00Z` |查詢範圍的結束時間，採RFC 3339格式，精確到秒。 |
|Aggregation |整數 |`300` |資料粒度，以秒為單位。 |
|DetailField |字串陣列 |`["Domain"]` |資料分割維度目前僅限於`Domain`，代表網域名稱。 |
|Total |整數 |`19503380` |在目前查詢條件下所截取的螢幕截圖總數。 |
|SnapshotDataList |[SnapshotDataList](https://docs.byteplus.com/en/docs/24/107365#snapshotdatalist)陣列 |`-` |所有時間粒度層級的資料。 |
|SnapshotDetailData |[SnapshotDetailData](https://docs.byteplus.com/en/docs/24/107365#snapshotdetaildata)陣列 |`-` |已依維度分割的資料。 |
|App |字串 |`live` |查詢串流粒度資料時的串流AppName欄位。 |
|Stream |字串 |`example_stream` |查詢串流粒度資料時的串流StreamName欄位。 |


<span id="snapshotdatalist"></span>
### SnapshotDataList


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|TimeStamp |字串 |`2022-04-13T00:00:00Z` |依時間粒度聚合資料時，每個時間粒度的起始時間，採RFC3339 UTC時間格式，精確到秒。 |
|Value |整數 |`9503380` |在目前資料聚合時間粒度內所截取的螢幕截圖總數。 |


<span id="snapshotdetaildata"></span>
### SnapshotDetailData


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Domain |字串 |`push.example.com` |依網域維度分割資料時的網域名稱資訊。 |
|Total |整數 |`19503380` |資料依維度分割後，該維度下所截取的螢幕截圖總數。 |
|SnapshotDataList |[SnapshotDataList](https://docs.byteplus.com/en/docs/24/107365#snapshotdatalist)陣列 |`-` |資料依維度分割後，該維度下所有粒度層級的資料。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveSnapshotData&Version=2023-01-01
{
    "DomainList": [
        "push.example.com",
        "push2.example.com"
    ],
    "StartTime": "2022-03-07T00:00:00Z",
    "EndTime": "2022-03-08T00:00:00Z",
    "Aggregation": 86400,
    "DetailField": [
        "Domain"
    ]
}
```


<span id="Sample response"></span>
### 回應範例

```json
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "DescribeLiveSnapshotData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "cn-north-1"
    },
    "Result": {
        "DomainList": [
            "push.example.com",
            "push2.example.com"
        ],
        "StartTime": "2022-03-07T00:00:00Z",
        "EndTime": "2022-03-08T00:00:00Z",
        "Aggregation": 86400,
        "DetailField": [
            "Domain"
        ],
        "Total": 19503380,
        "SnapshotDataList": [
            {
                "TimeStamp": "2022-03-07T00:00:00Z",
                "Value": 9503380
            },
            {
                "TimeStamp": "2022-03-08T00:00:00Z",
                "Value": 9507820
            }
        ],
        "SnapshotDetailData": [
            {
                "Domain": "push.example.com",
                "Total": 19503380,
                "SnapshotDataList": [
                    {
                        "TimeStamp": "2022-03-07T00:00:00Z",
                        "Value": 9503380
                    },
                    {
                        "TimeStamp": "2022-03-08T00:00:00Z",
                        "Value": 9507820
                    }
                ]
            },
            {
                "Domain": "push2.example.com",
                "Total": 19503380,
                "SnapshotDataList": [
                    {
                        "TimeStamp": "2022-03-07T00:00:00Z",
                        "Value": 9503380
                    },
                    {
                        "TimeStamp": "2022-03-08T00:00:00Z",
                        "Value": 9507820
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
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考[Request Parameters](https://docs.byteplus.com/en/docs/24/107365#request-parameters)說明進行檢查。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
