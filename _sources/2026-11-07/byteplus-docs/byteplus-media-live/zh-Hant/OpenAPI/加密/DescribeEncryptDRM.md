---
title: "DescribeEncryptDRM"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describecertdrm_2-zh-TW"
---

呼叫 `DescribeEncryptDRM` API，以檢視已設定的 DRM 證書管理平台存取金鑰及 FairPlay 證書資訊。

<span id="Requirements"></span>
## 需求

頻率限制：每個帳戶每秒 1 次查詢。

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=DescribeEncryptDRM&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了 API 專屬參數外，還必須搭配 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) 一同呼叫。

<span id="Query"></span>
### 查詢


|**參數** |**資料型態** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`DescribeEncryptDRM` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Response parameters"></span>
## 回應參數

如需 API 專屬回應參數，請參見下表。更多細節請參考 [請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 章節。


|**參數** |**資料型態** |**範例值** |**說明** |
|---|---|---|---|
|DRMItem |[DRMItem](https://docs.byteplus.com/en/docs/24/107397#drmitem) 物件 |`-` |DRM 加密配置列表。 |


<span id="drmitem"></span>
### DRMItem


|**參數** |**資料型態** |**範例值** |**說明** |
|---|---|---|---|
|APIKey |String |`desnjkfjsedlfndskfnsklnda` |DRM 證書管理平台 API 存取金鑰。 |
|CertificateName |String |`test` |自定 FairPlay 證書名稱。 |
|PrivateKeyFileName |String |`private.cer` |申請 FairPlay 證書時所建立的私鑰檔案名稱。 |
|CertificateFileName |String |`fairplay.pem` |FairPlay 證書檔案名稱。 |
|ApplicationSecretKey |String |`dandkandkadacdsknkmkmmknk` |申請 FairPlay 證書流程中，Apple 會回傳 ASk（Application Secret Key）字串。 |
|PrivateKey |String |`hufh29893rh2f384hfv82` |申請 FairPlay 證書時所建立的私鑰檔案金鑰。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "201806041104*****100232280022D30",
        "Action": "DescribeEncryptDRM",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "DRMItem": {
            "APIKey": "desnjkfjs*****dskfnsklnda",
            "CertificateName": "test",
            "PrivateKeyFileName": "private.cer",
            "CertificateFileName": "fairplay.pem",
            "ApplicationSecretKey": "dandkan*****sknkmkmmknk",
            "PrivateKey": "hufh298*****84hfv82"
        }
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為與本操作相關的錯誤碼。其他錯誤碼請參見 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**說明** |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍回傳錯誤碼，請 [聯絡客服](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考 [請求參數](https://docs.byteplus.com/en/docs/24/107397#request-parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料型態是否正確。 |
|403 |RequestForbidden |*  |因目前帳戶下無請求資源（資源包含網域命名空間、網域名稱、App 名稱、配置、證書），請求被拒絕。 |
|403 |RequestForbidden.AccountIDNotAllowed |此 AccountID 無權存取對應資源，請檢查請求參數 |請求被拒絕。目前帳戶下無請求資源（網域命名空間、網域名稱、應用、配置範本、證書）。 |
|403 |RequestForbidden.BillingStatus |AccountID 未啟用計費狀態，請開通服務或儲值。 |尚未啟用視頻直播服務或帳戶欠費，導致帳單不可用。請檢查服務開通狀態及帳戶欠費狀態。 |
|403 |AccessDenied |使用者無權於資源 %s 執行操作 %s |請求被拒絕。目前帳戶下無請求資源（網域命名空間、網域名稱、應用、配置範本、證書）或介面權限。 |
|404 |ResourceNotFound |*  |未找到資源（包含網域命名空間、網域名稱、App 名稱、配置、證書）。建議重試。若仍回傳錯誤碼，請 [聯絡客服](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請 [聯絡客服](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |發生與資料庫相關的內部錯誤，請聯絡管理員。 |發生與資料庫相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
