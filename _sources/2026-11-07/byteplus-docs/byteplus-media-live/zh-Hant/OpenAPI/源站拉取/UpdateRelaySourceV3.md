---
title: "UpdateRelaySourceV3"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updaterelaysourcev3-2023-zh-TW"
---

呼叫 `UpdateRelaySourceV3` API，以新增或更新播放觸發回源配置。播放觸發回源指的是僅在有觀眾觀看時才觸發回源，能節省源站伺服器的頻寬資源，並提升系統整體效率。

<span id="Requirements"></span>
## 需求

頻率限制：每個帳戶每秒最多 10 次查詢。

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=UpdateRelaySourceV3&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了專屬參數外，還必須帶上 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`UpdateRelaySourceV3` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |該域名所屬的域名空間。你可以呼叫 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或在 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面取得域名空間。 |
|App |String |否 |`live` |直播流 URL 中的 AppName 欄位。若未指定，則配置將套用至所有 AppName。可包含大寫字母（A\-Z）、小寫字母（a\-z）、數字（0\-9）、底線（_）、連字號（\-）及點（.），長度為 1 到 30 字元。 |
|GroupDetails |[GroupDetails](https://docs.byteplus.com/en/docs/24/107388#groupdetails) 陣列 |是 |`-` |回源配置群組列表。若某一配置群組回傳錯誤，系統會依陣列順序自動切換至下一個配置群組。 |


<span id="groupdetails"></span>
### GroupDetails


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Group |String |是 |`relay1` |回源配置群組名稱。 |
|Servers |[Servers](https://docs.byteplus.com/en/docs/24/107388#servers) 陣列 |是 |`-` |回源配置列表。若某一回源地址回傳錯誤，系統會依陣列順序自動切換至下一個地址。 |


<span id="servers"></span>
### Servers


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|RelaySourceDomain |String |是 |`example.org` |直播源伺服器地址，支援填寫源伺服器的域名或 IP 地址。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">當源伺服器使用非預設端口時，支援在回源地址中以 <code>域名:端口</code> 或 <code>IP:端口</code> 的形式配置端口。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">最多可新增 10 個回源地址。回源失敗時，會依你新增的地址順序循環嘗試。</div><br> |
|RelaySourceProtocol |String |是 |`rtmp` |串流協議。支援的值包括：<br><br><br>* `rtmp`<br><br>* `flv`<br><br>* `hls`<br><br>* `dash` |
|RelaySourceParams |JSON Map |否 |`{"key1": "value1", "key2": "value2"}` |自訂回源參數。此參數預設為空。格式為 `"Key":"Value"`，例如 `"domain":"live.push.net"`。 |


<span id="Response parameters"></span>
## 回應參數

此 API 僅在回應中返回 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://open.byteplusapi.com/?Action=UpdateRelaySourceV3&Version=2023-01-01
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
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "Service": "live",
        "Region": "ap-singapore-1",
        "Version": "2023-01-01",
        "Action": "UpdateRelaySourceV3_1h0pbmhmb",
        "RequestId": "202306041104200100100232280022D31"
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為本操作相關的錯誤碼。其他錯誤碼請參見 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**說明** |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回錯誤碼，請 [聯繫客服](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參閱[請求參數](https://docs.byteplus.com/en/docs/24/107388#request-parameters)說明以進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料型別是否正確。 |
|403 |RequestForbidden |*  |因當前帳號下無請求資源（資源包括網域命名空間、網域名稱、應用名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.AccountIDNotAllow |此 AccountID 無權存取對應資源，請檢查請求參數 |因當前帳號下無請求資源（資源包括網域命名空間、網域名稱、應用名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.BillingStatus |該 AccountID 未開通計費狀態，請啟用服務或儲值。 |尚未啟用視訊直播服務或帳號有欠費，導致計費資訊不可用。請檢查服務啟用狀態及帳號欠費狀態。 |
|404 |ResourceNotFound |*  |未找到資源（包含網域命名空間、網域名稱、應用名稱、配置及憑證）。建議重試。若仍返回錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|429 |RequestLimitExceeded.Exist |%s 已存在 |欲建立的資源（包含網域命名空間、網域名稱、應用名稱、配置、憑證）已存在。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |發生與資料庫相關的內部錯誤，請聯絡管理員。 |發生與資料庫相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
