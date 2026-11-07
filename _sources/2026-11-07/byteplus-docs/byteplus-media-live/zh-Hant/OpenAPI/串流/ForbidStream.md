---
title: "ForbidStream"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-forbidstream-2023-zh-TW"
---

呼叫 `ForbidStream` API 以停用直播串流。

<span id="Requirements"></span>
## 需求

頻率限制：每個帳戶每秒僅允許 1 次查詢。

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=ForbidStream&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了特定參數外，還必須搭配 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) 一同呼叫。

<span id="Query"></span>
### 查詢


|**參數** |**資料型態** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`ForbidStream` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型態** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Vhost |String |否 |`push.example.com` |該網域所屬的網域名稱空間。您可呼叫 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或於 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面取得網域名稱空間。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">僅需提供 <code>Vhost</code> 或 <code>Domain</code>，不可同時提供兩者。</div><br> |
|Domain |String |否 |`push.example.com` |網域名稱。您可呼叫 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或於 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面取得欲停用直播串流所使用的網域名稱。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">僅需提供 <code>Vhost</code> 或 <code>Domain</code>，不可同時提供兩者。</div><br> |
|App |String |是 |`live` |直播串流中的 AppName 欄位。可包含大寫字母（A\-Z）、小寫字母（a\-z）、數字（0\-9）、底線（_）、連字號（\-）及句點（.），長度為 1 至 30 字元。 |
|Stream |String |是 |`example_stream` |直播串流中的 StreamName 欄位。可包含大寫字母（A\-Z）、小寫字母（a\-z）、數字（0\-9）、底線（_）、連字號（\-）及句點（.），長度為 1 至 100 字元。 |
|EndTime |String |否 |`2021-04-14T00:00:01.000Z` |直播串流恢復的時間（RFC 3339 格式之 UTC 時間，精確至毫秒）。直播串流最多可停用 90 天。預設值為目前時間加 90 天。 |


<span id="Response parameters"></span>
## 回應參數

此 API 僅於回應中返回 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://open.byteplusapi.com/?Action=ForbidStream&Version=2023-01-01
{
    "Domain": "push.example.com",
    "App": "live",
    "Stream": "example_stream",
    "EndTime": "2021-04-14T00:00:01.000Z"
}
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "ForbidStream",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為與目前操作相關的錯誤碼。其他錯誤碼請參閱 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**說明** |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回錯誤碼，請 [聯絡客服](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參閱 [請求參數](https://docs.byteplus.com/en/docs/24/107248#request-parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料型態是否正確。 |
|400 |InvalidParam.Format |%s 格式錯誤 |參數格式不正確。請檢查錯誤訊息中指定參數是否有非法字元或 URL 格式錯誤。 |
|400 |InvalidParam.TimeLogic |startTime 晚於 endTime 等。 |傳入的時間參數不符合時間邏輯。請檢查是否存在以下問題：開始時間晚於結束時間。到期時間早於目前時間。 |
|403 |RequestForbidden |*  |請求被拒絕，因為當前帳戶下沒有請求的資源（資源包括網域名稱空間、網域名稱、應用名稱、配置和憑證）。 |
|403 |RequestForbidden.AccountIDNotAllowed |此 AccountID 無權存取對應資源，請檢查請求參數 |請求被拒絕，因為當前帳戶下沒有請求的資源（資源包括網域名稱空間、網域名稱、應用名稱、配置和憑證）。 |
|403 |RequestForbidden.BillingStatus |該 AccountID 未開通計費狀態，請啟用服務或充值。 |尚未啟用視訊直播服務或帳戶已欠費，導致帳單不可用。請檢查服務啟用狀態及帳戶欠費狀態。 |
|404 |ResourceNotFound |*  |未找到資源（包括網域名稱空間、網域名稱、應用名稱、配置和憑證）。建議重試。若仍返回錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |發生與資料庫相關的內部錯誤，請聯絡管理員。 |發生與資料庫相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.VhostOrDomain |發生與 vhost 或網域名稱相關的內部錯誤，請聯絡管理員。 |發生與網域名稱空間（Vhost）或網域名稱（Domain）相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
