---
title: "DescribeLiveTopPlayData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelivetopplaydata-2023-zh-TW"
---

呼叫 `DescribeLiveTopPlayData` API，查詢指定時間範圍內熱門直播流或熱門網域的流量與頻寬詳情。

## 要求

* 速率限制：每個帳號每秒 30 次查詢

* 數據延遲：前一天的數據可在當天 07:00 後查詢。

* 數據指標：

   * 頻寬數據以 1000 為基數計算，例如，1 Mbps = 1000 Kbps。

   * 流量數據以 1000 為基數計算，例如，1 GB = 1000 MB。

## HTTP 請求

* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=DescribeLiveTopPlayData&Version=2023\-01\-01

## 請求參數

### 公共參數

所有 API 除 API 特定參數外，還必須使用[公共參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)呼叫。

### 查詢

|參數 |數據類型 |必填 |範例值 |說明 |
|---|---|---|---|---|
|Action |String |是 |`DescribeLiveTopPlayData` |API 操作。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |

### Body 參數

|參數 |數據類型 |必填 |範例值 |說明 |
|---|---|---|---|---|
|StartTime |String |是 |`2024-11-16T00:00:00Z` |查詢的開始時間，採用 UTC 時間，依 RFC3339 格式，精確到秒。<br><br>> **说明**<br><br><br><br>* > 單次查詢的最長時間範圍為 31 天。<br><br><br>* > 歷史查詢範圍最長為 366 天。<br><br><br>* > 頻寬與流量數據按小時彙總。建議查詢的開始和結束時間涵蓋您要查詢期間的完整小時間隔。<br> |
|EndTime |String |是 |`2024-11-20T00:00:00Z` |查詢的結束時間，採用 UTC 時間，依 RFC3339 格式，精確到秒。 |
|QueryType |String |否 |`Stream` |查詢類型，列舉值：<br><br><br>* `Domain`：查詢熱門網域的流量與頻寬詳情。<br><br>* `Stream`（預設）：查詢熱門直播流的流量與頻寬詳情。 |
|SortBy |String |否 |`PeakBandwidth` |排序條件，列舉值：<br><br><br>* `PeakBandwidth`（預設）：依峰值頻寬降冪查詢。<br><br>* `AvgBandwidth`：依平均頻寬降冪查詢。<br><br>* `TotalTraffic`：依總流量降冪查詢。<br><br><br>> **说明**<br><br><br>> 此 API 會依指定指標對結果進行降冪排序，並根據 `PageNum` 和 `PageSize` 傳回對應的排名範圍。<br> |
|VhostList |Array of String |否 |`["push.example.com"]` |域名空間清單。預設為 null，表示查詢所有域名空間。您可以呼叫 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或前往 BytePlus 控制台的[網域](https://console.byteplus.com/live/main/domain/list)頁面，以取得域名空間資訊。 |
|DomainList |Array of String |否 |`["push.example.com"]` |網域清單。預設值為 null，表示查詢所有網域。<br><br>您可以呼叫 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或前往 BytePlus 控制台的[網域](https://console.byteplus.com/live/main/domain/list)頁面，以取得網域資訊。 |
|PageSize |Integer |否 |`10` |每頁的查詢結果數量。有效值：[1,1000]。預設值：`10`。<br><br>> **说明**<br><br><br>> 如果將此參數設為 `0`，則會使用預設值。<br> |
|PageNum |Integer |否 |`1` |頁碼。值必須大於或等於 `1`。預設值：`1`。 |

## 回應參數

如需唯一的 API 特定回應參數，請參閱下表。如需更多詳情，請參閱[請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)章節。

|參數 |數據類型 |範例值 |說明 |
|---|---|---|---|
|StartTime |String |`2024-11-16T00:00:00Z` |查詢的開始時間，採用 UTC 時間，依 RFC3339 格式，精確到秒。 |
|EndTime |String |`2024-11-20T00:00:00Z` |查詢的結束時間，採用 UTC 時間，依 RFC3339 格式，精確到秒。 |
|QueryType |String |`Stream` |查詢類型，列舉值：<br><br><br>* `Domain`：查詢熱門網域的流量與頻寬詳情。<br><br>* `Stream`（預設）：查詢熱門直播流的流量與頻寬詳情。 |
|SortBy |String |`PeakBandwidth` |排序條件，列舉值：<br><br><br>* `PeakBandwidth`（預設）：依峰值頻寬降冪查詢。<br><br>* `AvgBandwidth`：依平均頻寬降冪查詢。<br><br>* `TotalTraffic`：依總流量降冪查詢。 |
|VhostList |Array of String |`["push.example.com"]` |域名空間清單。 |
|DomainList |Array of String |`["push.example.com"]` |網域清單。 |
|DataItemList |Array of [DataItemList](https://docs.byteplus.com/en/docs/24/107396#dataitemlist) |`-` |頻寬與流量的詳細數據。 |
|Pagination |Object of [Pagination](https://docs.byteplus.com/en/docs/24/107396#pagination) |`-` |查詢結果的分頁資訊。 |

### DataItemList

|參數 |數據類型 |範例值 |說明 |
|---|---|---|---|
|Domain |String |`push.example.com` |網域名稱。 |
|App |String |`live` |直播流 URL 中的 AppName 欄位。依 Domain 查詢時，將此欄位留空。 |
|Stream |String |`example_stream` |直播流 URL 中的 StreamName 欄位。依 Domain 查詢時，將此欄位留空。 |
|PeakBandwidth |Float |`1000` |峰值頻寬，單位為 bps。 |
|AvgBandwidth |Float |`1000` |平均頻寬，單位為 bps。 |
|TotalTraffic |Float |`1000` |總流量，單位為 Bytes。 |

### Pagination

|參數 |數據類型 |範例值 |說明 |
|---|---|---|---|
|PageSize |Integer |`10` |每頁顯示的數據項目數。 |
|PageNum |Integer |`1` |分頁中的目前頁碼。 |
|TotalCount |String |`20` |查詢結果中的數據項目總數。 |

## 範例

### 範例請求

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveTopPlayData&Version=2023-01-01
{
    "StartTime": "2024-11-16T00:00:00Z",
    "EndTime": "2024-11-20T00:00:00Z",
    "QueryType": "Stream",
    "SortBy": "PeakBandwidth",
    "VhostList": [
        "push.example.com"
    ],
    "DomainList": [
        "push.example.com"
    ],
    "PageSize": 10,
    "PageNum": 1
}
```

### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeLiveTopPlayData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "StartTime": "2024-11-16T00:00:00Z",
        "EndTime": "2024-11-20T00:00:00Z",
        "QueryType": "Stream",
        "SortBy": "PeakBandwidth",
        "VhostList": [
            "push.example.com"
        ],
        "DomainList": [
            "push.example.com"
        ],
        "DataItemList": [
            {
                "Domain": "push.example.com",
                "App": "live",
                "Stream": "example_stream",
                "PeakBandwidth": 1000,
                "AvgBandwidth": 1000,
                "TotalTraffic": 1000
            }
        ],
        "Pagination": {
            "PageSize": 10,
            "PageNum": 1,
            "TotalCount": "20"
        }
    }
}
```

## 錯誤碼

以下是與目前操作相關的錯誤碼。如需其他錯誤碼，請參閱 [BytePlus OpenAPI 公共錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。

|狀態碼 |錯誤碼 |錯誤訊息 |說明 |
|---|---|---|---|
|400 |InvalidParam |\- |輸入參數無效或不符合要求。請參閱[請求參數](https://docs.byteplus.com/en/docs/24/107396#request-parameters)說明進行檢查。 |
|403 |RequestForbidden |\- |請求被拒絕，因為目前帳號下沒有請求的資源（資源包括域名空間、網域名稱、應用程式名稱、設定和憑證）。 |
|500 |InternalError |an internal error occurred, please contact the administrator. |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
