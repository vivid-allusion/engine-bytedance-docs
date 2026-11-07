---
title: "DescribeLiveCallbackData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelivecallbackdata-zh-TW"
---

此 API 可讓您查詢與直播相關的回呼記錄，包括事件類型、狀態、請求與回應資料。它可協助您排查回呼異常，並確認回呼是否已成功送達。

## 要求

速率限制：每個帳號每秒 30 次查詢。

## HTTP 請求

* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=DescribeLiveCallbackData&Version=2023\-01\-01

## 請求參數

### 公共參數

呼叫所有 API 時，除了 API 專屬參數外，還必須帶上[公共參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

### 查詢

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DescribeLiveCallbackData` |API 操作。 |
|Version |String |Yes |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |

### 主體參數

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|DomainList |String 陣列 |No |`["example.com", "example2.com"]` |要查詢的網域名稱清單。預設表示目前帳號下的所有網域名稱。 |
|App |String |No |`example_app` |應用程式名稱。必須與串流 URL 中使用的名稱相符。 |
|Stream |String |No |`example_stream` |串流名稱，用於準確定位特定直播串流。 |
|CallbackEventType |String 陣列 |No |`["push_start"]` |支援的回呼事件類型：<br><br><br>* `push_start`：推流開始<br><br>* `push_end`：推流結束<br><br>* `snapshot_event`：截圖回呼<br><br>* `record_event`：錄製回呼 |
|CallbackStatus |String 陣列 |No |`["success"]` |回呼狀態。支援以下值：<br><br><br>* `success`：成功。<br><br>* `fail`：失敗。 |
|StartTime |String |Yes |`2021-08-16T00:01:59Z` |查詢的開始時間，採用 UTC 時間與 RFC3339 格式，精度為秒。<br><br>> **说明**<br><br><br>> 單次查詢的最大時間跨度為 31 天，歷史查詢的最大時間範圍為 366 天。<br> |
|EndTime |String |Yes |`2021-08-16T00:01:59Z` |查詢的結束時間，採用 UTC 時間與 RFC3339 格式，精度為秒。 |
|PageNum |Integer |No |`1` |頁碼。值必須大於或等於 `1`。預設值：`1`。 |
|PageSize |Integer |No |`100` |每頁的查詢結果數量。有效值：[1,1000]。預設值：`100`。<br><br>> **说明**<br><br><br>> 如果將此參數設為 `0`，則使用預設值。<br> |

## 回應參數

如需 API 專屬的唯一回應參數，請參閱下表。如需更多詳細資訊，請參閱[請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)章節。

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|DomainList |String 陣列 |`["example.com", "example2.com"]` |網域名稱清單。 |
|App |String |`example_app` |應用程式名稱。 |
|Stream |String |`example_stream` |串流名稱。 |
|CallbackEventType |String 陣列 |`["push_start"]` |回呼事件類型。 |
|CallbackStatus |String 陣列 |`["success"]` |回呼狀態值。 |
|StartTime |String |`2021-08-16T00:01:59Z` |查詢的開始時間，採用 UTC 時間與 RFC3339 格式，精度為秒。 |
|EndTime |String |`2022-11-11T00:00:00Z` |查詢的結束時間，採用 UTC 時間與 RFC3339 格式，精度為秒。 |
|CallbackInfoList |[CallbackInfoList](https://docs.byteplus.com/en/docs/24/107367#callbackinfolist) 陣列 |`-` |回呼事件的詳細資訊。 |
|Pagination |[Pagination](https://docs.byteplus.com/en/docs/24/107367#pagination) 物件 |`-` |查詢結果的分頁資訊。 |

### CallbackInfoList

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Domain |String |`example.com` |網域名稱。 |
|App |String |`example_app` |應用程式名稱。 |
|Stream |String |`example_stream` |串流名稱。 |
|CallbackTime |String |`2022-11-11T00:00:00Z` |回呼執行時間。 |
|CallbackEventType |String |`push_start` |回呼事件類型。 |
|CallbackMethod |String |`post` |回呼請求方法。 |
|CallbackAddress |String |`http://example.com/xxx` |回呼目的地 URL。 |
|CallbackStatus |String |`success` |回呼狀態。 |
|CallbackBody |String |`{}` |回呼請求主體。 |
|CallbackResponseCode |String |`200` |回應的 HTTP 狀態碼。 |
|CallbackResponseHeader |String |`Content-Type: application/json; charset=utf-8\r\nContent-Length: 29` |HTTP 回應標頭。 |
|CallbackResponseBody |String |`{"error_code":200,"msg":"ok"}` |回呼的回應主體。 |
|CallbackResponseTime |String |`2022-11-11T00:00:00Z` |回呼回應時間。 |
|CallbackErrorMessage |String |`InternalServiceError` |錯誤訊息，於回呼失敗時返回。 |
|CallbackErrorCode |String |`The callback receiving service is unreachable. Please check whether the callback address is available.` |錯誤描述。 |

### Pagination

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|PageNum |Integer |`1` |目前頁面的頁碼。 |
|PageSize |Integer |`100` |每頁顯示的資料項目數量。 |
|TotalCount |Integer |`100` |查詢結果中的資料總數。 |

## 範例

### 範例請求

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveCallbackData&Version=2023-01-01
```

### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "20250410201942D5628AA78C98A0C818D0",
        "Action": "DescribeLiveCallbackData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "CallbackEventType": [
            "push_end"
        ],
        "StartTime": "2025-03-18T00:00:00Z",
        "EndTime": "2025-03-19T00:00:00Z",
        "CallbackInfoList": [
            {
                "Domain": "example.com",
                "App": "app_test",
                "Stream": "stream-111",
                "CallbackTime": "2025-03-18T23:30:52Z",
                "CallbackEventType": "push_end",
                "CallbackMethod": "post",
                "CallbackAddress": "http://example.com/callback/record",
                "CallbackStatus": "success",
                "CallbackBody": "{}",
                "CallbackResponseCode": "200",
                "CallbackResponseHeader": "HTTP/1.1 200 OK",
                "CallbackResponseBody": "{\"error_code\":200,\"msg\":\"ok\"}",
                "CallbackResponseTime": "2025-03-18T23:30:53Z",
                "CallbackErrorCode": "",
                "CallbackErrorMessage": ""
            }
        ],
        "Pagination": {
            "PageNum": 1,
            "PageSize": 100,
            "TotalCount": 1
        }
    }
}
```

## 錯誤碼

以下是與目前操作相關的錯誤碼。如需其他錯誤碼，請參閱 [BytePlus OpenAPI 公共錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。

|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|200 |CommonErr |\- |未分類錯誤。建議重試。如果仍返回此錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |\- |輸入參數無效或不符合要求。請參閱請求參數的描述進行檢查。 |
|400 |InvalidParam.BindError |Request parameter error, please check input data |參數驗證失敗。請檢查參數類型是否正確。 |
|403 |RequestForbidden |\- |請求遭到拒絕。目前帳號下沒有請求的資源（網域命名空間、網域名稱、應用程式、組態範本、憑證）。 |
|404 |ResourceNotFound |\- |找不到資源（網域命名空間、網域名稱、應用程式、組態範本、憑證）。建議重試。如果仍返回此錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |an internal error occurred, please contact the administrator. |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |服務之間發生錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |服務之間發生錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |內部服務逾時，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
