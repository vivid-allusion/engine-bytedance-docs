---
title: "UpdateUserAgentAccessRule"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updateuseragentaccessrule-zh-TW"
---

呼叫 `UpdateUserAgentAccessRule` API，以新增或更新 User\-Agent 限制。

## 要求

速率限制：每個帳戶每秒 10 次查詢。

## HTTP 請求

* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=UpdateUserAgentAccessRule&Version=2023\-01\-01

## 請求參數

### 通用參數

所有 API 除了 API 專屬參數外，還必須使用[通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)呼叫。

### 查詢

|參數 |資料類型 |必填 |範例值 |說明 |
|---|---|---|---|---|
|Action |String |是 |`UpdateUserAgentAccessRule` |API 操作。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |

### 主體參數

|參數 |資料類型 |必填 |範例值 |說明 |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |網域名稱空間。你可以呼叫 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或前往 BytePlus MediaLive 主控台中的[網域](https://console.byteplus.com/live/main/domain/list)頁面，以取得網域名稱空間。 |
|Domain |String |是 |`pull.example.com` |用於拉流的網域名稱。你可以呼叫 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或前往 BytePlus MediaLive 主控台中的[網域](https://console.byteplus.com/live/main/domain/list)頁面，以取得網域名稱。 |
|UaAccessRule |[UaAccessRule](https://docs.byteplus.com/en/docs/24/107327#uaaccessrule) 物件 |是 |`-` |UA 封鎖清單或允許清單詳細資料。 |

### UaAccessRule

|參數 |資料類型 |必填 |範例值 |說明 |
|---|---|---|---|---|
|AllowEmpty |Boolean |是 |`true` |指定是否將組態套用至包含空 UA 標頭，或不包含 UA 標頭的請求。例如，如果你將 **Type** 設為 **deny**，並將 **AllowEmpty** 設為 **true**，則包含空 UA 標頭或不包含 UA 標頭的請求會遭到拒絕。<br><br><br>* `true`：套用。<br><br>* `false`：不套用。 |
|Type |String |是 |`deny` |限制類型。<br><br><br>* `allow`：允許清單。<br><br>* `deny`：封鎖清單。 |
|Enable |Boolean |是 |`true` |指定是否啟用 UA 允許清單或封鎖清單。<br><br><br>* `true`：啟用。<br><br>* `false`：停用。 |
|UserAgent |String 陣列 |是 |`["Mozilla/5.0","*curl*"]` |封鎖清單或允許清單中的 UA 標頭清單。組態長度不能超過 30,000 個字元。你最多可以輸入 1,000 個 UA 標頭。<br><br><br>* UA 標頭區分大小寫。<br><br>* 你可以使用萬用字元 (\*) 表示任意數量的字元。 `*` 只能出現在 UA 標頭的開頭或結尾。你可以在 UA 標頭的開頭和結尾都新增 `*`，例如 `*curl*`。<br><br>* UA 標頭不能是 `*`。<br><br>* UA 標頭不能包含 `**`。<br><br>* UA 標頭只能包含可列印的 ASCII 字元，但 Delete（ASCII 碼 127）除外。<br><br>* UA 標頭不能只包含空格。 |

## 回應參數

此 API 在回應中只會傳回[通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

## 範例

### 範例請求

```json
POST https://open.byteplusapi.com/?Action=UpdateUserAgentAccessRule&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "Domain": "pull.example.com",
    "UaAccessRule": {
        "AllowEmpty": true,
        "Type": "deny",
        "Enable": true,
        "UserAgent": [
            "Mozilla/5.0",
            "*curl*"
        ]
    }
}
```

### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "UpdateUserAgentAccessRule",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```

## 錯誤碼

以下是與目前操作相關的錯誤碼。如需其他錯誤碼，請參閱 [BytePlus OpenAPI 的通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。

|狀態碼 |錯誤碼 |錯誤訊息 |說明 |
|---|---|---|---|
|200 |CommonErr |\- |未分類錯誤。建議重試。如果仍傳回此錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |\- |輸入參數無效或不符合要求。請參閱[請求參數](https://docs.byteplus.com/en/docs/24/107327#request-parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |Request parameter error, please check input data |參數驗證失敗。請檢查資料類型是否正確。 |
|403 |RequestForbidden |\- |請求遭到拒絕，因為目前帳戶下沒有請求的資源。資源包括網域名稱空間、網域名稱、應用程式名稱、組態和憑證。 |
|403 |RequestForbidden.AccountIDNotAllow |this AccountID does not have permission to access the corresponding resource, please check the request parameters |請求遭到拒絕，因為目前帳戶下沒有請求的資源。資源包括網域名稱空間、網域名稱、應用程式名稱、組態和憑證。 |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |視訊直播服務尚未啟用，或帳戶欠費，導致帳單不可用。請檢查服務啟用狀態和帳戶欠費狀態。 |
|404 |ResourceNotFound |\- |找不到資源。資源包括網域名稱空間、網域名稱、應用程式名稱、組態和憑證。建議重試。如果仍傳回此錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|404 |ResourceNotFound.DomainNotExist |domain not found |找不到網域名稱（Domain）。請檢查傳入的網域名稱是否與實際使用的網域名稱一致。 |
|500 |InternalError |an internal error occurred, please contact the administrator. |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |an internal error related to database occurred, please contact the administrator. |發生資料庫相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |內部服務逾時。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
