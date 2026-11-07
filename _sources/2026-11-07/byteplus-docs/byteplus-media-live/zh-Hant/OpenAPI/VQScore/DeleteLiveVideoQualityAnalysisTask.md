---
title: "DeleteLiveVideoQualityAnalysisTask"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletelivevideoqualityanalysistask-2023-zh-TW"
---

調用 `DeleteLiveVideoQualityAnalysisTask` API 以刪除視頻畫質分析任務。可刪除已完成及進行中的任務。

<span id="Requirements"></span>
## 要求

速率限制：每個帳號每秒 10 次查詢。

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=DeleteLiveVideoQualityAnalysisTask&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 必須帶入 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)及 API 專屬參數。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`DeleteLiveVideoQualityAnalysisTask` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。當前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Name |String |否 |`test` |要刪除的任務名稱。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">需至少提供 <code>Name</code> 或 <code>ID</code> 其中一個參數。</div><br> |
|ID |Long |否 |`123456` |要刪除的任務 ID。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">需至少提供 <code>Name</code> 或 <code>ID</code> 其中一個參數。</div><br> |


<span id="Response parameters"></span>
## 回應參數

此 API 僅於回應中返回 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```json
POST https://open.byteplusapi.com/?Action=DeleteLiveVideoQualityAnalysisTask&Version=2023-01-01
{
    "ID": 21312434***1234134134
}
```


<span id="Sample response"></span>
### 回應範例

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DeleteLiveVideoQualityAnalysisTask",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為本次操作相關的錯誤碼。其他錯誤碼請參見 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**說明** |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回錯誤碼，請 [聯繫支援](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考 [請求參數](https://docs.byteplus.com/en/docs/24/107443#request-parameters) 說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料型別是否正確。 |
|400 |InvalidParam.Empty |%s 為必填 |缺少參數。請檢查錯誤訊息中指定的參數是否有傳入。 |
|400 |InvalidParam.Format |%s 格式錯誤 |參數格式不正確。請檢查錯誤訊息中指定的參數是否有非法字元或 URL 格式錯誤。 |
|400 |InvalidParam.Length |%s 不得超過 %d |參數長度不正確。請檢查錯誤訊息中指定參數的長度是否超出限制。 |
|400 |InvalidParam.OutOfRange |%s 應為 {[%s]} 之一%s 應介於 %d 與 %d 之間 |參數超出允許範圍。請檢查錯誤訊息中指定參數的值是否超出範圍。 |
|400 |InvalidParam.TimeLogic |startTime 晚於 endTime 等。 |傳入的時間參數不符合時間邏輯。請檢查是否存在以下問題：<br><br><br>* 開始時間晚於結束時間。<br><br>* 過期時間早於目前時間。 |
|400 |InvalidParam.DomainAndApp |domain 與 app 不可同時存在 |不可同時傳入 Domain 與 App。請修改輸入參數。 |
|400 |InvalidParam.VhostOrDomainEmpty |請輸入 vhost 或 domain |Vhost 或 Domain 需作為輸入參數傳入其中之一。請修改輸入參數。 |
|400 |InvalidParam.StillUsing |%s 仍在使用中，無法刪除 |錯誤訊息中指定的資源正在使用中，導致無法刪除。請釋放資源後重試。 |
|403 |RequestForbidden |*  |請求被拒絕，因為當前帳戶下沒有請求的資源（資源包括域名空間、域名、應用名稱、配置和憑證）。 |
|403 |RequestForbidden.AccountIDNotAllow |此 AccountID 無權訪問對應資源，請檢查請求參數。 |請求被拒絕，因為當前帳戶下沒有請求的資源（資源包括域名空間、域名、應用名稱、配置和憑證）。 |
|403 |RequestForbidden.BillingStatus |該 AccountID 未開通計費狀態，請開通服務或充值。 |尚未啟用視頻直播服務或帳戶已欠費，導致賬單不可用。請檢查服務開通狀態及帳戶欠費狀態。 |
|404 |ResourceNotFound |*  |未找到資源（包括域名空間、域名、應用名稱、配置和憑證）。建議重試。若仍返回錯誤碼，請[聯繫客服](https://console.byteplus.com/workorder/create)。 |
|404 |ResourceNotFound.VhostNotExist |未找到 vhost |未找到域名空間（Vhost）。請檢查傳入的域名空間是否與實際使用的域名空間一致。 |
|404 |ResourceNotFound.DomainNotExist |未找到域名 |未找到域名（Domain）。請檢查傳入的域名是否與實際使用的域名一致。 |
|404 |ResourceNotFound.AppNotExist |未找到應用 |未找到應用名稱（App）。請檢查傳入的應用名稱是否與實際使用的應用名稱一致。 |
|404 |ResourceNotFound.PresetNotExist |未找到預設配置 |未找到配置。請檢查傳入的配置是否與已建立的配置一致。 |
|429 |RequestLimitExceeded |*  |請求創建的資源（包括域名空間、域名、應用名稱、配置、憑證）超出上限。 |
|429 |RequestLimitExceeded.Exist |%s 已存在 |請求創建的資源（包括域名空間、域名、應用名稱、配置、憑證）已存在。 |
|500 |InternalError |發生內部錯誤，請聯繫管理員。 |發生內部錯誤。請[聯繫客服](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |發生與資料庫相關的內部錯誤，請聯繫管理員。 |發生與資料庫相關的內部錯誤。請[聯繫客服](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.VhostOrDomain |發生與 vhost 或域名相關的內部錯誤，請聯繫管理員。 |發生與域名空間（Vhost）或域名（Domain）相關的內部錯誤。請[聯繫客服](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.ServicesOrBilling |發生與服務或計費相關的內部錯誤，請聯繫管理員。 |發生與服務或賬單相關的內部錯誤。請[聯繫客服](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.Preset |發生與預設配置相關的內部錯誤，請聯繫管理員。 |發生與服務或賬單相關的內部錯誤。請[聯繫客服](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.Stream |發生與串流相關的內部錯誤，請聯繫管理員。 |發生與串流相關的內部錯誤。請[聯繫客服](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯繫管理員。 |發生內部錯誤。請[聯繫客服](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯繫管理員。 |發生內部錯誤。請[聯繫客服](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceTimeout |內部服務逾時。請聯繫管理員。 |內部服務逾時。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
