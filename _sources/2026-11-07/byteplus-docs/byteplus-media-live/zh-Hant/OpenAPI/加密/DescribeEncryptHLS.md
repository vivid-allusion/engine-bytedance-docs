---
title: "DescribeEncryptHLS"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeencrypthls-zh-TW"
---

呼叫 `DescribeEncryptHLS` API，以查詢用於 HLS 標準加密的自主管理金鑰管理服務地址，以及金鑰更新週期。

<span id="Requirements"></span>
## 需求

頻率限制：每個帳戶每秒僅允許 1 次查詢。

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=DescribeEncryptHLS&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了專屬參數外，還必須帶上 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型態** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`DescribeEncryptHLS` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Response parameters"></span>
## 回應參數

有關專屬於此 API 的回應參數，請參見下表。更多細節請參考 [請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 章節。


|**參數** |**資料型態** |**範例值** |**說明** |
|---|---|---|---|
|URL |String |`http://example.kms.com/get_key?` |在建立自有金鑰管理服務後，客戶端會請求該地址以從金鑰管理服務取得金鑰。 |
|CycleTime |Float |`60` |視訊直播伺服器產生金鑰的更新週期，以秒為單位，值範圍為 [60,604800]。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeEncryptHLS",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "cn-north-1"
    },
    "Result": {
        "URL": "http://example.kms.com/get_key?",
        "CycleTime": 60
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為與本操作相關的錯誤碼。其他錯誤碼請參見 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**說明** |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回錯誤碼，請 [聯絡客服](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考 [請求參數](https://docs.byteplus.com/en/docs/24/107339#request-parameters) 說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料型態是否正確。 |
|403 |RequestForbidden |*  |因目前帳戶下無請求資源（資源包括網域名稱空間、網域名稱、App 名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.AccountIDNotAllow |此 AccountID 無權存取對應資源，請檢查請求參數 |因目前帳戶下無請求資源（資源包括網域名稱空間、網域名稱、App 名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.BillingStatus |AccountID 的帳單狀態不可用，請啟用服務或儲值。 |尚未啟用視訊直播服務或帳戶欠費，導致帳單不可用。請檢查服務啟用狀態及帳戶欠費狀態。 |
|404 |ResourceNotFound |*  |未找到資源（包括網域名稱空間、網域名稱、App 名稱、配置及憑證）。建議重試。若仍返回錯誤碼，請 [聯絡客服](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請 [聯絡客服](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|500 |InternalError.DB |發生與資料庫相關的內部錯誤，請聯絡管理員。 |發生內部錯誤。請 [聯絡客服](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請 [聯絡客服](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請 [聯絡客服](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請[聯絡客服](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
