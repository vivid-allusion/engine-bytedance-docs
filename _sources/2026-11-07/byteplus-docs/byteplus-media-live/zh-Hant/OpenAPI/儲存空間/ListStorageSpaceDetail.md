---
title: "ListStorageSpaceDetail"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-liststoragespacedetail-zh-TW"
---

調用 `ListStorageSpaceDetail` API 以查詢帳戶下指定儲存空間的詳細資訊。

<span id="Requirements"></span>
## 需求

速率限制：每個帳戶每秒 100 次查詢。

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=ListStorageSpaceDetail&Version=2020\-08\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 必須同時帶上 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) 和 API 專屬參數。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`ListStorageSpaceDetail` |API 操作。 |
|Version |String |是 |`2020-08-01` |本 API 操作的版本。當前版本：2020\-08\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|StorageSpaceList |Array of String |否 |`["bucket112233"]` |要查詢的儲存空間清單。如未指定，則查詢帳戶下所有儲存空間。 |


<span id="Response parameters"></span>
## 回應參數

如需唯一的 API 專屬回應參數，請參見下表。更多詳情請參考 [請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 章節。


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|StorageSpaceListDetail |Array of [StorageSpaceListDetail](https://docs.byteplus.com/en/docs/24/107413#storagespacelistdetail) |`-` |查詢到的每個儲存空間的詳細資訊。 |


<span id="storagespacelistdetail"></span>
### StorageSpaceListDetail


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|AccountID |String |`3000000285` |您的帳戶 ID。 |
|Name |String |`fcdn-boe` |儲存空間名稱。 |
|PublicDomain |String |`此參數已棄用。 \|` \|儲存空間的公網域名。 \| | |
|CnameDomain |String |`ccama.test.example.com` |公網域名所指向的 CNAME。 |
|TTL |Integer |`-` |此參數已棄用。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

<span id="Sample response"></span>
### 範例回應

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
        "StorageSpaceListDetail": [
            {
                "AccountID": "3000000285",
                "Name": "fcdn-boe",
                "PublicDomain": "test.example.com",
                "CnameDomain": "cname.test.example.com"
            }
        ]
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為與本操作相關的錯誤碼。其他錯誤碼請參見 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**說明** |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回錯誤碼，請 [聯繫客服](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考 [請求參數](https://docs.byteplus.com/en/docs/24/107413#request-parameters) 說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料型別是否正確。 |
|403 |RequestForbidden |*  |請求被拒絕，因為當前帳戶下無請求資源（資源包括域名空間、域名、應用名稱、配置和憑證）。 |
|403 |RequestForbidden.AccountIDNotAllow |此 AccountID 無權訪問對應資源，請檢查請求參數 |請求被拒絕，因為當前帳戶下無請求資源（資源包括域名空間、域名、應用名稱、配置和憑證）。 |
|403 |RequestForbidden.BillingStatus |該 AccountID 未開通計費狀態，請開通服務或充值。 |尚未開通視頻直播服務或帳戶欠費，導致無法獲取賬單。請檢查服務開通狀態及帳戶欠費狀態。 |
|404 |ResourceNotFound |*  |未找到資源（包括域名空間、域名、應用名稱、配置和憑證）。建議重試。若仍返回錯誤碼，請 [聯繫客服](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |發生內部錯誤，請聯繫管理員。 |發生內部錯誤。請 [聯繫客服](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |發生與資料庫相關的內部錯誤，請聯繫管理員。 |發生與資料庫相關的內部錯誤。請 [聯繫客服](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
