---
title: "DescribeReferer"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describereferer-2023-zh-TW"
---

呼叫 `DescribeReferer` API 查詢 Referer 黑名單或允許名單設定。

## 要求

速率限制：每個帳號每秒 1 次查詢。

## HTTP 請求

* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=DescribeReferer&Version=2023\-01\-01

## 請求參數

### 通用參數

所有 API 除了 API 專屬參數外，還必須使用[通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)呼叫。

### 查詢

|參數 |資料類型 |必填 |範例值 |說明 |
|---|---|---|---|---|
|Action |String |是 |`DescribeReferer` |API 操作。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |

### 主體參數

|參數 |資料類型 |必填 |範例值 |說明 |
|---|---|---|---|---|
|Vhost |String |否 |`push.example.com` |網域名稱空間。您可以呼叫 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或造訪 BytePlus MediaLive 控制台中的[網域](https://console.byteplus.com/live/main/domain/list)頁面，以取得網域名稱空間。<br><br>> **说明**<br><br><br>> 指定 `Vhost` 或 `Domain` 其中之一，請勿同時指定。<br> |
|Domain |String |否 |`pull.example.com` |用於拉流的網域名稱。您可以呼叫 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或造訪 BytePlus MediaLive 控制台中的[網域](https://console.byteplus.com/live/main/domain/list)頁面，以取得網域名稱。<br><br>> **说明**<br><br><br>> 指定 `Vhost` 或 `Domain` 其中之一，請勿同時指定。<br> |

## 回應參數

如需 API 專屬回應參數，請參閱下表。如需詳細資訊，請參閱[請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)章節。

|參數 |資料類型 |範例值 |說明 |
|---|---|---|---|
|RefererList |[RefererList](https://docs.byteplus.com/en/docs/24/107241#refererlist) 陣列 |`-` |查詢結果清單。 |

### RefererList

|參數 |資料類型 |範例值 |說明 |
|---|---|---|---|
|Vhost |String |`push.example.com` |網域名稱空間。 |
|Domain |String |`pull.example.com` |網域名稱。 |
|RefererInfoList |[RefererInfoList](https://docs.byteplus.com/en/docs/24/107241#refererinfolist) 陣列 |`-` |Referer 資訊清單。 |

### RefererInfoList

|參數 |資料類型 |範例值 |說明 |
|---|---|---|---|
|Key |String |`referer` |Referer 設定的名稱，固定為 `referer`。 |
|Type |String |`deny` |Referer 限制類型。可取以下值：<br><br><br>* `deny`：黑名單設定。如果拉流請求符合 Referer 規則，則會被拒絕。<br><br>* `allow`：允許名單設定。如果拉流請求符合 Referer 規則，則會被允許。 |
|Value |String |`example1.com` |Referer 限制規則，即待驗證拉流請求的 Referer 值。可新增完整網域名稱或萬用字元網域名稱。最多可輸入 300 個字元。 |
|Priority |Integer |`0` |已棄用。 |

## 範例

### 範例請求

```json
POST https://open.byteplusapi.com/?Action=DescribeReferer&Version=2023-01-01
{
    "Domain": "pull.example.com"
}
```

### 範例回應

```json
{
    "ResponseMetadata": {
        "Action": "DescribeReferer",
        "Region": "ap-singapore-1",
        "RequestId": "20230604110420****100232280022D31",
        "Service": "live",
        "Version": "2023-01-01"
    },
    "Result": {
        "RefererList": [
            {
                "Domain": "pull.example.com",
                "RefererInfoList": [
                    {
                        "Key": "referer",
                        "Priority": 0,
                        "Type": "deny",
                        "Value": "example1.com"
                    }
                ],
                "Vhost": "push.example.com"
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
|400 |InvalidParam |\- |輸入參數無效或不符合要求。請參閱[請求參數](https://docs.byteplus.com/en/docs/24/107241#request-parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |Request parameter error, please check input data |參數驗證失敗。請檢查資料類型是否正確。 |
|403 |RequestForbidden |\- |請求遭拒，因為目前帳號下沒有請求的資源。資源包括網域名稱空間、網域名稱、應用程式名稱、設定和憑證。 |
|403 |RequestForbidden.AccountIDNotAllow |this AccountID does not have permission to access the corresponding resource, please check the request parameters |請求遭拒，因為目前帳號下沒有請求的資源。資源包括網域名稱空間、網域名稱、應用程式名稱、設定和憑證。 |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |視訊直播服務尚未啟用，或帳號欠費，導致帳單不可用。請檢查服務啟用狀態和帳號欠費狀態。 |
|404 |ResourceNotFound |\- |找不到資源。資源包括網域名稱空間、網域名稱、應用程式名稱、設定和憑證。建議重試。如果仍傳回此錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |an internal error occurred, please contact the administrator. |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |an internal error related to database occurred, please contact the administrator. |發生與資料庫相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.VhostOrDomain |an internal error related to vhost or domain occurred, please contact the administrator. |發生與網域名稱空間 (Vhost) 或網域名稱 (Domain) 相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |內部服務逾時。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
