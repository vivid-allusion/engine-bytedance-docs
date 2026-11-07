---
title: "UpdateTimeShiftPresetV2"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatetimeshiftpresetv2-2023-zh-TW"
---

呼叫 `UpdateTimeShiftPresetV2` API，以更新已建立的時移配置。

<span id="Requirements"></span>
## 需求


* 生效說明：新增、更新及刪除時移配置後，需於操作完成（3\-5分鐘）後重新推流及拉流，才能使用變更後的配置。

* 頻率限制：每個帳戶每秒最多查詢 1 次。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=UpdateTimeShiftPresetV2&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了專屬參數外，還必須帶上 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Headers"></span>
### 標頭


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Content\-Type |字串 |是 |`application/json` |請求 body 的 MIME 類型。 |


<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |字串 |是 |`UpdateTimeShiftPresetV2` |API 操作名稱。 |
|Version |字串 |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Vhost |字串 |是 |`push.example.com` |網域名稱空間。可呼叫 [ListTimeShiftPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listtimeshiftpresetv2-2023) API 取得配置的網域名稱空間。 |
|App |字串 |是 |`live` |AppName 欄位。可呼叫 [ListTimeShiftPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listtimeshiftpresetv2-2023) API 取得配置的 AppName。 |
|Preset |字串 |是 |`preset-test` |配置名稱。可呼叫 [ListTimeShiftPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listtimeshiftpresetv2-2023) API 取得配置名稱。 |
|MaxShiftTime |整數 |是 |`3000` |時移時間，將直播流的可用時間延後指定秒數。例如，若將 `MaxShiftTime` 設為 `86400`，則直播流最晚可於初次播出後一天內觀看。單位：秒。預設值為 `86400`。有效範圍：300–1296000。 |
|Type |字串 |是 |`tos` |儲存類型。請始終設為 `tos`。 |


<span id="Response parameters"></span>
## 回應參數

此 API 僅於回應中返回 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://open.byteplusapi.com/?Action=UpdateTimeShiftPresetV2&Version=2023-01-01
Content-Type: application/json
{
    "Vhost": "push.example.com",
    "App": "live",
    "MaxShiftTime": 86400,
    "Preset": "preset-test",
    "Type": "tos"
}
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1",
        "Action": "UpdateTimeShiftPresetV2",
        "RequestId": "202306041104200100100232280022D31"
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為本操作相關的錯誤碼。其他錯誤碼請參見 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**說明** |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回錯誤碼，請 [聯繫客服](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考 [請求參數](https://docs.byteplus.com/en/docs/24/107346#request-parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料型別是否正確。 |
|403 |RequestForbidden |*  |因當前帳戶下無請求資源（資源包含網域名稱空間、網域名稱、App 名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.AccountIDNotAllowed |此 AccountID 無權存取對應資源，請檢查請求參數 |因當前帳戶下無請求資源（資源包含網域名稱空間、網域名稱、App 名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.BillingStatus |此 AccountID 未開通計費狀態，請啟用服務或儲值。 |尚未開通視頻直播服務或帳戶欠費，導致帳單不可用。請檢查服務開通狀態及帳戶欠費狀態。 |
|404 |ResourceNotFound |*  |未找到資源（包括網域名稱空間、網域名稱、應用名稱、配置及憑證）。建議重試。若仍返回錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|404 |ResourceNotFound.VhostNotExist |未找到 vhost。 |未找到網域名稱空間（Vhost）。請檢查傳入的網域名稱空間是否與實際使用的網域名稱空間一致。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |發生與資料庫相關的內部錯誤，請聯絡管理員。 |發生與資料庫相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.VhostOrDomain |發生與 vhost 或網域相關的內部錯誤，請聯絡管理員。 |發生與網域名稱空間（Vhost）或網域名稱（Domain）相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
