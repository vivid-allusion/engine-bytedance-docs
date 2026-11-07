---
title: "CreatePullToPushGroup"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createpulltopushgroup-2023-zh-TW"
---

調用 `CreatePullToPushGroup` API 以建立中繼任務群組並綁定至專案，透過配置群組即可根據專案管理子帳號權限。

<span id="Requirements"></span>
## 需求

速率限制：每個帳號每秒 10 次查詢。

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=CreatePullToPushGroup&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了需帶入 API 專屬參數外，還必須帶入 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`CreatePullToPushGroup` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。當前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Name |String |是 |`group001` |群組名稱。可包含中文、英文大寫字母（A\-Z）、英文小寫字母（a\-z）、數字（0\-9），長度為 1 至 20 個字元。 |
|ProjectName |String |是 |`default` |預設為空，表示屬於「default」專案。<br><br>群組名稱與專案關聯後，可依專案管理資源用量與計費。群組名稱建立後，無法變更專案設定。如需管理專案，請前往 BytePlus 控制台的 [Project](https://console.byteplus.com/iam/resourcemanage/project) 頁面。 |


<span id="Response parameters"></span>
## 回應參數

此 API 僅於回應中返回 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://open.byteplusapi.com/?Action=CreatePullToPushGroup&Version=2023-01-01
{
    "Name": "RelayGroup001",
    "ProjectName": "default"
}
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreatePullToPushGroup",
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
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回錯誤碼，請 [聯繫支援](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考 [請求參數](https://docs.byteplus.com/en/docs/24/107434#request-parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料型別是否正確。 |
|400 |InvalidParameter.Tags.Key |指定的參數 Tags.Key 無效。 |參數 `Tags.Key` 未通過驗證。請檢查參數是否正確。 |
|400 |InvalidParameter.Tags.Value |指定的參數 Tags.Value 無效。 |參數 `Tags.Value` 未通過驗證。請檢查參數是否正確。 |
|400 |InvalidParameter.Tags |指定的參數 Tags 無效。 |參數 `Tags` 驗證失敗。請檢查參數是否正確。 |
|400 |Duplicate.Tags.Key |指定的 tags 物件包含重複的 key。 |參數 `Tags.Key` 的值重複。請檢查參數是否正確。 |
|403 |RequestForbidden |*  |請求被拒絕，因當前帳號下無請求資源（資源包括網域名稱空間、網域名稱、應用名稱、配置、憑證）。 |
|403 |RequestForbidden.AccountIDNotAllowed |此 AccountID 無權存取對應資源，請檢查請求參數 |請求被拒絕，當前帳號下無請求資源（網域名稱空間、網域名稱、應用、配置範本、憑證）。 |
|404 |ResourceNotFound |*  |未找到資源（包含網域名稱空間、網域名稱、應用名稱、配置、憑證）。建議重試。若仍返回錯誤碼，請 [聯繫支援](https://console.byteplus.com/workorder/create)。 |
|429 |RequestLimitExceeded.Exist |請重新命名，因為請求建立的資源已存在 |請求建立的資源（包括網域名稱空間、網域名稱、應用程式名稱、組態、憑證）已存在。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |發生與資料庫相關的內部錯誤，請聯絡管理員。 |發生與資料庫相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
