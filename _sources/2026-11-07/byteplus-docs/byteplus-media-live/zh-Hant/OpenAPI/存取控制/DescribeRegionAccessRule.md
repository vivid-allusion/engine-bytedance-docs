---
title: "DescribeRegionAccessRule"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeregionaccessrule-zh-TW"
---

呼叫 `DescribeRegionAccessRule` API，查詢指定網域名稱的地理位置限制。

## 要求

速率限制：每個帳號每秒 10 次查詢。

## HTTP 請求

* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=DescribeRegionAccessRule&Version=2023\-01\-01

## 請求參數

### 通用參數

呼叫所有 API 時，除 API 特定參數外，還必須使用[通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

### 查詢

|參數 |資料類型 |必填 |範例值 |說明 |
|---|---|---|---|---|
|Action |String |是 |`DescribeRegionAccessRule` |API 操作。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |

### Body 參數

|參數 |資料類型 |必填 |範例值 |說明 |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |網域名稱空間。您可以呼叫 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或前往 BytePlus MediaLive 主控台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面取得網域名稱空間。 |
|Domain |String |是 |`push.example.com` |用於拉流或推流的網域名稱。您可以呼叫 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或前往 BytePlus MediaLive 主控台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面取得網域名稱。 |

## 回應參數

如需 API 特定的唯一回應參數，請參閱下表。如需更多詳細資訊，請參閱[請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)章節。

|參數 |資料類型 |範例值 |說明 |
|---|---|---|---|
|AccessRuleLists |[AccessRuleLists](https://docs.byteplus.com/en/docs/24/107312#accessrulelists) 陣列 |`-` |地理位置限制。 |

### AccessRuleLists

|參數 |資料類型 |範例值 |說明 |
|---|---|---|---|
|Vhost |String |`push.example.com` |網域名稱空間。 |
|Domain |String |`pull.example.com` |用於拉流的網域名稱。 |
|RegionAccessRule |[RegionAccessRule](https://docs.byteplus.com/en/docs/24/107312#regionaccessrule) 物件 |`-` |地理位置限制。 |

### RegionAccessRule

|參數 |資料類型 |範例值 |說明 |
|---|---|---|---|
|Type |String |`allow` |存取規則類型。<br><br><br>* `allow`：僅允許來自指定地區的請求存取您的網域名稱。<br><br>* `deny`：禁止來自指定地區的請求存取您的網域名稱。 |
|Enable |String |`true` |是否啟用設定。<br><br><br>* `true`：已啟用設定。<br><br>* `false`：已停用設定。 |
|CountryList |String 陣列 |`CN` |允許清單或封鎖清單中的國家和地區。使用 ISO 3166\-1 代碼表示國家和地區，例如 CN、SG 或 US。 |
|ProvinceList |String 陣列 |`HK` |允許清單或封鎖清單中的省份，目前僅支援中國的香港、澳門和台灣地區。對應代碼分別為 HK、MO 和 TW。 |

## 範例

### 範例請求

```json
POST https://open.byteplusapi.com/?Action=DescribeRegionAccessRule&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "Domain": "pull.example.com"
}
```

### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "202306041104200100100232280022D31",
        "Action": "DescribeRegionAccessRule",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "AccessRuleLists": [
            {
                "Vhost": "push.example.com",
                "Domain": "pull.example.com",
                "RegionAccessRule": {
                    "Type": "deny",
                    "Enable": true,
                    "RegionList": [
                        "CN",
                        "region2"
                    ]
                }
            }
        ]
    }
}
```

## 錯誤碼

以下是與目前操作相關的錯誤碼。如需其他錯誤碼，請參閱 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。

|狀態碼 |錯誤碼 |錯誤訊息 |說明 |
|---|---|---|---|
|200 |CommonErr |\- |未分類錯誤。建議重試。如果仍傳回此錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |\- |輸入參數無效或不符合要求。請參閱[請求參數](https://docs.byteplus.com/en/docs/24/107312#request-parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |Request parameter error, please check input data |參數驗證失敗。請檢查資料類型是否正確。 |
|400 |InvalidParam.DomainAndApp |domain and app exist can not exist at the same time |您不能同時傳入 Domain 和 App。請修改輸入參數。 |
|403 |RequestForbidden |\- |因目前帳號下沒有請求的資源，請求遭到拒絕。資源包括網域名稱空間、網域名稱、應用程式名稱、設定和憑證。 |
|403 |RequestForbidden.AccountIDNotAllow |this AccountID does not have permission to access the corresponding resource, please check the request parameters |因目前帳號下沒有請求的資源，請求遭到拒絕。資源包括網域名稱空間、網域名稱、應用程式名稱、設定和憑證。 |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |視訊直播服務尚未啟用，或帳號欠費，導致帳單不可用。請檢查服務啟用狀態和帳號欠費狀態。 |
|404 |ResourceNotFound |\- |找不到資源，包括網域名稱空間、網域名稱、應用程式名稱、設定和憑證。建議重試。如果仍傳回此錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|404 |ResourceNotFound.DomainNotExist |domain not found |找不到網域名稱 (Domain)。請檢查傳入的網域名稱是否與實際使用的網域名稱一致。 |
|500 |InternalError |an internal error occurred, please contact the administrator. |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |an internal error related to database occurred, please contact the administrator. |發生與資料庫相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |內部服務逾時。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
