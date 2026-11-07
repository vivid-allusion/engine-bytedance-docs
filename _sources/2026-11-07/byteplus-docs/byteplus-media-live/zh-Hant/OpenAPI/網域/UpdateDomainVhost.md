---
title: "UpdateDomainVhost"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatedomainvhost-zh-TW"
---

呼叫 `UpdateDomainVhost` API，以變更與該網域名稱關聯的網域名稱空間。

<span id="Requirements"></span>
## 需求

頻率限制：每個帳戶每秒最多 10 次查詢。

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=UpdateDomainVhost&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了需傳入 API 專屬參數外，還必須傳入 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型態** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`UpdateDomainVhost` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型態** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Domain |String |是 |`push.example.com` |欲變更關聯網域名稱空間的網域名稱。 |
|Vhost |String |是 |`push.example.com` |要與網域名稱關聯的新網域名稱空間。 |


<span id="Response parameters"></span>
## 回應參數

此 API 僅在回應中返回 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://open.byteplusapi.com/?Action=UpdateDomainVhost&Version=2023-01-01
{
    "Domain": "push.example.com",
    "Vhost": "push.example.com"
}
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "202306041104200100100232280022D31",
        "Action": "UpdateDomainVhost",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為與目前操作相關的錯誤碼。其他錯誤碼請參見 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**說明** |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回錯誤碼，請 [聯絡客服](https://docs.byteplus.com/en/docs/24/%5B++https://console.byteplus.com/workorder/create++%5D(https://console.byteplus.com/workorder/create))。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考 [請求參數](https://docs.byteplus.com/en/docs/24/107254#request-parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料型態是否正確。 |
|400 |InvalidParam.Format |%s 格式錯誤 |參數格式不正確。請檢查錯誤訊息中指定的參數是否有非法字元或 URL 格式錯誤。 |
|403 |RequestForbidden |*  |因目前帳戶下無請求資源（資源包括網域名稱空間、網域名稱、App 名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.AccountIDNotAllow |此 AccountID 無權存取對應資源，請檢查請求參數 |因目前帳戶下無請求資源（資源包括網域名稱空間、網域名稱、App 名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.BillingStatus |AccountID 的帳單狀態不可用，請開通服務或充值。 |尚未開通視頻直播服務或帳戶欠費，導致帳單不可用。請檢查服務開通狀態及帳戶欠費狀態。 |
|404 |ResourceNotFound |*  |未找到資源（包括網域名稱空間、網域名稱、App 名稱、配置及憑證）。建議重試。若仍返回錯誤碼，請 [聯絡客服](https://console.byteplus.com/workorder/create)。 |
|404 |ResourceNotFound.DomainNotExist |未找到網域名稱 |未找到網域名稱（Domain）。請檢查傳入的網域名稱是否與實際使用的網域名稱一致。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請 [聯絡客服](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |發生與資料庫相關的內部錯誤，請聯絡管理員。 |發生與資料庫相關的內部錯誤。請 [聯絡客服](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請 [聯絡客服](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|504 |內部服務逾時 |內部服務逾時。請聯絡管理員。 |內部服務逾時。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
