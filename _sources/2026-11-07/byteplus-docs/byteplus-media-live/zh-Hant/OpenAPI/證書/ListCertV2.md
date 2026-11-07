---
title: "ListCertV2"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listcertv2-zh-TW"
---

呼叫 `ListCertV2` API，檢視目前帳號下的憑證清單。

## 要求

速率限制：每個帳號每秒 10 次查詢。

## HTTP 請求

* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=ListCertV2&Version=2023\-01\-01

## 請求參數

### 通用參數

所有 API 除了 API 專用參數外，還必須帶上[通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

### 查詢

|參數 |資料類型 |必填 |範例值 |說明 |
|---|---|---|---|---|
|Action |String |是 |`ListCertV2` |API 操作。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |

### 主體參數

|參數 |資料類型 |必填 |範例值 |說明 |
|---|---|---|---|---|
|Available |Boolean |否 |`true` |是否擷取已啟用或已停用的憑證。<br><br><br>* `true`：（預設）擷取已啟用的憑證。<br><br>* `false`：擷取已停用的憑證。 |
|Domain |String |否 |`push.example.com` |憑證保護的網域名稱。支援精確搜尋。 |
|Expiring |Boolean |否 |`false` |是否擷取有效或已過期的憑證。<br><br><br>* `false`：（預設）擷取仍然有效的憑證。<br><br>* `true`：擷取已過期的憑證。<br><br><br>> **说明**<br><br><br>> 只有在指定 `Available` 時，此參數才會生效。<br> |
|CertName |String |否 |`domaincert` |憑證名稱。支援模糊搜尋。 |
|PageSize |Integer |否 |`10` |每頁的查詢結果數量。有效值：[1,1000]。<br><br>> **说明**<br><br><br>> `PageNum` 和 `PageSize` 必須一起指定。如果未指定任一參數，則會傳回所有結果。<br> |
|PageNum |Integer |否 |`1` |頁碼。有效值：[1,1000]。<br><br>> **说明**<br><br><br>> `PageNum` 和 `PageSize` 必須一起指定。如果未指定任一參數，則會傳回所有結果。<br> |
|ProjectName |String |否 |`MyProject` |與憑證關聯的專案名稱。此欄位為選填，可用於依專案名稱篩選憑證。 |

## 回應參數

如需 API 專用的唯一回應參數，請參閱下表。如需更多詳細資訊，請參閱[請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)章節。

|參數 |資料類型 |範例值 |說明 |
|---|---|---|---|
|CertList |[CertList](https://docs.byteplus.com/en/docs/24/107423#certlist) 陣列 |`-` |憑證清單。 |
|Total |Integer |`20` |目前查詢結果中的憑證總數。 |
|ExpirationInfo |[ExpirationInfo](https://docs.byteplus.com/en/docs/24/107423#expirationinfo) 物件 |`-` |目前查詢中所有憑證的到期資訊。 |

### CertList

|參數 |資料類型 |範例值 |說明 |
|---|---|---|---|
|ProjectName |String |`default` |憑證的專案。 |
|CertDomainList |String 陣列 |`["push.example.com"]` |憑證保護的網域名稱清單。 |
|CertName |String |`push.example.com` |憑證名稱。 |
|ChainID |String |`4060e26538a149e2a87b42*******11` |憑證鏈 ID。 |
|CertID |String |`812******1` |憑證 ID。 |
|NotAfter |String |`2024-08-18T07:19:00Z` |憑證的生效時間（UTC 時間，採用 RFC 3339 格式，時間戳記精確到秒）。 |
|NotBefore |String |`2020-08-19T07:19:00Z` |憑證的到期時間（UTC 時間，採用 RFC 3339 格式，時間戳記精確到秒）。 |
|Status |String |`OK` |憑證狀態。有效值包括：<br><br><br>* `OK`：正常。<br><br>* `Expire`：已過期。<br><br>* `30days`：30 天後到期。<br><br>* `15days`：15 天後到期。<br><br>* `7days`：7 天後到期。<br><br>* `1days`：1 天後到期。 |
|CreateTime |String |`2020-08-19T07:19:00Z` |憑證建立時的時間戳記，採用 RFC3339 格式，UTC 時區且精確到秒。 |

### ExpirationInfo

|參數 |資料類型 |範例值 |說明 |
|---|---|---|---|
|ActiveNum |Integer |`10` |目前有效且未過期的有效憑證數量。 |
|ExpireNum |Integer |`5` |目前查詢結果中的已過期憑證數量。 |
|ClosingExpireNum |Integer |`5` |一個月內即將到期的憑證數量。 |

## 範例

### 請求範例

```json
POST https://open.byteplusapi.com/?Action=ListCertV2&Version=2023-01-01
{
    "AccountID": "1000000001"
}
```

### 回應範例

```json
{
    "ResponseMetadata": {
        "RequestID":  "2020091618453101022706705762997",
        "Action": "ListCert",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "CertList": [
            {
                "CertID": "cert-94552b4a4b0a4b8fbe3d*****",
                "CertName": "*.example.com",
                "CertDomainList": ["*.example.com"],
                "ChainID": "4060e26538a149e2a87b42deba979011",
                "NotBefore": "2020-08-19T07:19:00Z",
                "NotAfter": "2024-08-18T07:19:00Z",
                "Status": "OK"
            }
            {
                "CertID": "cert-94552b4a4b0a4b8******e5152",
                "CertName": "*.test.com.cn",
                "CertDomainList": ["*.test.com.cn"],
                "ChainID": "d7134cbff1dd4425847f329cba0245e4",
                "NotBefore": "2020-08-11T05:42:54Z",
                "NotAfter": "2020-09-18T05:42:54Z",
                "Status": "Expire"
            }
        ]
    }
}
```

## 錯誤碼

以下是與目前操作相關的錯誤碼。如需其他錯誤碼，請參閱 [BytePlus OpenAPI 的通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。

|狀態碼 |錯誤碼 |錯誤訊息 |說明 |
|---|---|---|---|
|200 |CommonErr |\- |未分類的錯誤。建議重試。如果仍傳回此錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |\- |輸入參數無效或不符合要求。請參閱[請求參數](https://docs.byteplus.com/en/docs/24/107423#request-parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |Request parameter error, please check input data |參數驗證失敗。請檢查資料類型是否正確。 |
|403 |RequestForbidden |\- |由於目前帳號下沒有請求的資源，請求遭到拒絕（資源包括網域名稱空間、網域名稱、應用程式名稱、組態和憑證）。 |
|403 |RequestForbidden.AccountIDNotAllowed |this AccountID does not have permission to access the corresponding resource, please check the request parameters |請求遭到拒絕。目前帳號下沒有請求的資源（網域命名空間、網域名稱、應用程式、組態範本、憑證）。 |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |影片直播服務尚未啟用，或帳號欠費，導致帳單不可用。請檢查服務啟用狀態和帳號欠費狀態。 |
|403 |AccessDenied |User is not authorized to perform: %s on resource: %s |請求遭到拒絕。目前帳號下沒有請求的資源（網域命名空間、網域名稱、應用程式、組態範本、憑證）或介面權限。 |
|404 |ResourceNotFound |\- |找不到資源（包括網域名稱空間、網域名稱、應用程式名稱、組態和憑證）。建議重試。如果仍傳回此錯誤碼，請[聯絡支援](https://docs.byteplus.com/en/docs/24/%5B++https://console.byteplus.com/workorder/create++%5D(https://console.byteplus.com/workorder/create))。 |
|500 |InternalError |an internal error occurred, please contact the administrator. |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |an internal error related to database occurred, please contact the administrator. |發生與資料庫相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |內部服務逾時。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
