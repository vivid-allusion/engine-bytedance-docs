---
title: "GeneratePushURL"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generatepushurl-2023-zh-TW"
---

呼叫 `GeneratePushURL` API，以產生指定串流的推流地址。

<span id="Requirements"></span>
## 需求

頻率限制：每個帳戶每秒最多 25 次查詢。

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=GeneratePushURL&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了需傳入 API 專屬參數外，還必須帶入 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型態** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`GeneratePushURL` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型態** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Domain |String |是 |`push.example.com` |推流用的網域名稱。您可以呼叫 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或在 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面取得網域名稱。 |
|App |String |是 |`live` |推流 URL 中的 AppName 欄位。可包含大寫字母（A\-Z）、小寫字母（a\-z）、數字（0\-9）、底線（_）、連字號（\-）及點（.），長度為 1 至 30 字元。 |
|Stream |String |是 |`example_stream` |推流 URL 中的 StreamName 欄位。可包含大寫字母（A\-Z）、小寫字母（a\-z）、數字（0\-9）、底線（_）、連字號（\-）及點（.），長度為 1 至 100 字元。 |
|ValidDuration |Integer |否 |`5000` |地址自產生時起，會在 `ValidDuration` 指定的時間長度後過期。單位：秒。有效範圍：\> 0。預設值：604800（七天）。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">推流地址過期後，正在進行的推流不會受到影響。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">若同時設定 <code>ValidDuration</code> 與 <code>ExpiredTime</code>，僅 <code>ExpiredTime</code> 的設定會生效。</div><br> |
|ExpiredTime |String |否 |`2023-08-19T16:07:25Z` |地址的過期時間（RFC 3339 格式的本地時間，精確到秒），單位為秒。預設過期時間為地址產生後七天。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">推流地址過期後，正在進行的推流不會受到影響。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">若同時設定 <code>ValidDuration</code> 與 <code>ExpiredTime</code>，僅 <code>ExpiredTime</code> 的設定會生效。</div><br> |


<span id="Response parameters"></span>
## 回應參數

如需 API 專屬回應參數，請參閱下表。更多細節請參考 [請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 章節。


|**參數** |**資料型態** |**範例值** |**說明** |
|---|---|---|---|
|PushURLList |String 陣列 |`["rtmp://push.example.com/live/example_stream"]` |RTMP 推流地址。 |
|PushURLListDetail |[PushURLListDetail](https://docs.byteplus.com/en/docs/24/107368#pushurllistdetail) 陣列 |`-` |RTMP 推流地址詳細資訊。 |
|TsOverSrtURLList |String 陣列 |`["srt://push.example.com:9000?streamid=#!::h=push.example.com,r=live/example_stream,m=publish"]` |TS over SRT 推流地址。 |
|RtmpOverSrtURLList |String 陣列 |`["rtmp://push.example.com:1999/live/example_stream"]` |RTMP over SRT 推流地址。 |
|RtmURLList |String 陣列 |`["http://push.example.com/live/example_stream.sdp"]` |RTM 推流地址。 |
|AuthType |String |`TypeB` |用於產生推流地址的 URL 驗證類型。若值為空，表示目前網域未設定 URL 驗證。<br><br><br>* `TypeA`：Type A。<br><br>* `TypeB`：Type B。<br><br>* `TypeC`：Type C。<br><br>* `TypeCustom`：自訂類型。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">如需 Type A、B 或 C 的詳細資訊，請參見 <a href="https://docs.byteplus.com/en/docs/byteplus-media-live/docs-url-authentication">URL 驗證設定</a>。</div><br> |


<span id="pushurllistdetail"></span>
### PushURLListDetail


|**參數** |**資料型態** |**範例值** |**說明** |
|---|---|---|---|
|URL |String |`rtmp://live.push.example.com/live/example_stream` |RTMP 推流地址。 |
|DomainApp |字串 |`rtmp://push.example.com/live/` |OBS 推流地址。 |
|StreamSign |字串 |`example_stream` |OBS 串流金鑰。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://open.byteplusapi.com/?Action=GeneratePushURL&Version=2023-01-01
{
    "Domain": "push.example.com",
    "App": "live",
    "Stream": "example_stream",
    "ValidDuration": 5000,
    "ExpiredTime": "2023-08-19T16:07:25Z"
}
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GeneratePushURL",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "PushURLList": [
            "rtmp://push.example.com/live/example_stream"
        ],
        "PushURLListDetail": [
            {
                "URL": "rtmp://live.push.example.com/live/example_stream",
                "DomainApp": "rtmp://push.example.com/live/",
                "StreamSign": "example_stream"
            }
        ],
        "TsOverSrtURLList": [
            "srt://push.example.com:9000?streamid=#!::h=push.example.com,r=live/example_stream,m=publish"
        ],
        "RtmpOverSrtURLList": [
            "rtmp://push.example.com:1999/live/example_stream"
        ],
        "RtmURLList": [
            "http://push.example.com/live/example_stream.sdp"
        ],
        "AuthType": "TypeB"
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為與本操作相關的錯誤碼。其他錯誤碼請參見 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**描述** |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考[請求參數](https://docs.byteplus.com/en/docs/24/107368#request-parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料型別是否正確。 |
|400 |InvalidParam.Format |%s 格式錯誤 |參數格式不正確。請檢查錯誤訊息中指定參數是否包含非法字元或 URL 格式錯誤。 |
|400 |InvalidParam.OutOfRange |%s 應為 {[%s]} 之一%s 應介於 %d 與 %d 之間 |參數超出允許範圍。請檢查錯誤訊息中指定參數的值是否超出範圍。 |
|400 |InvalidParam.TimeLogic |startTime 晚於 endTime 等。 |傳入的時間參數不符合時間邏輯。請檢查是否存在以下問題：開始時間晚於結束時間。過期時間早於目前時間。 |
|403 |RequestForbidden |*  |因當前帳號下無請求資源（資源包括網域名稱空間、網域名稱、App 名稱、配置與憑證），請求被拒絕。 |
|403 |RequestForbidden.AccountIDNotAllowed |此 AccountID 無權存取對應資源，請檢查請求參數 |因當前帳號下無請求資源（資源包括網域名稱空間、網域名稱、App 名稱、配置與憑證），請求被拒絕。 |
|403 |RequestForbidden.BillingStatus |該 AccountID 未開通計費狀態，請開通服務或儲值。 |尚未啟用視訊直播服務或帳號欠費，導致計費不可用。請檢查服務開通狀態及帳號欠費狀態。 |
|404 |ResourceNotFound |*  |未找到資源（包括網域名稱空間、網域名稱、App 名稱、配置與憑證）。建議重試。若仍返回錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.VhostOrDomain |發生與 vhost 或網域名稱相關的內部錯誤，請聯絡管理員。 |發生與網域名稱（`Domain`）相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
