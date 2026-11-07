---
title: "RestartPullToPushTask"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-restartpulltopushtask-2023-zh-TW"
---

調用 `RestartPullToPushTask` API 以重新啟動處於已禁用狀態的轉發任務。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">自 2025 年 3 月 15 日起，我們將不再維護此舊版 API。其文檔將於 2025 年 6 月 14 日下架。建議遷移至新版 API。詳情請參見 <a href="https://docs.byteplus.com/en/docs/byteplus-media-live/continuepulltopushtask">ContinuePullToPushTask</a> 文檔。</div>


<span id="Requirements"></span>
## 需求

頻率限制：每個帳戶每秒 1 次查詢。

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=RestartPullToPushTask&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 調用時，除了 API 專屬參數外，還必須包含 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**數據類型** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`RestartPullToPushTask` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。當前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**數據類型** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|TaskId |String |是 |`8fde6aa0281d********986e242365` |任務 ID。可調用 [ListPullToPushTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listpulltopushtask-2023) API 以獲取任務 ID。 |
|GroupName |String |否 |`default` |任務所屬的群組名稱。可調用 [ListPullToPushGroup](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listpulltopushgroup-2023) API 以獲取群組名稱。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">主帳戶調用時，該欄位非必填。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">子帳戶調用時，該欄位為必填。</div><br> |


<span id="Response parameters"></span>
## 響應參數

此 API 僅在響應中返回 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```json
POST https://open.byteplusapi.com/?Action=RestartPullToPushTask&Version=2023-01-01
{
    "TaskId": "8fde6aa0281d********9a6e242365"
}
```


<span id="Sample response"></span>
### 響應範例

```json
{
    "ResponseMetadata": {
        "RequestId": "20211231152846010225099008082A0F4D",
        "Action": "RestartPullToPushTask",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為與當前操作相關的錯誤碼。如需其他錯誤碼，請參見 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**說明** |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回錯誤碼，請 [聯繫支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考 [請求參數](https://docs.byteplus.com/en/docs/24/107326#request-parameters) 說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查數據類型是否正確。 |
|403 |RequestForbidden |*  |因當前帳戶下無請求資源（資源包括域名空間、域名、應用名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.AccountIDNotAllow |該 AccountID 無權訪問對應資源，請檢查請求參數 |因當前帳戶下無請求資源（資源包括域名空間、域名、應用名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.BillingStatus |該 AccountID 未開通計費狀態，請開通服務或充值。 |尚未開通視頻直播服務或帳戶欠費，導致賬單不可用。請檢查服務開通狀態及帳戶欠費狀態。 |
|404 |ResourceNotFound |*  |未找到資源（包括域名空間、域名、應用名稱、配置及憑證）。建議重試。若仍返回錯誤碼，請 [聯繫支持](https://console.byteplus.com/workorder/create)。 |
|429 |RequestLimitExceeded |*  |請求創建的資源（包括域名空間、域名、應用名稱、配置、憑證）超出限制。 |
|500 |InternalError |發生內部錯誤，請聯繫管理員。 |發生內部錯誤。請 [聯繫支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯繫管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
