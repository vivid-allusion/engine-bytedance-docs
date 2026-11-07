---
title: "DescribeCallback"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describecallback-2023-zh-TW"
---

調用 `DescribeCallback` API 以獲取應用程式的回調配置。

<span id="Requirements"></span>
## 需求

速率限制：每個帳戶每秒 1 次查詢。

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=DescribeCallback&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了需傳遞 API 專屬參數外，還必須帶上 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`DescribeCallback` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。當前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Vhost |String |否 |`push.example.com` |域名空間。可調用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或前往 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面，獲取該域名所屬的域名空間。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">必須指定 <code>Vhost</code> 或 <code>Domain</code>，不可同時指定。</div><br> |
|Domain |String |否 |`push.example.com` |推流域名。可調用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或前往 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面，獲取域名。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">必須指定 <code>Vhost</code> 或 <code>Domain</code>，不可同時指定。</div><br> |
|App |String |否 |`Live` |直播流 URL 中的 AppName 欄位。可包含大寫字母（A\-Z）、小寫字母（a\-z）、數字（0\-9）、底線（_）、連字號（\-）及句點（.），長度為 1 至 30 個字元。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">若指定 Vhost 且未指定 App，則會查詢該域名空間下的所有應用。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">若指定 Domain，則不可指定 App。</div><br> |
|MessageType |String |否 |`push` |要接收的回調訊息類型。有效值包括：<br><br><br>* `push`：推流開始時觸發回調。<br><br>* `push_end`：推流結束時觸發回調。<br><br>* `snapshot`：截圖事件發生時觸發回調。<br><br>* `record`：錄製事件發生時觸發回調。 |


<span id="Response parameters"></span>
## 回應參數

有關 API 專屬回應參數，請參見下表。更多詳情請參考 [請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 章節。


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|CallbackList |[CallbackList](https://docs.byteplus.com/en/docs/24/107395#callbacklist) 陣列 |`-` |回調資訊列表。 |


<span id="callbacklist"></span>
### CallbackList


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|MessageType |String |`push` |要接收的回調訊息類型。有效值包括：<br><br><br>* `push`：推流開始時觸發回調。<br><br>* `push_end`：推流結束時觸發回調。<br><br>* `snapshot`：截圖事件發生時觸發回調。<br><br>* `record`：錄製事件發生時觸發回調。 |
|Vhost |String |`push.example.com` |域名空間。 |
|App |String |`push.example.com` |應用名稱。 |
|TranscodeCallback |Integer |`0` |定義是否接收轉碼流的回調。<br><br><br>* `0`：否。<br><br>* `1`：是。 |
|CallbackDetailList |[CallbackDetailList](https://docs.byteplus.com/en/docs/24/107395#callbackdetaillist) 陣列 |`-` |回調地址資訊列表。 |
|CreateTime |String |`2021-01-02 15:04:05` |回調配置的建立時間。 |
|CreateTimeUTC |String |`2021-01-02T15:04:05Z` |回調配置的建立時間（RFC 3339 格式 UTC 時間，精確到秒）。 |
|AuthKeyPrimary |String |`1622194197-0-0-5552*****e4e20387c6dc18afce****` |回調金鑰。 |
|AuthEnable |Boolean |`false` |是否啟用驗證。<br><br><br>* `false`：未啟用驗證。<br><br>* `true`：已啟用驗證。 |


<span id="callbackdetaillist"></span>
### CallbackDetailList


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|CallbackType |字串 |`http` |所使用的回調地址類型。若返回`http`，表示同時支援 HTTP 與 HTTPS。 |
|URL |字串 |`http://example.com/callback` |回調地址，長度為 1 到 100 個字元。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```json
POST https://open.byteplusapi.com/?Action=DescribeCallback&Version=2023-01-01
{
    "Vhost": "push.example.com"
}
```


<span id="Sample response"></span>
### 回應範例

```json
{
    "ResponseMetadata": {
        "RequestID": "202108291443190102121532040E197F15",
        "Action": "DescribeCallback",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "CallbackList": [
            {
                "App": "live",
                "AuthEnable": false,
                "AuthKeyPrimary": "",
                "CallbackDetailList": [
                    {
                        "CallbackType": "http",
                        "URL": "http://example.com/callback"
                    }
                ],
                "CreateTime": "2021-01-02 23:04:05",
                "CreateTimeUTC": "2021-01-02T15:04:05Z",
                "Domain": "",
                "MessageType": "push",
                "TranscodeCallback": 0,
                "Vhost": "push.live.example.com"
            }
        ]
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為與本操作相關的錯誤碼。其他錯誤碼請參見 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**說明** |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回錯誤碼，請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考[請求參數](https://docs.byteplus.com/en/docs/24/107395#request-parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料型態是否正確。 |
|403 |RequestForbidden |*  |因目前帳戶下無請求資源（資源包含網域名稱空間、網域名稱、應用名稱、配置與憑證），請求被拒絕。 |
|403 |RequestForbidden.AccountIDNotAllow |此 AccountID 無權存取對應資源，請檢查請求參數 |因目前帳戶下無請求資源（資源包含網域名稱空間、網域名稱、應用名稱、配置與憑證），請求被拒絕。 |
|403 |RequestForbidden.BillingStatus |此 AccountID 的帳單狀態不可用，請啟用服務或儲值。 |尚未啟用視訊直播服務或帳戶欠費，導致帳單不可用。請檢查服務啟用狀態及帳戶欠費狀態。 |
|404 |ResourceNotFound |*  |未找到資源（包含網域名稱空間、網域名稱、應用名稱、配置與憑證）。建議重試。若仍返回錯誤碼，請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|404 |ResourceNotFound.VhostNotExist |未找到 vhost |未找到網域名稱空間（Vhost）。請檢查傳入的網域名稱空間是否與實際使用的一致。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |發生與資料庫相關的內部錯誤，請聯絡管理員。 |發生與資料庫相關的內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
