---
title: "DescribeFormatAccessRule"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeformataccessrule-zh-TW"
---

呼叫 `DescribeFormatAccessRule` API 查詢協定限制。

## 要求

速率限制：每個帳號每秒 10 次查詢。

## HTTP 請求

* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=DescribeFormatAccessRule&Version=2023\-01\-01

## 請求參數

### 公共參數

所有 API 除了 API 特定參數外，還必須搭配[公共參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)呼叫。

### 查詢

|參數 |資料類型 |必填 |範例值 |說明 |
|---|---|---|---|---|
|Action |String |是 |`DescribeFormatAccessRule` |API 操作。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |

### Body 參數

|參數 |資料類型 |必填 |範例值 |說明 |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |網域名稱空間。您可以呼叫 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或前往 BytePlus MediaLive 控制台的[網域](https://console.byteplus.com/live/main/domain/list)頁面取得網域名稱空間。 |
|Domain |String |是 |`pull.example.com` |用於拉流的網域名稱。您可以呼叫 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或前往 BytePlus MediaLive 控制台的[網域](https://console.byteplus.com/live/main/domain/list)頁面取得網域名稱。 |

## 回應參數

如需 API 特定的唯一回應參數，請參閱下表。如需詳細資訊，請參閱[請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)章節。

|參數 |資料類型 |範例值 |說明 |
|---|---|---|---|
|AccessRuleLists |[AccessRuleLists](https://docs.byteplus.com/en/docs/24/107348#accessrulelists) 的陣列 |`-` |協定限制。 |

### AccessRuleLists

|參數 |資料類型 |範例值 |說明 |
|---|---|---|---|
|Vhost |String |`push.example.com` |網域名稱空間。 |
|Domain |String |`pull.example.com` |用於拉流的網域名稱。 |
|FormatAccessRule |[FormatAccessRule](https://docs.byteplus.com/en/docs/24/107348#formataccessrule) 的物件 |`-` |協定限制。 |

### FormatAccessRule

|參數 |資料類型 |範例值 |說明 |
|---|---|---|---|
|Type |String |`deny` |存取控制類型。唯一支援的值為 `deny`，會封鎖透過封鎖清單中協定的拉流。 |
|Enable |String |`true` |是否啟用設定。<br><br><br>* `true`：設定已啟用。<br><br>* `false`：設定已停用。 |
|FormatList |String 陣列 |`["flv","hls"]` |協定清單。有效選項包括：<br><br><br>* `flv`<br><br>* `hls`<br><br>* `rtmp`<br><br>* `webrtc`，表示 RTM 協定 |

## 範例

### 範例請求

```json
POST https://open.byteplusapi.com/?Action=DescribeFormatAccessRule&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "Domain": "pull.example.com"
}
```

### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeFormatAccessRule",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "AccessRuleLists": [
            {
                "Vhost": "push.example.com",
                "Domain": "pull.example.com",
                "FormatAccessRule": {
                    "Type": "deny",
                    "Enable": "true",
                    "FormatList": [
                        "flv",
                        "hls"
                    ]
                }
            }
        ]
    }
}
```

## 錯誤碼

以下是與目前操作相關的錯誤碼。如需其他錯誤碼，請參閱 [BytePlus OpenAPI 公共錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。

|狀態碼 |錯誤碼 |錯誤訊息 |說明 |
|---|---|---|---|
|200 |CommonErr |\- |未分類的錯誤。建議重試。如果仍傳回該錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |\- |輸入參數無效或不符合要求。請參閱[請求參數](https://docs.byteplus.com/en/docs/24/107348#request-parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |Request parameter error, please check input data |參數驗證失敗。請檢查資料類型是否正確。 |
|403 |RequestForbidden |\- |請求遭拒，因為目前帳號下沒有請求的資源。資源包括網域名稱空間、網域名稱、應用程式名稱、設定和憑證。 |
|403 |RequestForbidden.AccountIDNotAllow |this AccountID does not have permission to access the corresponding resource, please check the request parameters |請求遭拒，因為目前帳號下沒有請求的資源。資源包括網域名稱空間、網域名稱、應用程式名稱、設定和憑證。 |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |視訊直播服務尚未啟用，或帳號欠費，導致帳單不可用。請檢查服務啟用狀態和帳號欠費狀態。 |
|404 |ResourceNotFound |\- |找不到資源。資源包括網域名稱空間、網域名稱、應用程式名稱、設定和憑證。建議重試。如果仍傳回該錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|404 |ResourceNotFound.DomainNotExist |domain not found |找不到網域名稱 (Domain)。請檢查傳入的網域名稱是否與實際使用的網域名稱一致。 |
|500 |InternalError |an internal error occurred, please contact the administrator. |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |an internal error related to database occurred, please contact the administrator. |發生與資料庫相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |內部服務逾時。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
