---
title: "DescribeLivePullToPushBandwidthData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describelivepulltopushbandwidthdata-zh-TW"
---

呼叫 `DescribeLivePullToPushBandwidthData` API，以查詢在指定時間範圍內產生的轉推任務的頻寬使用情況。

<span id="Requirements"></span>
## 需求


* 計費：有關推流至第三方時的轉推頻寬價格，請參閱 [Relay](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-relay-1)。

* 頻率限制：每個帳戶每秒最多 30 次查詢

* 資料延遲：15 分鐘

* 資料指標：頻寬資料以 1000 為基數計算，例如，1 Mbps = 1000 Kbps。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=DescribeLivePullToPushBandwidthData&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了專屬參數外，還必須帶上 [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`DescribeLivePullToPushBandwidthData` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|GroupList |String 陣列 |否 |`["group001","group002"]` |轉推任務群組列表。預設值為空，表示查詢所有轉推任務的頻寬使用情況。 |
|StartTime |String |是 |`2021-04-13T00:00:00Z` |查詢範圍的起始時間，需符合 RFC 3339 格式並精確到秒。 |
|EndTime |String |是 |`2021-04-14T00:00:00Z` |查詢範圍的結束時間，需符合 RFC 3339 格式並精確到秒。 |
|Aggregation |Integer |否 |`300` |資料彙總粒度，以秒為單位，支援以下選項：<br><br><br>* `300`（預設）：5 分鐘。以 5 分鐘為粒度彙總時，單次查詢的最大時間跨度為 31 天，歷史查詢的最大時間範圍為 366 天。<br><br>* `3600`：1 小時。以 1 小時為粒度彙總時，單次查詢的最大時間跨度為 93 天，歷史查詢的最大時間範圍為 366 天。<br><br>* `86400`：1 天。以 1 天為粒度彙總時，單次查詢的最大時間跨度為 93 天，歷史查詢的最大時間範圍為 366 天。 |
|DetailField |String 陣列 |否 |`["Group"]` |資料分段維度預設為空，表示不進行資料分段。目前僅支援 `Group` 維度進行資料分段。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">僅當 <code>Group</code> 維度資料分段時，且 <code>DetailField</code> 參數設為 <code>Group</code> 且 <code>GroupList</code> 參數包含多個值時，才會進行分段。</div><br> |


<span id="Response parameters"></span>
## 回應參數

有關唯一的 API 專屬回應參數，請參見下表。更多細節請參閱 [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 章節。


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|StartTime |String |`2021-04-13T00:00:00Z` |查詢範圍的起始時間，需符合 RFC 3339 格式並精確到秒。 |
|EndTime |String |`2021-04-14T00:00:00Z` |查詢範圍的結束時間，需符合 RFC 3339 格式並精確到秒。 |
|Aggregation |Integer |`300` |資料粒度，以秒為單位。 |
|DetailField |String 陣列 |`["Group"]` |資料分段維度目前僅限於 `Group`，代表群組名稱。 |
|PeakUpBandwidth |Float |`12` |在目前查詢條件下拉流與推流的峰值頻寬，單位為 Mbps。 |
|BandwidthDataList |[BandwidthDataList](https://docs.byteplus.com/en/docs/24/107450#bandwidthdatalist) 陣列 |`-` |所有時間粒度的資料。 |
|BandwidthDetailDataList |[BandwidthDetailDataList](https://docs.byteplus.com/en/docs/24/107450#bandwidthdetaildatalist) 陣列 |`-` |資料經由維度分割後。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">僅當對應維度參數輸入多個值時，資料才會依指定維度分割後返回。</div><br> |
|GroupList |字串陣列 |`["group001"]` |群組名稱列表。 |


<span id="bandwidthdatalist"></span>
### BandwidthDataList


|**參數** |**資料型態** |**範例值** |**說明** |
|---|---|---|---|
|TimeStamp |字串 |`2022-04-13T00:00:00Z` |資料按時間粒度聚合時，每個時間粒度的起始時間，格式為 RFC3339 UTC 時間，精確到秒。 |
|UpBandwidth |浮點數 |`12.0` |在當前資料聚合時間粒度內，拉流與推流的峰值頻寬，單位為 Mbps。 |


<span id="bandwidthdetaildatalist"></span>
### BandwidthDetailDataList


|**參數** |**資料型態** |**範例值** |**說明** |
|---|---|---|---|
|Group |字串 |`group001` |資料按群組維度分割時的群組資訊。 |
|PeakUpBandwidth |浮點數 |`12.0` |在指定維度的時間範圍內，拉流與推流的峰值頻寬，單位為 Mbps。 |
|BandwidthDataList |[BandwidthDataList](https://docs.byteplus.com/en/docs/24/107450#bandwidthdatalist) 陣列 |`-` |資料分割後，當前維度下每個粒度層級的所有資料。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://open.byteplusapi.com/?Action=DescribeLivePullToPushBandwidthData&Version=2023-01-01
{
    "GroupList": [
        "group001"
    ],
    "StartTime": "2021-04-13T00:00:00Z",
    "EndTime": "2021-04-14T00:00:00Z",
    "Aggregation": 300,
    "DetailField": [
        "Group"
    ]
}
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "DescribeLivePullToPushBandwidthData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "GroupList": [
            "group001"
        ],
        "StartTime": "2021-04-13T00:00:00Z",
        "EndTime": "2021-04-14T00:00:00Z",
        "Aggregation": 300,
        "DetailField": [
            "Group"
        ],
        "PeakUpBandwidth": 12,
        "BandwidthDataList": [
            {
                "TimeStamp": "2022-04-13T00:00:00Z",
                "UpBandwidth": 12
            },
            {
                "TimeStamp": "2022-04-13T00:00:05Z",
                "UpBandwidth": 10
            }
        ],
        "BandwidthDetailDataList": [
            {
                "DstAddrType": "Live",
                "PeakUpBandwidth": 12,
                "BandwidthDataList": [
                    {
                        "TimeStamp": "2022-04-13T00:00:00Z",
                        "UpBandwidth": 12
                    },
                    {
                        "TimeStamp": "2022-04-13T00:00:05Z",
                        "UpBandwidth": 10
                    }
                ]
            },
            {
                "DstAddrType": "Third",
                "PeakUpBandwidth": 12,
                "BandwidthDataList": [
                    {
                        "TimeStamp": "2022-04-13T00:00:00Z",
                        "UpBandwidth": 12
                    },
                    {
                        "TimeStamp": "2022-04-13T00:00:05Z",
                        "UpBandwidth": 10
                    }
                ]
            }
        ]
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為與本操作相關的錯誤碼。其他錯誤碼請參見 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**說明** |
|---|---|---|---|
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考 [Request Parameters](https://docs.byteplus.com/en/docs/24/107450#request-parameters) 說明進行檢查。 |
|403 |RequestForbidden |*  |因當前帳戶下無請求資源（資源包括域名空間、域名、App 名稱、配置及憑證），請求被拒絕。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請 [聯絡客服](https://console.byteplus.com/workorder/create)。 |
