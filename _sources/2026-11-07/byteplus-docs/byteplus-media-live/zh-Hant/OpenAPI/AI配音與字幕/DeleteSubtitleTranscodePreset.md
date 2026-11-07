---
title: "DeleteSubtitleTranscodePreset"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletesubtitletranscodepreset-2023-zh-TW"
---

調用 `DeleteSubtitleTranscodePreset` API 以刪除已新增的字幕配置。

<span id="Requirements"></span>
## 需求


* **速率限制**：每個帳號每秒 10 次請求。

* **生效時間**：新增、編輯或刪除字幕配置後，需等待 3 至 5 分鐘並重新啟動推流，變更才會生效。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=DeleteSubtitleTranscodePreset&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 呼叫時，除了 API 專屬參數外，還必須包含 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`DeleteSubtitleTranscodePreset` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。當前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |域名空間。可調用 [ListVhostSubtitleTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostsubtitletranscodepreset-2023) API 以獲取要刪除字幕配置的 `Vhost` 值。 |
|App |String |是 |`live` |`AppName`。可調用 [ListVhostSubtitleTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostsubtitletranscodepreset-2023) API 以獲取要刪除字幕配置的 `App` 值。 |
|PresetName |String |是 |`OriginPreset` |字幕配置名稱。可調用 [ListVhostSubtitleTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostsubtitletranscodepreset-2023) API 以獲取要刪除字幕配置的 `PresetName` 值。 |


<span id="Response parameters"></span>
## 回應參數

此 API 僅在回應中返回 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```json
POST https://open.byteplusapi.com/?Action=DeleteSubtitleTranscodePreset&Version=2023-01-01
{
    "App": "live",
    "Vhost": "push.example.com",
    "PresetName": "OriginPreset"
}
```


<span id="Sample response"></span>
### 回應範例

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DeleteSubtitleTranscodePreset",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為本操作相關的錯誤碼。其他錯誤碼請參見 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**說明** |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回錯誤碼，請 [聯繫支援](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考 [請求參數](https://docs.byteplus.com/en/docs/24/107266#request-parameters) 說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料型別是否正確。 |
|400 |InvalidParam.StillUsing |%s 仍在使用中，無法刪除 |錯誤訊息中指定的資源正在使用中，導致無法刪除。請釋放資源後重試。 |
|403 |RequestForbidden |*  |請求被拒絕，因當前帳號下無請求資源（資源包括域名空間、域名、App 名稱、配置及憑證）。 |
|403 |RequestForbidden.AccountIDNotAllow |此 AccountID 無權訪問對應資源，請檢查請求參數 |請求被拒絕，因當前帳號下無請求資源（資源包括域名空間、域名、App 名稱、配置及憑證）。 |
|403 |RequestForbidden.BillingStatus |該 AccountID 尚未啟用計費功能，請開通服務或充值。 |尚未開通視頻直播服務或帳號欠費，導致計費不可用。請檢查服務開通狀態及帳號欠費狀態。 |
|404 |ResourceNotFound |*  |未找到資源（包括域名空間、域名、App 名稱、配置及憑證）。建議重試。若仍返回錯誤碼，請 [聯繫支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |發生內部錯誤，請聯繫管理員。 |發生內部錯誤。請 [聯繫支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.Preset |發生與預設相關的內部錯誤，請聯絡管理員。 |發生與預設相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務已逾時。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
