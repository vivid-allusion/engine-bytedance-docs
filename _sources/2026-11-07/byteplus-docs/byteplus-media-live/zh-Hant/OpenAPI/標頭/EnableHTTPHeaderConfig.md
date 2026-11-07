---
title: "EnableHTTPHeaderConfig"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-enablehttpheaderconfig-zh-TW"
---

調用 `EnableHTTPHeaderConfig` API 以啟用或停用 HTTP 標頭配置。

<span id="Requirements"></span>
## 需求

速率限制：每個帳號每秒 10 次查詢。

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=EnableHTTPHeaderConfig&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了 API 專屬參數外，還必須帶上 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`EnableHTTPHeaderConfig` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。當前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Vhost |String |是 |`example` |域名空間。可調用 [DescribeHTTPHeaderConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describehttpheaderconfig) API 以獲取待啟用或停用配置的域名空間值。 |
|Domain |String |否 |`example.com` |拉流域名。可調用 [DescribeHTTPHeaderConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describehttpheaderconfig) API 以獲取待啟用或停用配置的域名值。 |
|Phase |Integer |是 |`0` |HTTP 標頭配置的類型。可調用 [DescribeHTTPHeaderConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describehttpheaderconfig) API 以獲取待啟用或停用配置的類型值。<br><br><br>* `0`：響應標頭。<br><br>* `1`：請求標頭。 |
|Enable |Boolean |是 |`true` |是否啟用該配置。<br><br><br>* `true`：啟用<br><br>* `false`：停用 |


<span id="Response parameters"></span>
## 響應參數

此 API 僅在響應中返回 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```json
POST https://open.byteplusapi.com/?Action=EnableHTTPHeaderConfig&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "Phase": 0,
    "Enable": true,
    "Domain": "pull.example.com"
}
```


<span id="Sample response"></span>
### 響應範例

```json
{
    "ResponseMetadata": {
        "RequestId": "202306041104200100100232280022D31",
        "Action": "EnableHTTPHeaderConfig",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為與本次操作相關的錯誤碼。其他錯誤碼請參見 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**說明** |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回錯誤碼，請 [聯繫支援](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考 [請求參數](https://docs.byteplus.com/en/docs/24/107438#request-parameters) 說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料型別是否正確。 |
|400 |InvalidParam.DomainAndApp |domain 和 app 不能同時存在 |不可同時傳入 Domain 與 App。請修改輸入參數。 |
|403 |RequestForbidden |*  |請求被拒絕，因當前帳號下無請求資源（資源包括域名空間、域名、App 名稱、配置及憑證）。 |
|403 |RequestForbidden.AccountIDNotAllow |此 AccountID 無權訪問對應資源，請檢查請求參數 |請求被拒絕，因當前帳號下無請求資源（資源包括域名空間、域名、App 名稱、配置及憑證）。 |
|403 |RequestForbidden.BillingStatus |該 AccountID 未開通計費狀態，請開通服務或充值。 |未開通視訊直播服務或帳號欠費，導致計費不可用。請檢查服務開通狀態及帳號欠費狀態。 |
|404 |ResourceNotFound |*  |未找到資源（包括域名空間、域名、App 名稱、配置及憑證）。建議重試。若仍返回錯誤碼，請 [聯繫支援](https://console.byteplus.com/workorder/create)。 |
|404 |ResourceNotFound.DomainNotExist |未找到 domain |未找到域名（Domain）。請檢查傳入的網域名稱是否與實際使用中的網域名稱一致。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |發生與資料庫相關的內部錯誤，請聯絡管理員。 |發生與資料庫相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
