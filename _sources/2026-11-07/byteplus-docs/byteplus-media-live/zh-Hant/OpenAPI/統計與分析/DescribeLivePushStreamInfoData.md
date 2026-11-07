---
title: "DescribeLivePushStreamInfoData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describelivepushstreaminfodata-zh-TW"
---

呼叫 `DescribeLivePushStreamInfoData` API 以查詢推流資訊及斷流原因

## 要求

* 速率限制：每個帳號每秒 100 次查詢

## HTTP 要求

* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=DescribeLivePushStreamInfoData&Version=2023\-01\-01

## 要求參數

### 共用參數

除 API 特定參數外，所有 API 都必須搭配[共用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)呼叫。

### 查詢

|參數 |資料類型 |必填 |範例值 |說明 |
|---|---|---|---|---|
|Action |String |是 |`DescribeLivePushStreamInfoData` |API 操作。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |

### 主體參數

|參數 |資料類型 |必填 |範例值 |說明 |
|---|---|---|---|---|
|DomainList |String 陣列 |否 |`["push.example.com","push2.example.com"]` |您要查詢的網域名稱清單。 |
|App |String |否 |`live` |直播串流 URL 中的 AppName 欄位。可包含大寫字母 (A\-Z)、小寫字母 (a\-z)、數字 (0\-9)、底線 (_)、連字號 (\-) 和句點 (.)，長度範圍為 1 到 30 個字元。 |
|Stream |String |否 |`example_stream` |直播串流 URL 中的 StreamName 欄位。可包含大寫字母 (A\-Z)、小寫字母 (a\-z)、數字 (0\-9)、底線 (_)、連字號 (\-) 和句點 (.)，長度範圍為 1 到 100 個字元。 |
|StartTime |String |是 |`2023-05-29T00:00:00Z` |查詢範圍的開始時間，格式為 RFC 3339，精度為秒。您可以查詢過去 93 天內開始的資料。 |
|EndTime |String |是 |`2023-05-29T00:00:00Z` |查詢範圍的結束時間，格式為 RFC 3339，精度為秒。 |
|PageNum |Integer |否 |`1` |頁碼。值必須大於或等於 `1`。預設值：`1`。 |
|PageSize |Integer |否 |`20` |每頁的查詢結果數量。有效值：[1,1000]。預設值：`20`。<br><br>> **说明**<br><br><br>> 如果將此參數設為 `0`，則會使用預設值。<br> |

## 回應參數

如需 API 特有的回應參數，請參閱下表。如需更多詳細資訊，請參閱[要求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)章節。

|參數 |資料類型 |範例值 |說明 |
|---|---|---|---|
|DomainList |String 陣列 |`["push.example.com"]` |用於推流的網域名稱。 |
|App |String |`example_app` |直播串流 URL 中的 AppName 欄位。 |
|Stream |String |`exampel_stream` |直播串流 URL 中的 StreamName 欄位。 |
|StartTime |String |`2024-03-16T00:00:00Z` |查詢範圍的開始時間，格式為 RFC 3339，精度為秒。 |
|EndTime |String |`2024-03-16T00:01:59Z` |查詢範圍的結束時間，格式為 RFC 3339，精度為秒。 |
|PushStreamInfoDataList |[PushStreamInfoDataList](https://docs.byteplus.com/en/docs/24/107324#pushstreaminfodatalist) 陣列 |`-` |推流的詳細資訊。 |
|Pagination |[Pagination](https://docs.byteplus.com/en/docs/24/107324#pagination) 物件 |`-` |分頁資訊。 |

### PushStreamInfoDataList

|參數 |資料類型 |範例值 |說明 |
|---|---|---|---|
|App |String |`example_app` |直播串流 URL 中的 AppName 欄位。 |
|Stream |String |`example_stream` |直播串流 URL 中的 StreamName 欄位。 |
|StartTime |String |`2024-03-16T00:00:00Z` |每個區間的開始時間。RFC 3339 格式的 UTC 時間。 |
|EndTime |String |`2024-03-16T00:00:30Z` |每個區間的結束時間。RFC 3339 格式的 UTC 時間。 |
|Duration |Integer |`122345` |串流的持續時間。 |
|IP |String |`xx.xx.xx.xx` |推流的 IP 位址。 |
|StreamBreakReason |String |`Duplicate stream push with the same stream ID` |結束串流的原因。 |

### Pagination

|參數 |資料類型 |範例值 |說明 |
|---|---|---|---|
|PageCur |Integer |`1` |目前頁碼。 |
|PageSize |Integer |`20` |記錄檔大小，單位為位元組。 |
|TotalCount |Integer |`2` |結果總數。 |

## 範例

### 範例要求

```json
POST https://open.byteplusapi.com/?Action=DescribeLivePushStreamInfoData&Version=2023-01-01
{
    "Domain": "example.com",
    "App": "example_app",
    "Stream": "example_stream",
    "StartTime": "2021-08-16T00:00:00Z",
    "EndTime": "2021-08-16T00:01:59Z"
}
```

### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "DescribeLivePushStreamInfoData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "DomainList": [
            "push.example.com"
        ],
        "App": "example_app",
        "Stream": "exampel_stream",
        "StartTime": "2024-03-16T00:00:00Z",
        "EndTime": "2024-03-16T00:01:59Z",
        "PushStreamInfoDataList": [
            {
                "App": "example_app",
                "Stream": "example_stream",
                "StartTime": "2024-03-16T00:00:00Z",
                "EndTime": "2024-03-16T00:00:30Z",
                "Duration": 122345,
                "IP": "xx.xx.xx.xx",
                "StreamBreakReason": "Duplicate stream push with the same stream ID"
            }
        ],
        "Pagination": {
            "PageCur": 1,
            "PageSize": 20,
            "TotalCount": 2
        }
    }
}
```

## 錯誤碼

以下是與目前操作相關的錯誤碼。如需其他錯誤碼，請參閱 [BytePlus OpenAPI 的常見錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。

|狀態碼 |錯誤碼 |錯誤訊息 |說明 |
|---|---|---|---|
|400 |InvalidParam |\- |輸入參數無效或不符合要求。請參閱 [要求參數](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveispdata#request-parameters) 說明進行檢查。 |
|500 |InternalError |an internal error occurred, please contact the administrator. |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
