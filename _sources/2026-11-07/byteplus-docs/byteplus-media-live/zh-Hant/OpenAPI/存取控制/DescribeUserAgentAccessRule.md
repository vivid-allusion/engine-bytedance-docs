---
title: "DescribeUserAgentAccessRule"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeuseragentaccessrule-zh-TW"
---

呼叫 `DescribeUserAgentAccessRule` API 查詢 User\-Agent 限制。

## 要求

速率限制：每個帳戶每秒 10 次查詢。

## HTTP 請求

* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=DescribeUserAgentAccessRule&Version=2023\-01\-01

## 請求參數

### 公共參數

所有 API 除了 API 特定參數外，還必須搭配[公共參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)呼叫。

### 查詢

|參數 |資料類型 |必填 |範例值 |說明 |
|---|---|---|---|---|
|Action |String |是 |`DescribeUserAgentAccessRule` |API 操作。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |

### 主體參數

|參數 |資料類型 |必填 |範例值 |說明 |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |域名空間。您可以呼叫 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或造訪 BytePlus MediaLive 控制台中的[域名](https://console.byteplus.com/live/main/domain/list)頁面，以取得域名空間。 |
|Domain |String |否 |`pull.example.com` |用於拉流的域名。您可以呼叫 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或造訪 BytePlus MediaLive 控制台中的[域名](https://console.byteplus.com/live/main/domain/list)頁面，以取得域名。 |

## 回應參數

如需 API 特定的唯一回應參數，請參閱下表。如需更多詳細資訊，請參閱[請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)章節。

|參數 |資料類型 |範例值 |說明 |
|---|---|---|---|
|UserAgentList |[UserAgentList](https://docs.byteplus.com/en/docs/24/107447#useragentlist) 的陣列 |`-` |UA 封鎖清單和允許清單組態的清單。 |

### UserAgentList

|參數 |資料類型 |範例值 |說明 |
|---|---|---|---|
|Vhost |String |`push.example.com` |域名空間。 |
|Domain |String |`pull.example.com` |域名。 |
|UaAccessRule |[UaAccessRule](https://docs.byteplus.com/en/docs/24/107447#uaaccessrule) 的物件 |`-` |UA 封鎖清單或允許清單詳細資訊。 |

### UaAccessRule

|參數 |資料類型 |範例值 |說明 |
|---|---|---|---|
|AllowEmpty |Boolean |`true` |指定是否將此組態套用至包含空 UA 標頭或不包含 UA 標頭的請求。例如，如果將 **Type** 設定為 **deny**，並將 **AllowEmpty** 設定為 **true**，則包含空 UA 標頭或不包含 UA 標頭的請求將遭到拒絕。<br><br><br>* `true`：套用。<br><br>* `false`：不套用。 |
|Type |String |`deny` |限制類型。<br><br><br>* `allow`：允許清單。<br><br>* `deny`：封鎖清單。 |
|Enable |Boolean |`true` |指定是否啟用 UA 允許清單或封鎖清單。<br><br><br>* `true`：已啟用。<br><br>* `false`：已停用。 |
|UserAgent |String 的陣列 |`["Mozilla/5.0", "*curl*"]` |封鎖清單或允許清單中的 UA 標頭清單。 |

## 範例

### 範例請求

```json
POST https://open.byteplusapi.com/?Action=DescribeUserAgentAccessRule&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "Domain": "pull.example.com"
}
```

### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "202306041104200100*****2280022D31",
        "Action": "DescribeUserAgentAccessRule",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "UserAgentList": [
            {
                "Vhost": "push.example.com",
                "Domain": "pull.example.com",
                "UaAccessRule": {
                    "AllowEmpty": true,
                    "Type": "deny",
                    "Enable": true,
                    "UserAgent": [
                        "curl"
                    ]
                }
            }
        ]
    }
}
```

## 錯誤碼

以下是與目前操作相關的錯誤碼。如需其他錯誤碼，請參閱 [BytePlus OpenAPI 的常見錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。

|狀態碼 |錯誤碼 |錯誤訊息 |說明 |
|---|---|---|---|
|200 |CommonErr |\- |未分類錯誤。建議重試。如果仍傳回此錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |\- |輸入參數無效或不符合要求。請參閱[請求參數](https://docs.byteplus.com/en/docs/24/107447#request-parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |Request parameter error, please check input data |參數驗證失敗。請檢查資料類型是否正確。 |
|403 |RequestForbidden |\- |由於目前帳戶下沒有請求的資源，請求遭到拒絕。資源包括域名空間、域名、應用程式名稱、組態和憑證。 |
|403 |RequestForbidden.AccountIDNotAllow |this AccountID does not have permission to access the corresponding resource, please check the request parameters |由於目前帳戶下沒有請求的資源，請求遭到拒絕。資源包括域名空間、域名、應用程式名稱、組態和憑證。 |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |視訊直播服務尚未啟用，或帳戶欠費，導致帳單不可用。請檢查服務啟用狀態和帳戶欠費狀態。 |
|404 |ResourceNotFound |\- |找不到資源，包括域名空間、域名、應用程式名稱、組態和憑證。建議重試。如果仍傳回此錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|404 |ResourceNotFound.DomainNotExist |domain not found |找不到域名 (Domain)。請檢查傳入的域名是否與實際使用的域名一致。 |
|500 |InternalError |an internal error occurred, please contact the administrator. |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |an internal error related to database occurred, please contact the administrator. |發生與資料庫相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |內部服務逾時。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
