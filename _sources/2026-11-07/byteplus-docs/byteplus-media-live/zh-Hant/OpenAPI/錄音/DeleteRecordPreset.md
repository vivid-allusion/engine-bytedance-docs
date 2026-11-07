---
title: "DeleteRecordPreset"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deleterecordpreset-2023-zh-TW"
---

調用 `DeleteRecordPreset` API 以刪除已建立的錄製配置。

<span id="Requirements"></span>
## 需求


* 頻率限制：每個帳戶每秒 1 次查詢。

* 生效說明：新增、更新及刪除錄製配置後，需在操作完成後（3\-5 分鐘）重新推流及拉流，才能使用變更後的配置。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=DeleteRecordPreset&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了專屬參數外，還必須帶上 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`DeleteRecordPreset` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Vhost |String |否 |`push.example.com` |域名空間。可調用 [ListVhostRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostrecordpresetv2-2023) API 取得待刪除配置的域名空間。 |
|App |String |否 |`live` |AppName 欄位。可調用 [ListVhostRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostrecordpresetv2-2023) API 取得待刪除配置的 AppName。 |
|Stream |String |否 |`example_stream` |StreamName 欄位。可調用 [ListVhostRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostrecordpresetv2-2023) API 取得待刪除配置的 StreamName。 |
|Preset |String |是 |`liverecord` |配置名稱。可調用 [ListVhostRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostrecordpresetv2-2023) API 取得待刪除配置的名稱。 |


<span id="Response parameters"></span>
## 回應參數

此 API 僅在回應中返回 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://open.byteplusapi.com/?Action=DeleteRecordPreset&Version=2023-01-01
{
    "Preset": "liverecord",
    "Vhost": "push.example.com",
    "App": "live"
}
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "202204081618570101742350380146D011",
        "Action": "DeleteRecordPreset",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "cn-north-1"
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為與本操作相關的錯誤碼。其他錯誤碼請參見 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**說明** |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回錯誤碼，請 [聯繫客服](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考 [請求參數](https://docs.byteplus.com/en/docs/24/107421#request-parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料型別是否正確。 |
|400 |InvalidParam.StillUsing |%s 仍在使用中，無法刪除 |錯誤訊息中指定的資源正在使用中，導致無法刪除。請釋放資源後再重試。 |
|403 |RequestForbidden |*  |請求被拒絕，因目前帳戶下無請求資源（資源包括域名空間、域名、App 名稱、配置及憑證）。 |
|403 |RequestForbidden.AccountIDNotAllow |此 AccountID 無權訪問對應資源，請檢查請求參數 |請求被拒絕，因目前帳戶下無請求資源（資源包括域名空間、域名、App 名稱、配置及憑證）。 |
|403 |RequestForbidden.BillingStatus |AccountID 的計費狀態不可用，請開通服務或充值。 |尚未開通視頻直播服務或帳戶欠費，導致計費不可用。請檢查服務開通狀態及帳戶欠費狀態。 |
|404 |ResourceNotFound |*  |未找到資源（包括域名空間、域名、App 名稱、配置及憑證）。建議重試。若仍返回錯誤碼，請 [聯繫客服](https://console.byteplus.com/workorder/create)。 |
|404 |ResourceNotFound.PresetNotExist |未找到預設 |未找到配置。請檢查傳入的配置是否與已建立的配置一致。 |
|429 |RequestLimitExceeded.Exist |%s 已存在 |請求建立的資源（包括網域名稱空間、網域名稱、應用名稱、配置、憑證）已存在。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.Preset |發生與預設相關的內部錯誤，請聯絡管理員。 |發生與預設相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
