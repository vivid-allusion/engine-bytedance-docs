---
title: "DescribeRemoteAuth"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeremoteauth-2023-zh-TW"
---

呼叫 `DescribeRemoteAuth` API，查詢拉流網域的遠端鑑權設定。

## 要求

速率限制：每個帳戶每秒 10 次查詢

## HTTP 請求

* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=DescribeRemoteAuth&Version=2023\-01\-01

## 請求參數

### 公共參數

所有 API 除了 API 專屬參數外，還必須搭配[公共參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)呼叫。

### Query

|參數 |資料類型 |必填 |範例值 |說明 |
|---|---|---|---|---|
|Action |String |是 |`DescribeRemoteAuth` |API 操作。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |

### Body 參數

|參數 |資料類型 |必填 |範例值 |說明 |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |需要設定遠端鑑權的拉流網域名稱所屬的網域名稱空間。您可以呼叫 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或前往 BytePlus MediaLive 控制台的[網域](https://console.byteplus.com/live/main/domain/list)頁面，取得要查詢的網域名稱空間。 |
|Domain |String |是 |`pull.example.com` |需要設定遠端鑑權的拉流網域名稱。您可以呼叫 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或前往 BytePlus MediaLive 控制台的[網域](https://console.byteplus.com/live/main/domain/list)頁面，取得要查詢的網域。 |

## 回應參數

如需 API 專屬的唯一回應參數，請參閱下表。如需更多詳細資訊，請參閱[請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)章節。

|參數 |資料類型 |範例值 |說明 |
|---|---|---|---|
|Enable |Boolean |`true` |是否啟用目前的遠端鑑權設定。取值及含義如下。<br><br><br>* `true`：啟用；<br><br>* `false`：停用。 |
|AuthURL |String |`http://remoteauth.com` |遠端鑑權伺服器位址，支援 HTTP/HTTPS 通訊協定位址，也支援填入伺服器 IP 位址。遠端鑑權伺服器使用的預設連接埠為 80/443。若使用非預設連接埠，支援以 `domain name:port` 或 `IP:port` 格式設定。 |
|AuthURLPath |String |`/auth` |自訂遠端鑑權請求路徑，在 `UseUserRequest` 設為 `false` 時為必填。 |
|UseUserRequest |Boolean |`false` |遠端鑑權請求路徑使用使用者請求路徑或自訂請求路徑。取值及含義如下。<br><br><br>* `true`：使用使用者請求路徑，並將使用者請求路徑拼接到鑑權請求位址。<br><br>* `false`：自訂遠端鑑權請求路徑。 |
|Method |String |`POST` |鑑權請求方法，其取值及含義如下。<br><br><br>* `POST`：請求資料會作為請求主體傳送至伺服器；<br><br>* `GET`：請求資料包含在 URL 中。 |
|Timeout |Float |`10` |單次鑑權請求的逾時時間，預設為 1，單位為秒，取值範圍為 [0, 600]。 |
|DenyOnFailed |Boolean |`false` |發生請求異常時，是否視為鑑權失敗，取值及含義如下。<br><br><br>* `true`：鑑權失敗；<br><br>* `false`：鑑權成功。<br><br><br>> **说明**<br><br><br>> 請求無法到達鑑權伺服器時會發生異常，例如請求逾時、請求連接埠與鑑權伺服器連接埠不相符等。<br> |
|RetryTimes |Float |`3` |鑑權請求逾時後的重試次數，預設為 3 次，取值範圍為 [0, 10]。 |
|RetryInterval |Float |`10` |鑑權請求逾時後重試之間的時間間隔，單位為秒，預設為 10，取值範圍為 [1, 30]。 |
|QueryParamConfig |[ParamConfig](https://docs.byteplus.com/en/docs/24/107317#paramconfig) 物件 |`-` |鑑權請求 URL 參數設定。 |
|HeaderParamConfig |[ParamConfig](https://docs.byteplus.com/en/docs/24/107317#paramconfig) 物件 |`-` |鑑權請求 Header 參數設定。 |
|HeaderHost |String |`remoteauth.com` |自訂鑑權請求標頭中 Host 參數的值，不支援輸入空格，最大長度為 1024 個字元。 |
|BodyParams |[Params](https://docs.byteplus.com/en/docs/24/107317#params) 陣列 |`-` |鑑權請求 Body 參數設定。<br><br>> **说明**<br><br><br>> 當鑑權請求方法為 POST 時，支援設定鑑權請求的 Body 參數。<br> |
|AllowStatus |Integer 陣列 |`[200,201,202]` |鑑權成功時，鑑權伺服器傳回的狀態碼。所有狀態碼都應在 [200, 499] 範圍內，且不得與 DenyStatus 重複。 |
|DenyRule |[DenyRule](https://docs.byteplus.com/en/docs/24/107317#denyrule) 物件 |`-` |鑑權失敗時，鑑權伺服器傳回的狀態碼。所有狀態碼都應在 [200, 499] 範圍內，且不得與 AllowStatus 重複。 |
|DenyReturnCode |Float |`403` |鑑權失敗時，MediaLive 傳回給用戶端的狀態碼應在 [400, 699] 範圍內。 |
|DenyOtherStatus |Boolean |`true` |當鑑權伺服器傳回的狀態碼不在已定義的鑑權成功或鑑權失敗狀態碼中時，將其視為鑑權成功或鑑權失敗，取值及含義如下。<br><br><br>* `true`：鑑權失敗；<br><br>* `false`：鑑權成功。 |
|CacheConfig |[CacheConfig](https://docs.byteplus.com/en/docs/24/107317#cacheconfig) 物件 |`-` |鑑權快取設定。當設定為空時，表示不使用快取判斷鑑權結果。 |
|EnableHLSAuth |Boolean |`true` |是否啟用 HLS 通訊協定拉流請求的鑑權開關，取值及含義如下。<br><br><br>* `true`：啟用；<br><br>* `false`：停用。 |
|EnableHLSTSAuth |Boolean |`true` |是否對 HLS 通訊協定串流的 TS 片段啟用遠端鑑權，取值及含義如下。<br><br><br>* `true`：啟用；<br><br>* `false`：停用。<br><br><br>> **说明**<br><br><br>> 啟用 HLS 通訊協定拉流請求的遠端鑑權開關時，必須啟用 TS 片段的遠端鑑權。<br> |

### ParamConfig

|參數 |資料類型 |範例值 |說明 |
|---|---|---|---|
|UseUserParam |Boolean |`true` |遠端鑑權請求的 URL 或 Header 參數，是否使用使用者請求參數或自訂參數，取值及含義如下。<br><br><br>* `true`：使用使用者請求參數；<br><br>* `false`：自訂參數。 |
|Params |[Params](https://docs.byteplus.com/en/docs/24/107317#params) 陣列 |`-` |自訂參數時的參數設定，支援常數參數和變數參數總計不超過 25 個，並提取不超過 25 個使用者請求參數。 |

### Params

|參數 |資料類型 |範例值 |說明 |
|---|---|---|---|
|Type |String |`const_string` |參數類型，其取值及含義如下。<br><br><br>* `const_string`：常數；<br><br>* `header`：使用者請求的 Header 參數；<br><br>* `query`：使用者請求的 URL 參數；<br><br>* `vhost`：值為變數 vhost 的參數，表示拉流請求中網域名稱所屬的網域名稱空間；<br><br>* `domain`：值為變數 domain 的參數，表示拉流請求中使用的網域名稱；<br><br>* `app`：值為變數 app 的參數，表示拉流請求中使用的 AppName；<br><br>* `stream`：值為變數 stream 的參數，表示拉流請求中使用的 StreamName；<br><br>* `client_ip`：值為變數 client_ip 的參數，表示拉流用戶端的 IP 位址；<br><br>* `server_ip`：值為變數 server_ip 的參數，表示回應拉流請求的 CDN 節點 IP 位址；<br><br>* `request_uri`：值為變數 request_uri 的參數，表示拉流請求位址的 URI。 |
|ParamName |String |`name` |參數名稱，最大長度為 100 個字元，不支援空格。<br><br>> **说明**<br><br><br><br>* > 當參數類型為常數時，表示常數參數的參數名稱。<br><br><br>* > 當參數類型為使用者請求的 Header 參數或 URL 參數時，表示從使用者請求中提取對應參數。<br><br><br>* > 當參數類型為變數時，不生效。<br> |
|ToName |String |`Name` |新參數名稱，最大長度為 100 個字元，預設為空，表示不設定新參數名稱，且不支援空格。<br><br>> **说明**<br><br><br><br>* > 當參數類型為常數時，不生效；<br><br><br>* > 當參數類型為使用者請求的 Header 參數或 URL 參數時，表示鑑權請求期間使用 ToName 值，取代使用者請求中的對應參數名稱；<br><br><br>* > 當參數類型為變數時，表示將 ToName 的值作為此變數的參數名稱。<br> |
|Value |String |`website` |參數類型為常數時的參數值，最大長度為 100 個字元，不支援空格。 |

### DenyRule

|參數 |資料類型 |範例值 |說明 |
|---|---|---|---|
|DenyStatus |Float 陣列 |`[403,404]` |鑑權失敗時，鑑權伺服器傳回的狀態碼。所有狀態碼都應在 [200, 499] 範圍內，且不得與 AllowStatus 重複。 |

### CacheConfig

|參數 |資料類型 |範例值 |說明 |
|---|---|---|---|
|UseSameCache |Boolean |`false` |是否對成功和失敗的鑑權使用相同設定，包括快取鍵值和快取到期時間。<br><br><br>* `true`：使用相同設定；<br><br>* `false`：不使用相同設定。 |
|CacheExpireSecond |Float |`1800` |快取到期時間，預設值 `0` 表示不快取，單位為秒，取值範圍為 [0, 3600]。<br><br>> **说明**<br><br><br><br>* > 當成功和失敗的鑑權使用相同設定時，表示鑑權快取到期時間；<br><br><br>* > 當成功和失敗的鑑權不使用相同設定時，表示成功鑑權快取的到期時間。<br> |
|CacheKeys |[Keys](https://docs.byteplus.com/en/docs/24/107317#keys) 物件 |`-` |用於產生鑑權結果快取鍵的參數設定，最多支援 50 個參數。<br><br>> **说明**<br><br><br><br>* > 當成功和失敗的鑑權使用相同設定時，表示鑑權結果的快取鍵設定；<br><br><br>* > 當成功和失敗的鑑權不使用相同設定時，表示成功鑑權快取的到期時間。<br> |
|DenyExpireSecond |Float |`1800` |鑑權失敗快取的到期時間，當預設值為 `0` 時表示不快取，單位為秒，取值範圍為 [0, 3600]。<br><br>> **说明**<br><br><br>> 當成功和失敗的鑑權不使用相同設定時生效，即 `UseSameCache` 設定為 `false` 時。<br> |
|DenyKeys |[Keys](https://docs.byteplus.com/en/docs/24/107317#keys) 物件 |`-` |用於產生鑑權失敗結果快取鍵的參數設定，最多支援 50 個參數。<br><br>> **说明**<br><br><br>> 當成功和失敗的鑑權不使用相同設定時生效，即 `UseSameCache` 設定為 `false` 時。<br> |

### Keys

|參數 |資料類型 |範例值 |說明 |
|---|---|---|---|
|Type |String |`header` |用於產生快取鍵的參數類型，其取值及含義如下。<br><br><br>* `query`：使用者拉流請求的 URL 參數；<br><br>* `header`：使用者拉流請求的 Header 參數；<br><br>* `vhost`：使用使用者拉流所在網域的 vhost 值作為參數；<br><br>* `domain`：使用使用者拉流請求的 domain 值作為參數；<br><br>* `app`：使用使用者拉流請求中的 AppName 值作為參數；<br><br>* `stream`：使用使用者拉流請求中的 StreamName 值作為參數；<br><br>* `client_ip`：使用拉流使用者用戶端的 IP 位址作為參數；<br><br>* `request_uri`：使用拉流請求位址的 URI 作為參數。 |
|ParamName |String |`host` |參數名稱，當參數類型為 query 或 Header 時生效且為必填，表示使用指定拉流請求中參數名稱對應的參數值，作為產生快取鍵的參數。 |

## 範例

### 範例請求

```json
POST https://open.byteplusapi.com/?Action=DescribeRemoteAuth&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "Domain": "pull.example.com"
}
```

### 範例回應

```json
{
    "ResponseMetadata": {
        "Action": "DescribeRemoteAuth",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1",
        "RequestId": "202306041104200100100232280022D31"
    },
    "Result": {
        "Enable": true,
        "AuthURL": "http://remoteauth.com",
        "AuthURLPath": "/auth",
        "UseUserRequest": true,
        "Method": "POST",
        "Timeout": 10,
        "RetryTimes": 3,
        "RetryInterval": 10,
        "DenyRule": {
            "DenyStatus": [
                400
            ]
        },
        "DenyReturnCode": 403,
        "CacheConfig": {
            "CacheExpireSecond": 1800,
            "DenyExpireSecond": 1800,
            "CacheKeys": {
                "Type": "header",
                "ParamName": "host"
            },
            "DenyKeys": {
                "Type": "query",
                "ParamName": "lr"
            },
            "UseSameCache": true
        },
        "EnableHLSAuth": true,
        "EnableHLSTSAuth": true,
        "HeaderHost": "remoteauth.com",
        "QueryParamConfig": {
            "UseUserParam": true,
            "Params": [
                {
                    "Type": "query",
                    "ParamName": "lr",
                    "ToName": "LR",
                    "Value": "lang_en"
                }
            ]
        },
        "HeaderParamConfig": {
            "UseUserParam": true,
            "Params": [
                {
                    "Type": "header",
                    "ParamName": "Accept",
                    "ToName": "Accept",
                    "Value": "text/html"
                }
            ]
        },
        "BodyParams": [
            {
                "Type": "const_string",
                "ParamName": "name",
                "ToName": "Name",
                "Value": "website"
            }
        ],
        "AllowStatus": [
            200,
            202
        ],
        "DenyOnFailed": true,
        "DenyOtherStatus": false
    }
}
```

## 錯誤碼

以下為與目前操作相關的錯誤碼。如需其他錯誤碼，請參閱 [BytePlus OpenAPI 公共錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。

|狀態碼 |錯誤碼 |錯誤訊息 |說明 |
|---|---|---|---|
|200 |CommonErr |\- |未分類錯誤。建議重試。如果仍傳回此錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |\- |輸入參數無效或不符合要求。請參閱[請求參數](https://docs.byteplus.com/en/docs/24/107317#request-parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |Request parameter error, please check input data |參數驗證失敗。請檢查資料類型是否正確。 |
|400 |InvalidParam.Format |%s format error |參數格式不正確。請檢查錯誤訊息中指定的參數是否存在非法字元或 URL 格式錯誤。 |
|400 |InvalidParam.DomainAndApp |domain and app exist can not exist at the same time |您不能同時傳入 Domain 和 App。請修改輸入參數。 |
|403 |RequestForbidden |\- |請求遭拒，因為目前帳戶下沒有請求的資源（資源包括網域名稱空間、網域名稱、應用程式名稱、設定和憑證）。 |
|403 |RequestForbidden.AccountIDNotAllow |this AccountID does not have permission to access the corresponding resource, please check the request parameters |請求遭拒，因為目前帳戶下沒有請求的資源（資源包括網域名稱空間、網域名稱、應用程式名稱、設定和憑證）。 |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |視訊直播服務尚未啟用，或帳戶欠費，導致帳單不可用。請檢查服務啟用狀態和帳戶欠費狀態。 |
|404 |ResourceNotFound |\- |找不到資源（包括網域名稱空間、網域名稱、應用程式名稱、設定和憑證）。建議重試。如果仍傳回此錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |an internal error occurred, please contact the administrator. |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |an internal error related to database occurred, please contact the administrator. |發生與資料庫相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |Internal Service 逾時。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
