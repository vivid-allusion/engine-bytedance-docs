---
title: "DeleteCallback"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletecallback-2023-zh-TW"
---

呼叫 `DeleteCallback` API 以刪除回調配置。

<span id="Requirements"></span>
## 需求

頻率限制：每個帳戶每秒 1 次查詢。

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=DeleteCallback&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了需傳遞 API 專屬參數外，還必須帶上 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`DeleteCallback` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Vhost |String |否 |`push.live.example.com` |域名空間。可呼叫 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或在 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面取得該域名所屬的域名空間。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">若在新增回調配置時指定 <code>Vhost</code> 而非 <code>Domain</code>，刪除時也需同樣指定。</div><br> |
|Domain |String |否 |`push.live.example.com` |推流用的域名。可呼叫 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或在 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面取得域名。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">若在新增回調配置時指定 <code>Domain</code> 而非 <code>Vhost</code>，刪除時也需同樣指定。</div><br> |
|App |String |否 |`example_app` |直播串流 URL 中的 AppName 欄位。可包含大寫字母（A\-Z）、小寫字母（a\-z）、數字（0\-9）、底線（_）、連字號（\-）及點（.），長度為 1 至 30 字元。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">若指定 <code>Vhost</code> 並未指定 <code>App</code>，則會移除該域名空間下所有回調配置。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">若指定 <code>Domain</code>，則不可指定 <code>App</code>。</div><br> |
|MessageType |String |否 |`push` |要接收的回調訊息類型。有效值包括：<br><br><br>* `push`：推流開始時觸發回調。<br><br>* `push_end`：推流結束時觸發回調。<br><br>* `snapshot`：截圖事件發生時觸發回調。<br><br>* `record`：錄製事件發生時觸發回調。 |


<span id="Response parameters"></span>
## 回應參數

此 API 僅在回應中返回 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://open.byteplusapi.com/?Action=DeleteCallback&Version=2023-01-01
{
    "App": "live",
    "Domain": "",
    "MessageType": "push",
    "Vhost": "push.example.com"
}
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "DeleteCallback",
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
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回錯誤碼，請 [聯絡客服](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考 [請求參數](https://docs.byteplus.com/en/docs/24/107359#request-parameters)說明進行校驗。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數校驗未通過。請檢查資料型別是否正確。 |
|400 |InvalidParam.OutOfRange |%s 應為 {[%s]} 之一，%s 應介於 %d 與 %d 之間 |參數超出允許範圍。請檢查錯誤訊息中指定參數的值是否超出範圍。 |
|403 |RequestForbidden |*  |因當前帳戶下無請求資源（資源包括域名空間、域名、App 名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.AccountIDNotAllow |此 AccountID 無權訪問對應資源，請檢查請求參數 |請求被拒絕，因為當前帳戶下沒有請求的資源（資源包括網域名稱空間、網域名稱、應用名稱、配置和憑證）。 |
|403 |RequestForbidden.BillingStatus |無法取得該 AccountID 的計費狀態，請啟用服務或儲值。 |尚未啟用視訊直播服務或帳戶存在欠費，導致無法取得帳單。請檢查服務啟用狀態及帳戶欠費狀態。 |
|404 |ResourceNotFound |*  |未找到資源（包括網域名稱空間、網域名稱、應用名稱、配置和憑證）。建議重試。若仍返回錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|404 |ResourceNotFound.VhostNotExist |未找到 vhost |未找到網域名稱空間（Vhost）。請檢查傳入的網域名稱空間是否與實際使用中的網域名稱空間一致。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |發生與資料庫相關的內部錯誤，請聯絡管理員。 |發生與資料庫相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
