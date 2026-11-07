---
title: "ListBindEncryptDRM"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describecertdrm_4-zh-TW"
---

調用 `ListBindEncryptDRM` 介面以查詢指定網域命名空間及應用名稱的加密配置，或檢視指定網域命名空間下的所有加密配置。

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=ListBindEncryptDRM&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 必須帶上 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)，並包含專屬參數。

<span id="Query"></span>
### 查詢


|**參數** |**資料型態** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`ListBindEncryptDRM` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型態** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |網域命名空間。可透過 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或在 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面取得該網域所屬的命名空間。 |
|App |String |否 |`live` |直播串流 URL 中的 AppName 欄位。可包含大寫字母（A\-Z）、小寫字母（a\-z）、數字（0\-9）、底線（_）、連字號（\-）及點（.），長度為 1 至 30 字元。若未指定，表示查詢所有網域命名空間下的所有配置。 |


<span id="Response parameters"></span>
## 回應參數

專屬於 API 的回應參數請參見下表。更多細節請參考 [請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 章節。


|**參數** |**資料型態** |**範例值** |**說明** |
|---|---|---|---|
|DRMBindingList |[DRMBindingList](https://docs.byteplus.com/en/docs/24/107369#drmbindinglist) 陣列 |`-` |DRM 加密配置列表。 |


<span id="drmbindinglist"></span>
### DRMBindingList


|**參數** |**資料型態** |**範例值** |**說明** |
|---|---|---|---|
|Vhost |String |`push.example.com` |網域命名空間。 |
|App |String |`live` |AppName 欄位。 |
|DRMSystems |String 陣列 |`["FairPlay","Widevine"]` |加密類型，支援的值及其含義如下。<br><br><br>* `FairPlay`：使用 FairPlay 技術的商業 DRM 加密；<br><br>* `Widevine`：使用 Widevine 技術的商業 DRM 加密；<br><br>* `PlayReady`：使用 PlayReady 技術的商業 DRM 加密；<br><br>* `ClearKey`：HLS 標準加密。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">DRM 加密與 HLS 標準加密不可同時配置。</div><br> |
|EncryptOriginStream |Boolean |`true` |是否啟用原始串流加密，值及含義如下。<br><br><br>* `true`：已啟用；<br><br>* `false`：未啟用。 |
|EncryptTranscodeStream |Boolean |`true` |是否啟用轉碼串流加密，值及含義如下。<br><br><br>* `true`：已啟用；<br><br>* `false`：未啟用。 |
|EncryptTranscodeSuffix |String 陣列 |`["_hd"]` |啟用轉碼串流加密時，配置需加密的轉碼串流後綴。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```json
POST https://open.byteplusapi.com/?Action=ListBindEncryptDRM&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "App": "live"
}
```


<span id="Sample response"></span>
### 回應範例

```json
{
    "ResponseMetadata": {
        "RequestId": "202306041104200100100232280022D31",
        "Action": "ListBindEncryptDRM",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "cn-north-1"
    },
    "Result": {
        "DRMBindingList": [
            {
                "Vhost": "push.example.com",
                "App": "live",
                "AccountID": "1000000002",
                "Enable": true,
                "EncryptTranscodeSuffix": [
                    "_hd"
                ]
            }
        ]
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為本操作相關的錯誤碼。其他錯誤碼請參見 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**說明** |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回錯誤碼，請 [聯繫客服](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考 [請求參數](https://docs.byteplus.com/en/docs/24/107369#request-parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料型態是否正確。 |
|403 |RequestForbidden |*  |因當前帳號下無請求資源（資源包括網域命名空間、網域名稱、應用名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.AccountIDNotAllow |此 AccountID 無權存取對應資源，請檢查請求參數 |請求被拒絕，因為目前帳戶下沒有所需的資源（資源包括網域名稱空間、網域名稱、應用名稱、配置和憑證）。 |
|403 |RequestForbidden.BillingStatus |AccountID 的帳單狀態不可用，請啟用服務或儲值。 |尚未啟用視訊直播服務或帳戶欠費，導致帳單不可用。請檢查服務啟用狀態及帳戶欠費狀態。 |
|404 |ResourceNotFound |*  |未找到資源（包括網域名稱空間、網域名稱、應用名稱、配置和憑證）。建議重新嘗試。若仍返回錯誤碼，請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |發生與資料庫相關的內部錯誤，請聯絡管理員。 |發生與資料庫相關的內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
