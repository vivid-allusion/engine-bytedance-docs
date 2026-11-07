---
title: "DeleteWatermarkPreset"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletewatermarkpreset-2023-zh-TW"
---

呼叫 `DeleteWatermarkPreset` API 以刪除現有的浮水印配置。

<span id="Requirements"></span>
## 需求


* 頻率限制：每個帳戶每秒 1 次查詢。

* 生效時間：新增、更新或刪除浮水印配置後，變更將於 3 至 5 分鐘內生效。變更生效後產生的轉碼串流或 ABR（自適應碼率）子串流將使用最新的浮水印配置。在變更生效前產生的現有轉碼串流或 ABR 子串流不會自動套用更新。若在變更前不存在任何轉碼串流或 ABR 子串流，請等待配置生效。若在變更前已存在轉碼串流或 ABR 子串流且需要使用更新後的配置，請於配置新增、更新或刪除後等待 3 至 5 分鐘，再重新推送串流。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=DeleteWatermarkPreset&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了需傳入 API 專屬參數外，還必須包含 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型態** |**是否必填** |**範例值** |**描述** |
|---|---|---|---|---|
|Action |String |是 |`DeleteWatermarkPreset` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型態** |**是否必填** |**範例值** |**描述** |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |網域名稱空間。可呼叫 [ListVhostWatermarkPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostwatermarkpreset-2023) API 取得配置的網域名稱空間，作為 `Vhost` 參數值。 |
|App |String |是 |`live` |直播串流 URL 中的 `AppName` 欄位。可呼叫 [ListVhostWatermarkPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostwatermarkpreset-2023) API 取得配置的 `AppName`，作為 `App` 參數值。 |
|Stream |String |否 |`example_stream` |直播串流 URL 中的 `StreamName` 欄位。可呼叫 [ListVhostWatermarkPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostwatermarkpreset-2023) API 取得配置的 `StreamName`，作為 `Stream` 參數值。 |


<span id="Response parameters"></span>
## 回應參數

此 API 僅於回應中返回 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://open.byteplusapi.com/?Action=DeleteWatermarkPreset&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "App": "live"
}
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "DeleteWatermarkPreset",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為與本操作相關的錯誤碼。其他錯誤碼請參見 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**描述** |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回錯誤碼，請 [聯絡客服](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考 [請求參數](https://docs.byteplus.com/en/docs/24/107321#request-parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料型態是否正確。 |
|400 |InvalidParam.StillUsing |%s 仍在使用中，無法刪除 |錯誤訊息中指定的資源正在使用中，導致無法刪除。請釋放資源後再重試。 |
|403 |RequestForbidden |*  |因目前帳戶下無請求資源（資源包括網域名稱空間、網域名稱、App 名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.AccountIDNotAllowed |此 AccountID 無權存取對應資源，請檢查請求參數 |因目前帳戶下無請求資源（資源包括網域名稱空間、網域名稱、App 名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.BillingStatus |無法取得該 AccountID 的帳單狀態，請啟用服務或儲值。 |視訊直播服務尚未啟用或帳戶欠費，導致無法取得帳單。請檢查服務啟用狀態及帳戶欠費狀態。 |
|404 |ResourceNotFound |*  |未找到資源（包括域名空間、域名、應用名稱、配置和憑證）。建議重試。若仍返回錯誤碼，請[聯繫技術支援](https://console.byteplus.com/workorder/create)。 |
|404 |ResourceNotFound.PresetNotExist |未找到預設。 |未找到配置。請檢查傳入的配置是否與已建立的配置一致。 |
|500 |InternalError |發生內部錯誤，請聯繫管理員。 |發生內部錯誤。請[聯繫技術支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.Preset |發生與預設相關的內部錯誤，請聯繫管理員。 |發生與預設相關的內部錯誤。請[聯繫技術支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯繫管理員。 |發生內部錯誤。請[聯繫技術支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯繫管理員。 |發生內部錯誤。請[聯繫技術支援](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯繫管理員。 |內部服務逾時。請[聯繫技術支援](https://console.byteplus.com/workorder/create)。 |
