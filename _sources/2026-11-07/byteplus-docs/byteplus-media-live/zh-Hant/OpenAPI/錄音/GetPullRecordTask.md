---
title: "GetPullRecordTask"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/GetPullRecordTask-zh-TW"
---

調用 `GetPullRecordTask` API 查詢單個直播錄製任務的信息。

<span id="4b5fc640"></span>
## 需求

頻率限制：每個帳戶每秒最多 50 次查詢。

<span id="c6f0364b"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=GetPullRecordTask&Version=2023\-01\-01


<span id="b4bba97f"></span>
## 請求參數

<span id="754fb9f4"></span>
### 通用參數

所有 API 調用時，除 API 專屬參數外，還必須包含 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="b104238e"></span>
### 查詢


|參數 |數據類型 |是否必填 |範例值 |說明 |
|---|---|---|---|---|
|Action |String |是 |`GetPullRecordTask` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本號。當前版本：2023\-01\-01。 |


<span id="05a50648"></span>
### Body 參數


|參數 |數據類型 |是否必填 |範例值 |說明 |
|---|---|---|---|---|
|TaskID |String |是 |`5b903f78c7f5ae*******01f6fe2eea` |任務 ID，即錄製任務的唯一標識符。可調用 [ListPullRecordTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listpullrecordtask) API 獲取任務 ID。 |


<span id="721ebd5b"></span>
## 響應參數

有關唯一的 API 專屬響應參數，請參見下表。更多詳情請參考 [請求響應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 章節。


|參數 |數據類型 |範例值 |說明 |
|---|---|---|---|
|TaskDetail |[TaskDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/GetPullRecordTask#taskdetail) 對象 |`-` |任務詳情。 |


<span id="58d749ae"></span>
### TaskDetail


|參數 |數據類型 |範例值 |說明 |
|---|---|---|---|
|TaskId |String |`5b903f78c7f5ae*******01f6fe2eea` |任務 ID。 |
|StartTime |String |`2023-10-09T15:16:15Z` |任務開始時間，UTC 時間，RFC3339 格式，精確到秒。 |
|EndTime |String |`2023-10-09T15:18:28Z` |任務結束時間，UTC 時間，RFC3339 格式，精確到秒。 |
|Vhost |String |`example.com` |創建錄製任務時傳入的域名命名空間。 |
|Domain |String |`pull.example.com` |創建錄製任務時傳入的域名。 |
|App |String |`live` |創建錄製任務時傳入的應用名稱。 |
|Status |String |`未開始` |錄製任務的狀態。可能的取值如下。<br><br><br>* `停用`：錄製任務已被停止；<br><br>* `未開始`：錄製任務尚未開始；<br><br>* `生效中`：錄製任務進行中；<br><br>* `已結束`：錄製已完成。 |


<span id="70ec6ad3"></span>
## 範例

<span id="888ee4c6"></span>
### 請求範例

```JSON
POST https://open.byteplusapi.com/?Action=GetPullRecordTask&Version=2023-01-01
{
    "TaskID": "5b903f78c7f5ae*******01f6fe2eea"
}
```


<span id="f6ebe8b7"></span>
### 響應範例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetPullRecordTask",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "TaskDetail": {
            "TaskId": "5b903f78c7f5ae*******01f6fe2eea",
            "StartTime": "2023-10-09T15:16:15Z",
            "EndTime": "2023-10-09T15:18:28Z",
            "Vhost": "example.com",
            "Domain": "pull.example.com",
            "App": "live",
            "Status": "生效中"
        }
    }
}
```


<span id="821e3fe0"></span>
## 錯誤碼

以下為與當前操作相關的錯誤碼。其他錯誤碼請參見 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|狀態碼 |錯誤碼 |錯誤信息 |說明 |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。如仍返回該錯誤碼，請 [聯繫支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考 [請求參數](#Request Parameters) 說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入數據 |參數驗證未通過。請檢查參數類型是否正確。 |
|403 |RequestForbidden |*  |請求被拒絕。當前帳戶下無請求的資源（域名空間、域名、應用、配置模板、證書）。 |
|403 |RequestForbidden.AccountIDNotAllowed |該 AccountID 無權訪問對應資源，請檢查請求參數 |請求被拒絕。當前帳戶下無請求的資源（域名空間、域名、應用、配置模板、證書）。 |
|403 |RequestForbidden.BillingStatus |該 AccountID 未開通計費狀態，請開通服務或充值。 |視頻直播服務未開通或帳戶欠費，導致賬單不可用。請檢查服務開通狀態及帳戶欠費情況。 |
|404 |ResourceNotFound |*  |未找到資源（網域命名空間、網域名稱、應用程式、配置範本、憑證）。建議重試。如果仍然返回此錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |服務之間發生錯誤，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |服務之間發生錯誤，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
