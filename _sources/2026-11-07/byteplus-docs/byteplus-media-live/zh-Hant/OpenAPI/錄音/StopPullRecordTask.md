---
title: "StopPullRecordTask"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-stoppullrecordtask-zh-TW"
---

呼叫 `StopPullRecordTask` API，以停止尚未啟動或正在執行的錄製任務。停止正在執行的錄製任務將會產生錄製檔案。

<span id="83d84d76"></span>
## 需求

頻率限制：每個帳戶每秒最多 50 次查詢。

<span id="4cd90e5f"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=StopPullRecordTask&Version=2023\-01\-01


<span id="d5669adc"></span>
## 請求參數

<span id="a293ff65"></span>
### 通用參數

所有 API 除了需帶入 API 專屬參數外，還必須帶入 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="99f0e3ec"></span>
### 查詢


|參數 |資料型別 |是否必填 |範例值 |說明 |
|---|---|---|---|---|
|Action |String |是 |`StopPullRecordTask` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="c262ce78"></span>
### Body 參數


|參數 |資料型別 |是否必填 |範例值 |說明 |
|---|---|---|---|---|
|TaskId |String |是 |`f831f3b0********1aa4dcf7621` |錄製任務的唯一識別碼。你可以呼叫 [ListPullRecordTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listpullrecordtask) API 來查看直播錄製任務的任務 ID。 |


<span id="6308500a"></span>
## 回應參數

此 API 僅於回應中返回 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="e814026d"></span>
## 範例

<span id="da1c188d"></span>
### 範例請求

```JSON
POST https://open.byteplusapi.com/?Action=StopPullRecordTask&Version=2023-01-01
{
    "TaskId": "f831f3b0********1aa4dcf7621"
}
```


<span id="6ab439ca"></span>
### 範例回應

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "StopPullRecordTask",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```


<span id="1469dbba"></span>
## 錯誤碼

以下為與本次操作相關的錯誤碼。其他錯誤碼請參見 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|狀態碼 |錯誤碼 |錯誤訊息 |說明 |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回此錯誤碼，請 [聯繫客服](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考 [請求參數](#Request Parameters) 說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數未通過驗證。請檢查參數型別是否正確。 |
|403 |RequestForbidden |*  |請求被拒絕。當前帳戶下無請求資源（域名空間、域名、應用、配置模板、憑證）。 |
|403 |RequestForbidden.AccountIDNotAllow |此 AccountID 無權訪問對應資源，請檢查請求參數 |請求被拒絕。當前帳戶下無請求資源（域名空間、域名、應用、配置模板、憑證）。 |
|403 |RequestForbidden.BillingStatus |此 AccountID 的計費狀態不可用，請開通服務或充值。 |因未開通視頻直播服務或帳戶逾期，帳單不可用。請檢查服務開通狀態及帳戶逾期狀態。 |
|404 |ResourceNotFound |*  |未找到資源（域名空間、域名、應用、配置模板、憑證）。建議重試。若仍返回此錯誤碼，請 [聯繫客服](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |發生內部錯誤，請聯繫管理員。 |發生內部錯誤，請 [聯繫客服](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯繫管理員。 |服務間發生錯誤時，請 [聯繫客服](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯繫管理員。 |服務間發生錯誤，請 [聯繫客服](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯繫管理員。 |內部服務逾時，請 [聯繫客服](https://console.byteplus.com/workorder/create)。 |
