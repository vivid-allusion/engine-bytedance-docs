---
title: "ListPullRecordTask"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listpullrecordtask-zh-TW"
---

此 API 用於查詢目前帳戶下建立的直播錄製任務清單，並支援依分頁、網域名稱、應用程式名稱、串流名稱等條件進行組合查詢。透過此 API，您可以取得任務的具體資訊，例如錄製時段、任務狀態等。這有助於追蹤錄製進度、監控任務狀態，並支援後續資源管理工作。

## 要求

* 速率限制：每個帳戶每秒 50 次查詢。

* 計費：此 API 用於查詢已建立的錄製任務記錄，不涉及即時錄製或資料儲存操作，因此不會產生費用。

## HTTP 請求

* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=ListPullRecordTask&Version=2023\-01\-01

## 請求參數

### 通用參數

除 API 專屬參數外，所有 API 都必須使用[通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)呼叫。

### 查詢

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`ListPullRecordTask` |API 操作。 |
|Version |String |Yes |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |

### 主體參數

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|PageNum |Integer |Yes |`1` |頁碼。值必須大於或等於 `1`。 |
|PageSize |Integer |Yes |`5` |每頁的查詢結果數量。有效值：`[1,500]`。 |
|Vhost |String |No |`example` |網域名稱空間。您可以呼叫 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或前往 BytePlus MediaLive 主控台中的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面，以取得網域所屬的網域名稱空間。 |
|Domain |String |No |`push.example.com` |直播串流使用的推流網域名稱或拉流網域名稱。您可以呼叫 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或前往 BytePlus MediaLive 主控台中的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面，以取得網域名稱。 |
|App |String |No |`live` |應用程式名稱，與直播串流位址中的 `AppName` 欄位值相同，用於指定要更新的錄製設定。預設為空。您可以呼叫  [ListVhostRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostrecordpresetv2-2023) API，以取得 `App` 值。 |
|Stream |String |No |`example_stream` |串流名稱，其值對應直播串流位址中 `StreamName` 欄位的值，用於指定要查詢的錄製任務，預設為空。您可以呼叫  [ListVhostRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostrecordpresetv2-2023) API，以取得 `Stream` 的值。 |

## 回應參數

如需 API 專屬回應參數，請參閱下表。如需更多詳細資訊，請參閱[請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)章節。

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|List |Array of [List](https://docs.byteplus.com/en/docs/24/107263#list) |`-` |直播錄製任務清單。 |
|Pagination |Object of [Pagination](https://docs.byteplus.com/en/docs/24/107263#pagination) |`-` |查詢結果的分頁資訊。 |

### List

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|TaskId |String |`f831f3b0dc******aa4dcf7621` |任務 ID，任務的唯一識別碼。 |
|StartTime |String |`2023-06-30T15:04:05Z` |錄製開始時間，採用 RFC3339 格式的 UTC 時間，精確到秒。 |
|EndTime |String |`2023-06-30T15:05:05Z` |錄製結束時間，採用 RFC3339 格式的 UTC 時間，精確到秒。 |
|Vhost |String |`push.example.com` |網域命名空間名稱。 |
|Domain |String |`push.example.com` |推流網域名稱或拉流網域名稱。 |
|App |String |`Live` |應用程式名稱。 |
|Stream |String |`example_stream` |串流名稱。 |
|Status |String |`Finished` |錄製任務的狀態。可能值如下。<br><br><br>* `停用`：錄製任務已停止；<br><br>* `未开始`：錄製任務尚未開始；<br><br>* `生效中`：錄製任務進行中；<br><br>* `已结束`：錄製已完成。 |

### Pagination

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|PageCur |Integer |`1` |目前頁面的頁碼。 |
|PageSize |Integer |`2` |每頁顯示的資料項目數量。 |
|PageTotal |Integer |`43` |查詢結果資料的總頁數。 |
|TotalCount |Integer |`86` |查詢結果中的資料項目總數。 |

## 範例

### 範例請求

```json
POST https://open.byteplusapi.com/?Action=ListPullRecordTask&Version=2023-01-01
{
    "PageNum": 1,
    "PageSize": 2
}
```

### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListPullRecordTask",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "List": [
            {
                "TaskId": "f831f3b0dc******aa4dcf7621",
                "StartTime": "2023-06-30T15:04:05Z",
                "EndTime": "2023-06-30T15:05:05Z",
                "Vhost": "push.example.com",
                "Domain": "push.example.com",
                "App": "Live",
                "Stream": "example_stream",
                "Status": "Finished"
            },
            {
                "TaskId": "a1b2c3d4e5******f6g7h8i9j0",
                "StartTime": "2023-06-30T16:04:05Z",
                "EndTime": "2023-06-30T16:05:05Z",
                "Vhost": "pull.example.com",
                "Domain": "pull.example.com",
                "App": "Live",
                "Stream": "another_stream",
                "Status": "InProgress"
            }
        ],
        "Pagination": {
            "PageCur": 1,
            "PageSize": 2,
            "PageTotal": 43,
            "TotalCount": 86
        }
    }
}
```

## 錯誤碼

以下是與目前操作相關的錯誤碼。如需其他錯誤碼，請參閱 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。

|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|200 |CommonErr |\- |未分類錯誤。建議重試。如果仍傳回此錯誤碼，請 [聯絡支援](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |\- |輸入參數無效或不符合要求。請參閱[請求參數](#Request Parameters)的描述進行檢查。 |
|400 |InvalidParam.BindError |Request parameter error, please check input data |參數驗證失敗。請檢查參數類型是否正確。 |
|403 |RequestForbidden |\- |請求遭拒。目前帳戶下沒有請求的資源（網域名稱空間、網域名稱、應用程式、設定範本、憑證）。 |
|403 |RequestForbidden.AccountIDNotAllow |this AccountID does not have permission to access the corresponding resource, please check the request parameters |請求遭拒。目前帳戶下沒有請求的資源（網域名稱空間、網域名稱、應用程式、設定範本、憑證）。 |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |視訊直播服務未啟用，或帳戶欠費，導致帳單無法使用。請檢查服務啟用狀態和帳戶欠費情況。 |
|404 |ResourceNotFound |\- |找不到資源（網域命名空間、網域名稱、應用程式、設定範本、憑證）。建議重試。如果仍傳回此錯誤碼，請 [聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |an internal error occurred, please contact the administrator. |發生內部錯誤，請 [聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |服務之間發生錯誤，請 [聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |服務之間存在錯誤，請 [聯絡支援](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |內部服務逾時，請 [聯絡支援](https://console.byteplus.com/workorder/create)。 |
