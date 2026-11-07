---
title: "UpdateFormatAccessRule"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updateformataccessrule-zh-TW"
---

呼叫 `UpdateFormatAccessRule` API 以建立協定限制。

## 要求

速率限制：每個帳號每秒 10 次查詢。

## HTTP 請求

* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=UpdateFormatAccessRule&Version=2023\-01\-01

## 請求參數

### 通用參數

除 API 專屬參數外，呼叫所有 API 時都必須帶上[通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

### 查詢

|參數 |資料類型 |必填 |範例值 |描述 |
|---|---|---|---|---|
|Action |String |是 |`UpdateFormatAccessRule` |API 操作。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |

### 主體參數

|參數 |資料類型 |必填 |範例值 |描述 |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |網域名稱空間。您可以呼叫 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或造訪 BytePlus MediaLive 控制台中的[網域](https://console.byteplus.com/live/main/domain/list)頁面，以取得網域名稱空間。 |
|Domain |String |是 |`pull.example.com` |用於拉流的網域名稱。您可以呼叫 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或造訪 BytePlus MediaLive 控制台中的[網域](https://console.byteplus.com/live/main/domain/list)頁面，以取得網域名稱。 |
|FormatAccessRule |[FormatAccessRule](https://docs.byteplus.com/en/docs/24/107293#formataccessrule) 的物件 |是 |`-` |協定限制詳細資料。 |

### FormatAccessRule

|參數 |資料類型 |必填 |範例值 |描述 |
|---|---|---|---|---|
|Type |String |是 |`deny` |存取控制的類型。唯一支援的值為 `deny`，會封鎖透過封鎖清單中協定進行的拉流。 |
|Enable |Boolean |是 |`true` |是否啟用此設定。<br><br><br>* `true`：啟用此設定。<br><br>* `false`：停用此設定。 |
|FormatList |Array of String |是 |`["flv"]` |協定清單。有效選項包括：<br><br><br>* `flv`<br><br>* `hls`<br><br>* `rtmp`<br><br>* `webrtc`，表示 RTM 協定 |

## 回應參數

此 API 只會在回應中傳回[通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

## 範例

### 範例請求

```json
POST https://open.byteplusapi.com/?Action=UpdateFormatAccessRule&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "Domain": "pull.example.com",
    "FormatAccessRule": {
        "Type": "deny",
        "Enable": true,
        "FormatList": [
            "flv"
        ]
    }
}
```

### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "UpdateFormatAccessRule",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```

## 錯誤碼

以下是與目前操作相關的錯誤碼。如需其他錯誤碼，請參閱 [BytePlus OpenAPI 的通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。

|狀態碼 |錯誤碼 |錯誤訊息 |描述 |
|---|---|---|---|
|200 |CommonErr |\- |未分類錯誤。建議重試。如果仍傳回此錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |\- |輸入參數無效或不符合要求。請參閱[請求參數](https://docs.byteplus.com/en/docs/24/107293#request-parameters)描述進行檢查。 |
|400 |InvalidParam.BindError |Request parameter error, please check input data |參數驗證失敗。請檢查資料類型是否正確。 |
|403 |RequestForbidden |\- |由於目前帳號下沒有請求的資源，請求被拒絕。資源包括網域名稱空間、網域名稱、應用程式名稱、設定和憑證。 |
|403 |RequestForbidden.AccountIDNotAllow |this AccountID does not have permission to access the corresponding resource, please check the request parameters |由於目前帳號下沒有請求的資源，請求被拒絕。資源包括網域名稱空間、網域名稱、應用程式名稱、設定和憑證。 |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |影片直播服務尚未啟用，或帳號欠費，導致帳單不可用。請檢查服務啟用狀態和帳號欠費狀態。 |
|404 |ResourceNotFound |\- |找不到資源。資源包括網域名稱空間、網域名稱、應用程式名稱、設定和憑證。建議重試。如果仍傳回此錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|404 |ResourceNotFound.DomainNotExist |domain not found |找不到網域名稱（Domain）。請檢查傳入的網域名稱是否與實際使用的網域名稱一致。 |
|500 |InternalError |an internal error occurred, please contact the administrator. |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |an internal error related to database occurred, please contact the administrator. |發生與資料庫相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |內部服務逾時。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
