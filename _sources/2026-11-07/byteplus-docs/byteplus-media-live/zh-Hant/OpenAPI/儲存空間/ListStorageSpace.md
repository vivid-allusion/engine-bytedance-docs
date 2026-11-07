---
title: "ListStorageSpace"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-liststoragespace-zh-TW"
---

調用 `ListStorageSpace` API 以查詢帳戶下所有可用儲存空間的列表。在配置錄製與截圖設定時，可以參考此列表。

<span id="Requirements"></span>
## 需求

頻率限制：每個帳戶每秒最多 100 次查詢。

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=ListStorageSpace&Version=2020\-08\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了需帶入 API 專屬參數外，還必須帶入 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`ListStorageSpace` |API 操作名稱。 |
|Version |String |是 |`2020-08-01` |此 API 操作的版本。目前版本：2020\-08\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|PageSize |Integer |是 |`10` |每頁查詢結果數量。 |
|PageNum |Integer |是 |`1` |頁碼。 |


<span id="Response parameters"></span>
## 回應參數

有關唯一的 API 專屬回應參數，請參見下表。更多細節請參考 [請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 章節。


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|StorageSpace |Array of String |`["byteplus-bucket1"]` |可用儲存空間列表。 |
|CurPage |Integer |`1` |目前頁碼。 |
|Total |Integer |`60` |儲存空間總數。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```json
POST https://open.byteplusapi.com/?Action=ListStorageSpace&Version=2020-08-01
{
    "PageSize": 10,
    "PageNum": 1
}
```


<span id="Sample response"></span>
### 回應範例

```json
{
    "ResponseMetadata": {
        "RequestId": "202204060959170101742350380764F506",
        "Action": "ListStorageSpace",
        "Version": "2020-08-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "StorageSpace": [
            "byteplus-bucket1",
            "byteplus-bucket12",
            "byteplus-bucket13232"
        ],
        "CurPage": 1,
        "Total": 60
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為與本操作相關的錯誤碼。其他錯誤碼請參見 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**說明** |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回錯誤碼，請 [聯繫客服](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考 [請求參數](https://docs.byteplus.com/en/docs/24/107414#request-parameters) 說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料型別是否正確。 |
|403 |RequestForbidden |*  |因當前帳戶下無請求資源（資源包括域名空間、域名、應用名稱、配置與憑證），請求被拒絕。 |
|403 |RequestForbidden.AccountIDNotAllow |此 AccountID 無權訪問對應資源，請檢查請求參數 |因當前帳戶下無請求資源（資源包括域名空間、域名、應用名稱、配置與憑證），請求被拒絕。 |
|403 |RequestForbidden.BillingStatus |AccountID 的計費狀態不可用，請開通服務或充值。 |尚未開通視頻直播服務或帳戶欠費，導致帳單不可用。請檢查服務開通狀態及帳戶欠費狀態。 |
|404 |ResourceNotFound |*  |未找到資源（包括域名空間、域名、應用名稱、配置與憑證）。建議重試。若仍返回錯誤碼，請 [聯繫客服](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |發生內部錯誤，請聯繫管理員。 |發生內部錯誤。請 [聯繫客服](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |發生與資料庫相關的內部錯誤，請聯繫管理員。 |發生與資料庫相關的內部錯誤。請 [聯繫客服](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯繫管理員。 |發生內部錯誤。請 [聯繫客服](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯繫管理員。 |發生內部錯誤。請 [聯繫客服](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
