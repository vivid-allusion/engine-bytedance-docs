---
title: "RelaunchPullToPushTask"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-relaunchpulltopushtask-zh-TW"
---

調用 `RelaunchPullToPushTask` API 以重新啟動處於已禁用狀態的轉發任務。

<span id="Requirements"></span>
## 需求

速率限制：每個帳號每秒 1 次查詢。

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=RelaunchPullToPushTask&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了需帶入 API 專屬參數外，還必須帶入 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`RelaunchPullToPushTask` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。當前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|TaskId |String |是 |`8fde6aa0281d********986e242365` |任務 ID。可調用 [ListPullToPushTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listpulltopushtask-2023) API 以獲取任務 ID。 |
|GroupName |String |否 |`default` |任務所屬的群組名稱。可調用 [ListPullToPushGroup](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listpulltopushgroup-2023) API 以獲取群組名稱。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">使用主帳號調用時，非必填欄位。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">使用子帳號調用時，為必填欄位。</div><br> |


<span id="Response parameters"></span>
## 回應參數

此 API 僅在回應中返回 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```json
POST https://open.byteplusapi.com/?Action=RelaunchPullToPushTask&Version=2023-01-01
{
    "TaskId": "8fde6aa0281d********9a6e242365"
}
```


<span id="Sample response"></span>
### 回應範例

```json
{
    "ResponseMetadata": {
        "RequestId": "20211231152846010225099008082A0F4D",
        "Action": "RelaunchPullToPushTask",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為與當前操作相關的錯誤碼。其他錯誤碼請參見 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**說明** |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回錯誤碼，請 [聯繫技術支援](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考 [請求參數](https://docs.byteplus.com/en/docs/24/107382#request-parameters) 說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料型別是否正確。 |
|403 |RequestForbidden |*  |因當前帳號下無請求資源（資源包括網域命名空間、網域名稱、應用名稱、配置與憑證），請求被拒絕。 |
|403 |RequestForbidden.AccountIDNotAllow |此 AccountID 無權訪問對應資源，請檢查請求參數 |因當前帳號下無請求資源（資源包括網域命名空間、網域名稱、應用名稱、配置與憑證），請求被拒絕。 |
|403 |RequestForbidden.BillingStatus |該 AccountID 未開通計費狀態，請開通服務或充值。 |尚未開通視頻直播服務或帳號欠費，導致計費不可用。請檢查服務開通狀態及帳號欠費狀態。 |
|404 |ResourceNotFound |*  |未找到資源（包括網域命名空間、網域名稱、應用名稱、配置與憑證）。建議重試。若仍返回錯誤碼，請 [聯繫技術支援](https://console.byteplus.com/workorder/create)。 |
|429 |RequestLimitExceeded |*  |請求建立的資源（包括網域命名空間、網域名稱、應用名稱、配置、憑證）超出上限。 |
|500 |InternalError |發生內部錯誤，請聯繫管理員。 |發生內部錯誤。請 [聯繫技術支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯繫管理員。 |發生內部錯誤。請 [聯繫技術支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯繫管理員。 |發生內部錯誤。請 [聯繫技術支援](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯繫管理員。 |內部服務逾時。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
