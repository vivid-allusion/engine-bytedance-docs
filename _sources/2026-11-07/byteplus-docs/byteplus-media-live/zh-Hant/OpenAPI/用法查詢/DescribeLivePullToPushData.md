---
title: "DescribeLivePullToPushData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describelivepulltopushdata-zh-TW"
---

調用 `DescribeLivePullToPushData` API，可查詢指定時間範圍內由群組產生的所有轉推任務的時長用量。

<span id="Requirements"></span>
## 需求


* 計費：有關轉推計費，請參閱 [Relay](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-relay-1)。

* 頻率限制：每個帳號每秒最多 30 次查詢

* 數據延遲：

   * 當聚合粒度為 60 秒時，數據延遲為 5 分鐘；

   * 其他時間粒度下，數據延遲為 15 分鐘。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=DescribeLivePullToPushData&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了需帶入 API 專屬參數外，還必須帶入 [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`DescribeLivePullToPushData` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。當前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|GroupList |Array of String |否 |`["group001"]` |轉推任務群組列表。預設值為空，表示查詢所有轉推任務的時長用量。 |
|StartTime |String |是 |`2022-03-07T00:00:00Z` |查詢範圍的起始時間，需使用 RFC 3339 格式，精確到秒。 |
|EndTime |String |是 |`2021-04-14T00:00:00Z` |查詢範圍的結束時間，需使用 RFC 3339 格式，精確到秒。 |
|Aggregation |Integer |否 |`3600` |數據聚合的粒度，單位為秒，支援以下選項：<br><br><br>* `60`：1 分鐘。以 1 分鐘為聚合單位時，單次查詢的最大時間跨度為 24 小時，歷史查詢時間範圍為 366 天；<br><br>* `3600`：1 小時。以 1 小時為聚合單位時，單次查詢的最大時間跨度為 93 天，歷史查詢的最大時間範圍為 366 天。<br><br>* `86400`：（預設）1 天。以 1 天為聚合單位時，單次查詢的最大時間跨度為 93 天，歷史查詢的最大時間範圍為 366 天。 |
|DetailField |Array of String |否 |`["Group"]` |數據分割維度預設為空，表示不進行數據分割。目前僅支援以 `Group` 為數據分割維度。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">僅當 <code>DetailField</code> 參數設為 <code>Group</code> 且 <code>GroupList</code> 參數包含多個值時，才會以 <code>Group</code> 維度進行數據分割。</div><br> |
|App |String |否 |`live` |直播流 URL 中的 AppName 欄位。可包含大寫字母（A\-Z）、小寫字母（a\-z）、數字（0\-9）、底線（_）、連字號（\-）及句點（.），長度為 1 至 30 個字元。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">查詢流級別數據時，需同時傳入 <code>App</code> 與 <code>Stream</code> 參數。</div><br> |
|Stream |String |否 |`example_stream` |直播流 URL 中的 StreamName 欄位。可包含大寫及小寫字母（A\-Z, a\-z）、數字（0\-9）、底線（_）、連字號（\-）及句點（.），長度為 1 至 100 個字元。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">查詢串流粒度資料時，必須同時提供<code>App</code>與<code>Stream</code>參數。</div><br> |


<span id="Response parameters"></span>
## 回應參數

有關唯一的 API 專屬回應參數，請參見下表。更多詳情請參閱 [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 章節。


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|StartTime |String |`2021-04-13T00:00:00Z` |查詢的起始時間（UTC），格式為 RFC3339，精確到秒。 |
|EndTime |String |`2021-04-14T00:00:00Z` |查詢的結束時間（UTC），格式為 RFC3339，精確到秒。 |
|Aggregation |Integer |`300` |資料粒度，單位為秒。 |
|DetailField |Array of String |`["Group"]` |資料細分維度目前僅支援`Group`，代表群組名稱。 |
|TotalDuration |Float |`6` |在當前查詢條件下拉流與推流的總時長，單位為分鐘。 |
|PullToPushDataList |Array of [PullToPushDataList](https://docs.byteplus.com/en/docs/24/107401#pulltopushdatalist) |`-` |所有粒度層級的資料。 |
|PullToPushDetailDataList |Array of [PullToPushDetailDataList](https://docs.byteplus.com/en/docs/24/107401#pulltopushdetaildatalist) |`-` |依維度分割的資料。 |
|App |String |`live` |查詢串流粒度資料時的串流名稱中的 AppName。 |
|Stream |String |`example_stream` |查詢串流粒度資料時的串流名稱中的 StreamName。 |
|GroupList |Array of String |`["group001"]` |群組名稱清單。 |


<span id="pulltopushdatalist"></span>
### PullToPushDataList


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|TimeStamp |String |`2022-04-13T00:00:00Z` |依時間粒度聚合資料時，每個時間粒度的起始時間，格式為 RFC3339 UTC 時間，精確到秒。 |
|Value |Float |`99` |當前資料聚合時間粒度內拉流與推流的總時長，單位為分鐘。 |


<span id="pulltopushdetaildatalist"></span>
### PullToPushDetailDataList


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Group |String |`group001` |依群組維度分割資料時的群組資訊。 |
|TotalDuration |Float |`99` |依維度分割資料後當前維度下拉流與推流的總時長，單位為分鐘。 |
|PullToPushDataList |Array of [PullToPushDataList](https://docs.byteplus.com/en/docs/24/107401#pulltopushdatalist) |`-` |依維度分割資料後當前維度下所有粒度層級的資料。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```json
POST https://open.byteplusapi.com/?Action=DescribeLivePullToPushData&Version=2023-01-01
{
    "GroupList": [
        "group001"
    ],
    "StartTime": "2022-03-07T00:00:00Z",
    "EndTime": "2022-03-08T00:00:00Z",
    "Aggregation": 86400,
    "DetailField": [
        "Group"
    ]
}
```


<span id="Sample response"></span>
### 回應範例

```json
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100****",
        "Action": "DescribeLivePullToPushData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "GroupList": [
            "group001"
        ],
        "StartTime": "2022-03-07T00:00:00Z",
        "EndTime": "2022-03-08T00:00:00Z",
        "Aggregation": 86400,
        "DetailField": [
            "Group"
        ],
        "TotalDuration": 6,
        "PullToPushDataList": [
            {
                "TimeStamp": "2022-03-07T00:00:00Z",
                "Value": 99
            }
        ],
        "PullToPushDetailDataList": [
            {
                "Group": "group001",
                "TotalDuration": 6,
                "PullToPushDataList": [
                    {
                        "TimeStamp": "2022-03-07T00:00:00Z",
                        "Value": 99
                    }
                ]
            }
        ]
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為本操作相關的錯誤碼。其他錯誤碼請參見 [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**說明** |
|---|---|---|---|
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考[Request Parameters](https://docs.byteplus.com/en/docs/24/107401#request-parameters)說明進行檢查。 |
|403 |RequestForbidden |*  |請求被拒絕，因為當前帳號下無請求資源（資源包括網域名稱空間、網域名稱、App 名稱、配置與憑證）。 |
|500 |InternalError |發生內部錯誤，請聯繫管理員。 |發生內部錯誤。請[聯繫支援](https://console.byteplus.com/workorder/create)。 |
