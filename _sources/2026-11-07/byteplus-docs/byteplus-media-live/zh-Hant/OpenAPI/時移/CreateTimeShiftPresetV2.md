---
title: "CreateTimeShiftPresetV2"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createtimeshiftpresetv2-2023-zh-TW"
---

呼叫 `CreateTimeShiftPresetV2` API 以建立直播時移配置。完成直播時移配置後，使用者將能在直播過程中觀看先前已播出的內容。

<span id="Requirements"></span>
## 需求


* 先決條件：請確保已配置錄製任務，並為 AppName 選擇 HLS 儲存格式。

* 生效說明：新增、更新或刪除時移配置後，需於操作後（3\-5 分鐘）重新推流與拉流，以套用變更後的配置。

* 頻率限制：每個帳戶每秒僅可查詢 1 次。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=CreateTimeShiftPresetV2&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了專屬參數外，皆須帶入 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型態** |**必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`CreateTimeShiftPresetV2` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型態** |**必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |域名空間。可呼叫 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或於 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面取得該域名所屬的域名空間。 |
|App |String |是 |`live` |直播流 URL 中的 AppName 欄位。可包含大寫字母（A\-Z）、小寫字母（a\-z）、數字（0\-9）、底線（_）、連字號（\-）及句點（.），長度為 1 至 30 字元。 |
|MaxShiftTime |Integer |是 |`300` |時移時間，將直播流的可用時間延後指定秒數。例如，若將 `MaxShiftTime` 設為 `86400`，則直播流最長可於初次播出後一天內觀看。單位：秒。預設值為 `86400`。有效範圍：300–1296000。 |
|Type |String |是 |`tos` |儲存類型。請始終設為 `tos`。 |
|Bucket |String |否 |`bucket1` |TOS 儲存的 bucket。 |
|PullDomain |String |是 |`pull.example.com` |拉流用的域名。 |


<span id="Response parameters"></span>
## 回應參數

此 API 僅於回應中返回 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://open.byteplusapi.com/?Action=CreateTimeShiftPresetV2&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "App": "live",
    "MaxShiftTime": 86400,
    "PullDomain": "pull.example.com",
    "Bucket": "bucket1",
    "Type": "tos"
}
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "CreateTimeshiftPresetV2",
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
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回錯誤碼，請 [聯絡客服](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考 [請求參數](https://docs.byteplus.com/en/docs/24/107357#request-parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料型態是否正確。 |
|403 |RequestForbidden |*  |因當前帳戶下無請求資源（資源包含域名空間、域名、App 名稱、配置及憑證），故請求被拒絕。 |
|403 |RequestForbidden.AccountIDNotAllowed |此 AccountID 無權訪問對應資源，請檢查請求參數 |因當前帳戶下無請求資源（資源包含域名空間、域名、App 名稱、配置及憑證），故請求被拒絕。 |
|403 |RequestForbidden.BillingStatus |AccountID 的計費狀態不可用，請開通服務或充值。 |視訊直播服務尚未啟用或帳戶有欠費，導致帳單無法使用。請檢查服務啟用狀態及帳戶欠費狀態。 |
|404 |ResourceNotFound |*  |未找到資源（包括網域名稱空間、網域名稱、應用名稱、配置和憑證）。建議重試。如果仍返回錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|404 |ResourceNotFound.VhostNotExist |未找到 vhost |未找到網域名稱空間（Vhost）。請檢查傳入的網域名稱空間是否與實際使用中的網域名稱空間一致。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |發生與資料庫相關的內部錯誤，請聯絡管理員。 |發生與資料庫相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.VhostOrDomain |發生與 vhost 或網域相關的內部錯誤，請聯絡管理員。 |發生與網域名稱空間（Vhost）或網域名稱（Domain）相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
