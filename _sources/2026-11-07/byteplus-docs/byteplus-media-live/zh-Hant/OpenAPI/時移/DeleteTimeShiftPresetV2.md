---
title: "DeleteTimeShiftPresetV2"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletetimeshiftpresetv2-2023-zh-TW"
---

呼叫 `DeleteTimeShiftPresetV2` API 以刪除已建立的時移配置。

<span id="Requirements"></span>
## 需求


* 生效說明：新增、更新及刪除時移配置後，需在操作完成（3\-5分鐘）後重新推流及拉流，才能使用變更後的配置。

* 頻率限制：每個帳戶每秒僅可查詢 1 次。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=DeleteTimeShiftPresetV2&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了專屬參數外，還必須帶上 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Headers"></span>
### 標頭


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Content\-Type |字串 |是 |`application/json` |請求 Body 的 MIME 類型。 |


<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |字串 |是 |`DeleteTimeShiftPresetV2` |API 操作名稱。 |
|Version |字串 |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Vhost |字串 |是 |`push.example.com` |域名空間。可呼叫 [ListTimeShiftPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listtimeshiftpresetv2-2023) API 取得配置的域名空間。 |
|App |字串 |是 |`live` |AppName 欄位。可呼叫 [ListTimeShiftPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listtimeshiftpresetv2-2023) API 取得配置的 AppName。 |
|Preset |字串 |是 |`preset-test` |配置名稱。可呼叫 [ListTimeShiftPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listtimeshiftpresetv2-2023) API 取得配置名稱。 |


<span id="Response parameters"></span>
## 回應參數

此 API 僅在回應中返回 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://open.byteplusapi.com/?Action=DeleteTimeShiftPresetV2&Version=2023-01-01
Content-Type: application/json
{
    "Vhost": "push.example.com",
    "App": "live",
    "Preset": "preset-test"
}
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "Action": "DeleteTimeShiftPresetV2",
        "Region": "ap-singapore-1",
        "Service": "live",
        "Version": "2023-01-01",
        "RequestId": "202306041104200100100232280022D31"
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為與本操作相關的錯誤碼。其他錯誤碼請參見 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**說明** |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回錯誤碼，請 [聯繫客服](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考 [請求參數](https://docs.byteplus.com/en/docs/24/107448#request-parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料型別是否正確。 |
|403 |RequestForbidden |*  |因當前帳戶下無請求資源（資源包括域名空間、域名、App 名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.AccountIDNotAllowed |此 AccountID 無權訪問對應資源，請檢查請求參數 |因當前帳戶下無請求資源（資源包括域名空間、域名、App 名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.BillingStatus |AccountID 的計費狀態不可用，請開通服務或充值。 |未啟用視頻直播服務或帳戶欠費，導致帳單不可用。請檢查服務開通狀態及帳戶欠費狀態。 |
|404 |ResourceNotFound |*  |未找到資源（包括域名空間、域名、App 名稱、配置及憑證）。建議重試。若仍返回錯誤碼，請 [聯繫客服](https://console.byteplus.com/workorder/create)。 |
|404 |ResourceNotFound.VhostNotExist |未找到 vhost |未找到域名空間（Vhost）。請檢查傳入的域名空間是否與實際使用的域名空間一致。 |
|500 |InternalError |發生內部錯誤，請聯繫管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |發生與資料庫相關的內部錯誤，請聯絡管理員。 |發生與資料庫相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.VhostOrDomain |發生與虛擬主機或網域相關的內部錯誤，請聯絡管理員。 |發生與網域名稱空間（Vhost）或網域名稱（Domain）相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
