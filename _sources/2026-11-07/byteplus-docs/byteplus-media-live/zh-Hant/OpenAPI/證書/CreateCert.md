---
title: "CreateCert"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createcert-2023-zh-TW"
---

呼叫 `CreateCert` API，將您的憑證新增或更新至 MediaLive，以便日後綁定至網域名稱並啟用 HTTPS。

<span id="Requirements"></span>
## 需求

頻率限制：每個帳戶每秒 1 次查詢。

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=CreateCert&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了 API 專屬參數外，還必須帶上 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型態** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`CreateCert` |API 操作。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型態** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|ProjectName |String |否 |`default` |專案名稱。設定憑證的專案歸屬。預設值為 `Default`。設定專案後，具有專案權限的子帳戶可使用該憑證。 |
|CertName |String |否 |`pushCertName` |憑證名稱。 |
|ChainID |String |否 |`9*********a982edf6e84bba1f` |憑證鏈 ID。用於識別整個憑證鏈，包括端實體憑證（伺服器憑證）、中間憑證（中間 CA 憑證）以及根憑證（根 CA 憑證）。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">使用本 API 更新憑證資訊時，必須傳入 <code>ChainID</code>。</div><br> |
|Rsa |[Rsa](https://docs.byteplus.com/en/docs/24/107288#rsa) 物件 |是 |`-` |憑證資訊，包含憑證內容及憑證私鑰內容。 |
|UseWay |String |是 |`https` |憑證用途。請始終設為 `https`，即代表 HTTPS 加密。 |


<span id="rsa"></span>
### Rsa


|**參數** |**資料型態** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Pubkey |String |是 |`*******` |憑證內容。您需在電腦上使用文字編輯器開啟憑證，並將全部內容複製貼上作為參數。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">系統支援自動獲取憑證鏈。您只需上傳為您的網域簽發的憑證，系統會自動獲取完整憑證鏈。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">若選擇上傳憑證鏈，請務必包含伺服器憑證、中間憑證及根憑證，並按正確順序排列：伺服器憑證在前，其次為中間憑證，最後為根憑證。順序錯誤將導致憑證鏈失效。</div><br> |
|Prikey |String |是 |`*******` |憑證私鑰內容。您需在電腦上使用文字編輯器開啟憑證私鑰，並將全部內容複製貼上作為參數。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">請確保憑證私鑰未設密碼保護。</div><br> |


<span id="Response parameters"></span>
## 回應參數

有關唯一的 API 專屬回應參數，請參見下表。更多細節請參考 [請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)章節。


|**參數** |**資料型態** |**範例值** |**說明** |
|---|---|---|---|
|ChainID |String |`9*********a982edf6e84bba1f` |憑證鏈 ID。 |
|Domain |String |`live.example.com` |使用本憑證的網域名稱。 |
|UseWay |String |`https` |憑證用途。請始終設為 `https`，即代表 HTTPS 加密。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://open.byteplusapi.com/?Action=CreateCert&Version=2023-01-01
{
    "UseWay": "https",
    "Rsa": {
        "PubKey": "******",
        "PriKey": "******"
    }
}
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestID": "2020091618492801022706705734830",
        "Action": "CreateCert",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "cn-north-1"
    },
    "Result": {
        "ChainID": "9**47c0151394d93a982edf6e84bba1f",
        "Domain": "push.example.com",
        "UseWay": "https"
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為與本操作相關的錯誤碼。其他錯誤碼請參見 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**Status Code** |**Error Code** |**Error Message** |**說明** |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍然返回錯誤碼，請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考[請求參數](https://docs.byteplus.com/en/docs/24/107288#request-parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料型別是否正確。 |
|400 |InvalidParam.OutOfRange |%s 應為 {[%s]} 之一%s 應介於 %d 與 %d 之間 |參數超出允許範圍。請檢查錯誤訊息中指定參數的值是否超出範圍。 |
|403 |RequestForbidden |*  |因目前帳戶下無請求資源（資源包括網域命名空間、網域名稱、應用名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.AccountIDNotAllow |此 AccountID 無權存取對應資源，請檢查請求參數 |因目前帳戶下無請求資源（資源包括網域命名空間、網域名稱、應用名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.BillingStatus |此 AccountID 未開通計費狀態，請啟用服務或儲值。 |尚未啟用視頻直播服務或帳戶欠費，導致帳單不可用。請檢查服務啟用狀態及帳戶欠費狀態。 |
|404 |ResourceNotFound |*  |未找到資源（包括網域命名空間、網域名稱、應用名稱、配置及憑證）。建議重試。若仍然返回錯誤碼，請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |發生與資料庫相關的內部錯誤，請聯絡管理員。 |發生與資料庫相關的內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
