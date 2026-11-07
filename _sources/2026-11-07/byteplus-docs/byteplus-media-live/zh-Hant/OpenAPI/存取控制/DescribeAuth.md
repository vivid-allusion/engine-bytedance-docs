---
title: "DescribeAuth"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeauth-2023-zh-TW"
---

呼叫 `DescribeAuth` API，查詢符合查詢條件的 URL 鑑權設定。

## 要求

速率限制：每個帳號每秒 1 次查詢。

## HTTP 請求

* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=DescribeAuth&Version=2023\-01\-01

## 請求參數

### 通用參數

呼叫所有 API 時，除了 API 專屬參數外，還必須傳入[通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

### 查詢

|參數 |資料類型 |是否必填 |範例值 |說明 |
|---|---|---|---|---|
|Action |String |是 |`DescribeAuth` |API 操作。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |

### Body 參數

|參數 |資料類型 |是否必填 |範例值 |說明 |
|---|---|---|---|---|
|Vhost |String |否 |`pull.example.com` |域名空間。您可以呼叫 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或前往 BytePlus MediaLive 控制台的[域名管理](https://console.byteplus.com/live/main/domain/list)頁面，以取得域名空間。<br><br>> **说明**<br><br><br>> 應提供 `Vhost` 或 `Domain`，不可同時提供。<br> |
|Domain |String |否 |`pull.example.com` |域名。您可以呼叫 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或前往 BytePlus MediaLive 控制台的[域名管理](https://console.byteplus.com/live/main/domain/list)頁面，以取得域名。<br><br>> **说明**<br><br><br>> 應提供 `Vhost` 或 `Domain`，不可同時提供。<br> |
|App |String |否 |`live` |直播流 URL 中的 AppName 欄位。預設為空，表示查詢所有 AppName。可包含大寫字母 (A\-Z)、小寫字母 (a\-z)、數字 (0\-9)、底線 (_)、連字號 (\-) 和句點 (.)，長度範圍為 1 到 30 個字元。 |
|SceneType |String |是 |`push` |鑑權情境類型，其取值與含義如下。<br><br><br>* `push`：推流鑑權。<br><br>* `pull`：拉流鑑權。 |

## 回應參數

如需 API 專屬的唯一回應參數，請參閱下表。如需更多詳細資訊，請參閱[請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)章節。

|參數 |資料類型 |範例值 |說明 |
|---|---|---|---|
|AuthList |[AuthList](https://docs.byteplus.com/en/docs/24/107311#authlist) 陣列 |`-` |查詢結果清單。 |

### AuthList

|參數 |資料類型 |範例值 |說明 |
|---|---|---|---|
|Vhost |String |`pull.example.com` |域名空間。 |
|Domain |String |`pull.example.com` |域名。 |
|App |String |`live` |AppName 欄位。 |
|SceneType |String |`push` |鑑權情境類型，其取值與含義如下。<br><br><br>* `push`：推流鑑權。<br><br>* `pull`：拉流鑑權。 |
|AuthDetailList |[AuthDetailList](https://docs.byteplus.com/en/docs/24/107311#authdetaillist) 陣列 |`-` |鑑權資訊清單。 |
|ValidDuration |Integer |`604800` |有效期間，單位為秒。 |
|AuthStatus |Boolean |`false` |鑑權狀態。有效值包括：<br><br><br>* `false`：鑑權設定已停用。<br><br>* `true`：鑑權設定已啟用。 |
|TimeStampBase |Integer |`10` |時間戳記的時間格式。有效值：<br><br><br>* `2`：二進位。<br><br>* `8`：八進位。<br><br>* `10`：十進位。<br><br>* `16`：十六進位。<br><br><br>> **说明**<br><br><br>> 當 `SceneType` 的值為 `push` 時，此參數的值固定為 `10`。<br> |

### AuthDetailList

|參數 |資料類型 |範例值 |說明 |
|---|---|---|---|
|SecretKey |String |`1asd111` |用於鑑權的金鑰。 |
|EncryptionAlgorithm |String |`md5` |加密演算法。 |
|AuthField |JSON Map |`{"volcSecret":"sign","volcTime":"expire"}` |推流/拉流位址中鑑權資訊的自訂參數名稱。 |
|EncryptField |String 陣列 |`["key","volcTime","Domain"]` |您用於鑑權的資訊。 |
|AuthType |String |`TypeB` |URL 鑑權類型。有效值：<br><br><br>* `TypeA`：Type A。<br><br>* `TypeB`：Type B。<br><br>* `TypeC`：Type C。<br><br>* `TypeCustom`：自訂類型。<br><br><br>> **说明**<br><br><br>> 如需 A、B 或 C 類型的更多資訊，請參閱[設定 URL 鑑權](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-url-authentication)。<br> |

## 範例

### 範例請求

```json
POST https://open.byteplusapi.com/?Action=DescribeAuth&Version=2023-01-01
{
    "Vhost": "pull.example.com",
    "SceneType": "push"
}
```

### 範例回應

```json
{
    "ResponseMetadata": {
        "Action": "DescribeAuth",
        "Region": "ap-singapore-1",
        "RequestId": "20230604110420****100232280022D31",
        "Service": "live",
        "Version": "2023-01-01"
    },
    "Result": {
        "AuthList": [
            {
                "App": "live",
                "AuthDetailList": [
                    {
                        "SecretKey": "1asd111",
                        "EncryptionAlgorithm": "md5",
                        "AuthField": {},
                        "EncryptField": [],
                        "AuthType": "TypeB"
                    }
                ],
                "AuthStatus": false,
                "Domain": "pull.example.com",
                "SceneType": "push",
                "ValidDuration": 604800,
                "Vhost": "pull.example.com",
                "TimeStampBase": 10
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
|400 |InvalidParam |\- |輸入參數無效或不符合要求。請參閱[請求參數](https://docs.byteplus.com/en/docs/24/107311#request-parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |Request parameter error, please check input data |參數驗證失敗。請檢查資料類型是否正確。 |
|403 |RequestForbidden |\- |請求遭拒，因為目前帳號下沒有請求的資源（資源包括域名空間、域名、應用程式名稱、設定和憑證）。 |
|403 |RequestForbidden.AccountIDNotAllow |this AccountID does not have permission to access the corresponding resource, please check the request parameters |請求遭拒，因為目前帳號下沒有請求的資源（資源包括域名空間、域名、應用程式名稱、設定和憑證）。 |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |影片直播服務尚未啟用，或帳號欠費，導致帳單不可用。請檢查服務啟用狀態和帳號欠費狀態。 |
|404 |ResourceNotFound |\- |找不到資源（包括域名空間、域名、應用程式名稱、設定和憑證）。建議重試。如果仍傳回此錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|404 |ResourceNotFound.VhostNotExist |vhost not found |找不到域名空間 (Vhost)。請檢查傳入的域名空間是否與實際使用的域名空間一致。 |
|500 |InternalError |an internal error occurred, please contact the administrator. |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |an internal error related to database occurred, please contact the administrator. |發生資料庫相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |內部服務逾時。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
