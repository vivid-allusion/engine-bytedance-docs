---
title: "DeleteUserAgentAccessRule"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deleteuseragentaccessrule_1-zh-TW"
---

呼叫 `DeleteUserAgentAccessRule` API 以刪除 User\-Agent 限制。

## 要求

速率限制：每個帳號每秒 10 次查詢。

## HTTP 請求

* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=DeleteUserAgentAccessRule&Version=2023\-01\-01

## 請求參數

### 公共參數

所有 API 除了 API 特定參數外，還必須使用[公共參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)呼叫。

### 查詢

|參數 |資料類型 |是否必填 |範例值 |描述 |
|---|---|---|---|---|
|Action |String |是 |`DeleteUserAgentAccessRule` |API 操作。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |

### 主體參數

|參數 |資料類型 |是否必填 |範例值 |描述 |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |域名空間。你可以呼叫 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或前往 BytePlus MediaLive 控制台的[域名](https://console.byteplus.com/live/main/domain/list)頁面，以取得域名空間。 |
|Domain |String |是 |`pull.example.com` |用於拉流的域名。你可以呼叫 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或前往 BytePlus MediaLive 控制台的[域名](https://console.byteplus.com/live/main/domain/list)頁面，以取得域名。 |

## 回應參數

此 API 在回應中僅傳回[公共參數](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

## 範例

### 請求範例

```json
POST https://open.byteplusapi.com/?Action=DeleteUserAgentAccessRule&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "Domain": "pull.example.com"
}
```

### 回應範例

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DeleteUserAgentAccessRule",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```

## 錯誤碼

以下是與目前操作相關的錯誤碼。若需其他錯誤碼，請參閱 [BytePlus OpenAPI 的通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。

|狀態碼 |錯誤碼 |錯誤訊息 |描述 |
|---|---|---|---|
|200 |CommonErr |\- |未分類錯誤。建議重試。如果仍傳回此錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |\- |輸入參數無效，或不符合要求。請參考[請求參數](https://docs.byteplus.com/en/docs/24/107298#request-parameters)描述進行檢查。 |
|400 |InvalidParam.BindError |Request parameter error, please check input data |參數驗證失敗。請檢查資料類型是否正確。 |
|403 |RequestForbidden |\- |請求遭拒，因為目前帳號下沒有請求的資源。資源包括域名空間、域名、應用程式名稱、設定和憑證。 |
|403 |RequestForbidden.AccountIDNotAllow |this AccountID does not have permission to access the corresponding resource, please check the request parameters |請求遭拒，因為目前帳號下沒有請求的資源。資源包括域名空間、域名、應用程式名稱、設定和憑證。 |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |影片直播服務尚未啟用，或帳號欠費，導致帳單不可用。請檢查服務啟用狀態和帳號欠費狀態。 |
|404 |ResourceNotFound |\- |找不到資源，包括域名空間、域名、應用程式名稱、設定和憑證。建議重試。如果仍傳回此錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|404 |ResourceNotFound.DomainNotExist |domain not found |找不到域名（Domain）。請檢查傳入的域名是否與實際使用的域名一致。 |
|500 |InternalError |an internal error occurred, please contact the administrator. |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |an internal error related to database occurred, please contact the administrator. |發生與資料庫相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |內部服務逾時。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
