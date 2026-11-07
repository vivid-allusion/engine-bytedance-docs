---
title: "DescribeCDNSnapshotHistory"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describecdnsnapshothistory-2023-zh-TW"
---

呼叫 `DescribeCDNSnapshotHistory` API 以查詢直播的截圖檔案資訊。

## 要求

速率限制：每個帳號每秒 1 次查詢。

## HTTP 請求

* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=DescribeCDNSnapshotHistory&Version=2023\-01\-01

## 請求參數

### 通用參數

除 API 特定參數外，所有 API 都必須搭配[通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)呼叫。

### 查詢

|參數 |資料類型 |必填 |範例值 |說明 |
|---|---|---|---|---|
|Action |String |是 |`DescribeCDNSnapshotHistory` |API 作業。 |
|Version |String |是 |`2023-01-01` |此 API 作業的版本。目前版本：2023\-01\-01。 |

### 主體參數

|參數 |資料類型 |必填 |範例值 |說明 |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |網域名稱空間。您可以呼叫 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或前往 BytePlus MediaLive 主控台的 [網域](https://console.byteplus.com/live/main/domain/list) 頁面，以取得網域所屬的網域名稱空間。 |
|App |String |是 |`live` |直播 URL 中的 AppName 欄位。可包含大寫字母 (A\-Z)、小寫字母 (a\-z)、數字 (0\-9)、底線 (_)、連字號 (\-) 和句點 (.)，長度範圍為 1 到 30 個字元。 |
|Stream |String |是 |`stream-123` |直播 URL 中的 StreamName 欄位。可包含大寫字母 (A\-Z)、小寫字母 (a\-z)、數字 (0\-9)、底線 (_)、連字號 (\-) 和句點 (.)，長度範圍為 1 到 100 個字元。 |
|DateFrom |String |是 |`2022-04-01T00:00:00Z` |查詢範圍的開始時間（本地時間，RFC 3339 格式，精確到秒）。查詢指定錄製任務的詳細資料時，DateFrom 應設為錄製任務開始時間之前的任意時間。 |
|DateTo |String |是 |`2022-04-02T00:00:00Z` |查詢範圍的結束時間（本地時間，RFC 3339 格式，精確到秒）。DateTo 必須晚於 DateFrom，且 DateTo 與 DateFrom 之間的間隔不得超過 7 天。 |
|PageNum |Integer |否 |`1` |頁碼。值必須大於或等於 `1`。預設值：`1`。 |
|PageSize |Integer |否 |`10` |每頁的查詢結果數量。有效值：[1,1000]。預設值：`10`。<br><br>> **说明**<br><br><br>> 如果您將此參數設為 `0`，則會使用預設值。<br> |
|Type |String |否 |`tos` |儲存類型。請一律設為 `tos`。 |

## 回應參數

如需唯一的 API 特定回應參數，請參閱下表。如需更多詳細資料，請參閱[請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)章節。

|參數 |資料類型 |範例值 |說明 |
|---|---|---|---|
|Data |[Data](https://docs.byteplus.com/en/docs/24/107261#data) 的陣列 |`-` |截圖記錄清單。 |
|Pagination |[Pagination](https://docs.byteplus.com/en/docs/24/107261#pagination) 的物件 |`-` |分頁資訊。 |

### Data

|參數 |資料類型 |範例值 |說明 |
|---|---|---|---|
|Vhost |String |`push.example.com` |網域名稱空間。 |
|App |String |`live` |AppName 欄位。 |
|Stream |String |`stream-123` |StreamName 欄位。 |
|Path |String |`20210830135051697.jpeg` |截圖檔案的儲存路徑。 |
|TimeStamp |String |`2021-08-30 21:48:25.000` |精確到毫秒的截圖時間戳記。 |
|Width |Integer |`720` |截圖寬度，單位為 px。 |
|Height |Integer |`1280` |截圖高度，單位為 px。 |

### Pagination

|參數 |資料類型 |範例值 |說明 |
|---|---|---|---|
|PageCur |Integer |`1` |目前頁碼。 |
|PageSize |Integer |`10` |每頁的結果數量。 |
|PageTotal |Integer |`231` |總頁數。 |
|TotalCount |Integer |`4613` |擷取到的錄製檔案總數。 |

## 範例

### 範例請求

```json
POST https://open.byteplusapi.com/?Action=DescribeCDNSnapshotHistory&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "App": "live",
    "Stream": "stream-123",
    "DateFrom": "2022-04-01T00:00:00Z",
    "DateTo": "2022-04-02T00:00:00Z"
}
```

### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "DescribeCDNSnapshotHistory",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Data": [
            {
                "App": "live",
                "FileSize": 0,
                "Height": 1280,
                "Path": "20210830135051697.jpeg",
                "Stream": "testStream413",
                "TimeStamp": "2021-08-30 21:48:25.000",
                "Vhost": "example.org",
                "Width": 720
            }
        ],
        "Pagination": {
            "PageCur": 1,
            "PageSize": 10,
            "PageTotal": 231,
            "TotalCount": 4613
        }
    }
}
```

## 錯誤碼

以下是與目前作業相關的錯誤碼。如需其他錯誤碼，請參閱 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。

|狀態碼 |錯誤碼 |錯誤訊息 |說明 |
|---|---|---|---|
|200 |CommonErr |\- |未分類錯誤。建議重試。如果仍傳回此錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |\- |輸入參數無效或不符合要求。請參閱[請求參數](https://docs.byteplus.com/en/docs/24/107261#request-parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |Request parameter error, please check input data |參數驗證失敗。請檢查資料類型是否正確。 |
|403 |RequestForbidden |\- |由於目前帳號下沒有請求的資源，因此請求遭到拒絕（資源包括網域名稱空間、網域名稱、應用程式名稱、設定和憑證）。 |
|403 |RequestForbidden.AccountIDNotAllow |this AccountID does not have permission to access the corresponding resource, please check the request parameters |由於目前帳號下沒有請求的資源，因此請求遭到拒絕（資源包括網域名稱空間、網域名稱、應用程式名稱、設定和憑證）。 |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |視訊直播服務尚未啟用，或帳號欠費，導致帳單無法使用。請檢查服務啟用狀態和帳號欠費狀態。 |
|404 |ResourceNotFound |\- |找不到資源（包括網域名稱空間、網域名稱、應用程式名稱、設定和憑證）。建議重試。如果仍傳回此錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |an internal error occurred, please contact the administrator. |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |內部服務逾時。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
