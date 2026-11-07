---
title: "DescribeRelaySourceV3"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describerelaysourcev3-2023-zh-TW"
---

調用 `DescribeRelaySourceV3` API 查詢播放觸發的回源拉流配置。

<span id="Requirements"></span>
## 需求

速率限制：每個帳號每秒最多 10 次查詢。

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=DescribeRelaySourceV3&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了需傳入 API 專屬參數外，還必須帶上 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`DescribeRelaySourceV3` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。當前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |域名空間。可調用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或在 BytePlus MediaLive 控制台的 [域名](https://console.byteplus.com/live/main/domain/list) 頁面獲取該域名所屬的域名空間。 |
|App |String |否 |`live` |直播流 URL 中的 AppName 欄位。如未指定，表示查詢結果不過濾 AppName 欄位。可包含大寫字母（A\-Z）、小寫字母（a\-z）、數字（0\-9）、底線（_）、連字號（\-）及句點（.），長度為 1 到 30 個字元。 |
|Group |String |否 |`relay1` |回源拉流配置組名稱。 |


<span id="Response parameters"></span>
## 回應參數

有關 API 專屬回應參數，請參見下表。更多細節請參考 [請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 章節。


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|RelaySourceConfigList |[RelaySourceConfigList](https://docs.byteplus.com/en/docs/24/107371#relaysourceconfiglist) 陣列 |`-` |回源拉流配置組列表。 |


<span id="relaysourceconfiglist"></span>
### RelaySourceConfigList


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Vhost |String |`push.example.com` |域名空間。 |
|App |String |`live` |AppName 欄位。 |
|GroupDetails |[GroupDetails](https://docs.byteplus.com/en/docs/24/107371#groupdetails) 陣列 |`-` |該組的回源拉流配置。 |


<span id="groupdetails"></span>
### GroupDetails


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Group |String |`relay1` |回源拉流配置組名稱。 |
|Servers |[Servers](https://docs.byteplus.com/en/docs/24/107371#servers) 陣列 |`-` |回源伺服器配置列表。 |


<span id="servers"></span>
### Servers


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|RelaySourceProtocol |String |`rtmp` |串流協議。 |
|RelaySourceDomain |String |`example.org` |回源地址。 |
|RelaySourceParams |JSON Map |`{"key1": "value1","key2": "value2"}` |自定義回源拉流參數。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://open.byteplusapi.com/?Action=DescribeRelaySourceV3&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "App": "live"
}
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "DescribeRelaySource",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "cn-north-1"
    },
    "Result": {
        "RelaySourceConfigList": [
            {
                "Vhost": "push.example.com",
                "App": "live",
                "GroupDetails": [
                    {
                        "Group": "relay1",
                        "Servers": [
                            {
                                "RelaySourceProtocol": "rtmp",
                                "RelaySourceDomain": "example.org",
                                "RelaySourceParams": {
                                    "key1": "value1",
                                    "key2": "value2"
                                }
                            }
                        ]
                    }
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
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回錯誤碼，請 [聯繫支援](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考 [請求參數](https://docs.byteplus.com/en/docs/24/107371#request-parameters) 說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料型別是否正確。 |
|403 |RequestForbidden |*  |請求被拒絕，因當前帳號下無請求資源（資源包括域名空間、域名、App 名稱、配置及憑證）。 |
|403 |RequestForbidden.AccountIDNotAllow |此 AccountID 無權訪問對應資源，請檢查請求參數 |請求被拒絕，因當前帳號下無請求資源（資源包括域名空間、域名、App 名稱、配置及憑證）。 |
|403 |RequestForbidden.BillingStatus |該 AccountID 未開通計費狀態，請開通服務或充值。 |尚未啟用視訊直播服務或帳戶有欠費，導致帳單無法使用。請檢查服務啟用狀態及帳戶欠費狀態。 |
|404 |ResourceNotFound |*  |未找到資源（包括網域名稱空間、網域名稱、應用名稱、組態及憑證）。建議重試。若仍返回錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |發生與資料庫相關的內部錯誤，請聯絡管理員。 |發生與資料庫相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
