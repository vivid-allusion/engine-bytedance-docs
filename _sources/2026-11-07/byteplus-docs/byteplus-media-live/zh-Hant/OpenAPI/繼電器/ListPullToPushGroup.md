---
title: "ListPullToPushGroup"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listpulltopushgroup-2023-zh-TW"
---

調用 `ListPullToPushGroup` API 以查詢群組名稱列表。

<span id="Requirements"></span>
## 需求

頻率限制：每個帳戶每秒 10 次查詢。

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=ListPullToPushGroup&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了需帶入 API 專屬參數外，還必須帶入 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`ListPullToPushGroup` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。當前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|PageNum |Integer |是 |`1` |頁碼。BytePlus MediaLive 會將查詢結果分頁，僅返回指定頁面的結果。有效範圍：1–1000。 |
|PageSize |Integer |是 |`10` |每頁返回的結果數量。有效範圍：1–1000。 |
|StatusList |Integer 陣列 |否 |`0` |群組狀態，取值及其含義如下。<br><br><br>* `0`：（預設）可用；<br><br>* `1`：已刪除，不可用。 |


<span id="Response parameters"></span>
## 回應參數

如需 API 專屬回應參數，請參見下表。如需更多細節，請參考 [請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 章節。


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|List |[List](https://docs.byteplus.com/en/docs/24/107342#list) 陣列 |`-` |群組資訊列表。 |
|Total |Integer |`1` |查詢結果的資料條數。 |


<span id="list"></span>
### 列表


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Name |String |`group001` |群組名稱。 |
|ProjectName |String |`default` |群組所屬的專案。 |
|Status |Integer |`0` |群組狀態，取值及其含義如下。<br><br><br>* `0`：（預設）可用；<br><br>* `1`：已刪除，不可用。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```json
POST https://open.byteplusapi.com/?Action=ListPullToPushGroup&Version=2023-01-01
{
    "PageNum": 1,
    "PageSize": 10
}
```


<span id="Sample response"></span>
### 回應範例

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListPullToPushGroup",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "List": [
            {
                "Name": "Group001",
                "ProjectName": "default",
                "Status": 0
            }
        ],
        "Total": 1
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為與當前操作相關的錯誤碼。如需其他錯誤碼，請參見 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**說明** |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回錯誤碼，請 [聯繫支援](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考 [請求參數](https://docs.byteplus.com/en/docs/24/107342#request-parameters) 說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料型別是否正確。 |
|400 |InvalidParameter.Tags.Key |指定的參數 Tags.Key 無效。 |參數 `Tags.Key` 驗證失敗。請檢查參數是否正確。 |
|400 |InvalidParameter.Tags.Value |指定的參數 Tags.Value 無效。 |參數 `Tags.Value` 驗證失敗。請檢查參數是否正確。 |
|403 |RequestForbidden |*  |請求被拒絕，因當前帳戶下無請求的資源（資源包括網域名稱空間、網域名稱、應用名稱、配置及憑證）。 |
|403 |RequestForbidden.AccountIDNotAllowed |此 AccountID 無權存取對應資源，請檢查請求參數 |請求被拒絕，因當前帳戶下無請求的資源（資源包括網域名稱空間、網域名稱、應用名稱、配置及憑證）。 |
|404 |ResourceNotFound |*  |未找到資源（包括網域名稱空間、網域名稱、應用名稱、配置及憑證）。建議重試。若仍返回錯誤碼，請 [聯繫支援](https://console.byteplus.com/workorder/create)。 |
|429 |RequestLimitExceeded.Exist |請重新命名，所請求建立的資源已存在 |所請求建立的資源（包括網域名稱空間、網域名稱、應用程式名稱、組態、憑證）已存在。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |發生與資料庫相關的內部錯誤，請聯絡管理員。 |發生與資料庫相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
