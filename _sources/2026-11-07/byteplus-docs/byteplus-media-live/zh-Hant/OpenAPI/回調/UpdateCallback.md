---
title: "UpdateCallback"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatecallback-2023-zh-TW"
---

呼叫 `UpdateCallback` API，以新增或更新串流推送、錄製及截圖事件的回調配置。

<span id="Requirements"></span>
## 需求

頻率限制：每個帳戶每秒最多 1 次查詢。

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=UpdateCallback&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 在呼叫時，除了 API 專屬參數外，還必須包含 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`UpdateCallback` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|MessageType |String |是 |`push` |要接收的回調訊息類型。值及其含義如下：<br><br><br>* `push`：當串流推送開始時觸發回調。<br><br>* `push_end`：當串流推送結束時觸發回調。<br><br>* `snapshot`：當發生截圖事件時觸發回調。<br><br>* `record`：當發生錄製事件時觸發回調。<br><br>* `audit_sanpshot`：當截圖審核完成時觸發回調。 |
|Vhost |String |否 |`push.example.com` |域名空間，即直播串流地址所屬的域名。可呼叫 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或前往 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面，獲取該域名所屬的域名空間。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">必須指定 <code>Vhost</code> 或 <code>Domain</code>，不可同時指定。</div><br> |
|Domain |String |否 |`push.example.com` |串流推送的域名。可呼叫 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或前往 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面，獲取域名。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">必須指定 <code>Vhost</code> 或 <code>Domain</code>，不可同時指定。</div><br> |
|App |String |否 |`example_app` |直播串流 URL 中的 AppName 欄位。可包含大寫字母（A\-Z）、小寫字母（a\-z）、數字（0\-9）、底線（_）、連字號（\-）及句點（.），長度為 1 至 30 字元。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">若指定 Domain，則不可指定 App。</div><br> |
|TranscodeCallback |Integer |否 |`0` |定義是否接收轉碼串流的回調。值及其含義如下：<br><br><br>* `0`：（預設）否。<br><br>* `1`：是。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">當 <code>MessageType</code> 為 <code>Push</code> 或 <code>Push_end</code> 時生效。</div><br> |
|CallbackDetailList |[CallbackDetailList](https://docs.byteplus.com/en/docs/24/107362#callbackdetaillist) 陣列 |是 |`-` |回調地址資訊列表。 |
|AuthEnable |Boolean |否 |`false` |是否啟用回調驗證。啟用驗證後，可透過回調訊息中的 `sign` 和 `t` 欄位，驗證收到的回調是否來自 BytePlus MediaLive。<br><br><br>* `false`：（預設）不啟用驗證。<br><br>* `true`：啟用驗證。 |
|AuthKeyPrimary |String |否 |`1622194197-0-0-5552*****e4e20387c6dc18afce****` |回調金鑰。若將 `AuthEnable` 設為 `true`，則必須指定 `AuthKeyPrimary`。可包含數字及字母。最大長度：32 字元。 |


<span id="callbackdetaillist"></span>
### CallbackDetailList


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|CallbackType |String |是 |`http` |所使用的回調地址類型。僅可設為 `http`，即同時支援 HTTP 與 HTTPS。 |
|URL |String |是 |`http://example.com/callback` |回調地址，必須為1至100個字元。 |


<span id="Response parameters"></span>
## 回應參數

此 API 僅在回應中返回 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://open.byteplusapi.com/?Action=UpdateCallback&Version=2023-01-01
{
    "Vhost": "push.live.example.com",
    "App": "example_app",
    "MessageType": "push",
    "TranscodeCallback": 0,
    "CallbackDetailList": [
        {
            "CallbackType": "http",
            "URL": "http://example.com/callback"
        }
    ]
}
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "UpdateCallback",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為與本操作相關的錯誤碼。其他錯誤碼請參見 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**描述** |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回錯誤碼，請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考[請求參數](https://docs.byteplus.com/en/docs/24/107362#request-parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料型態是否正確。 |
|400 |InvalidParam.Format |%s格式錯誤 |參數格式不正確。請檢查錯誤訊息中指定的參數是否有非法字元或URL格式錯誤。 |
|400 |InvalidParam.OutOfRange |%s應為{[%s]}之一%s應介於%d與%d之間 |參數超出允許範圍。請檢查錯誤訊息中指定參數的值是否超出範圍。 |
|400 |InvalidParam.DomainAndApp |domain與app不可同時存在 |不可同時傳入Domain與App。請修改輸入參數。 |
|400 |InvalidParam.Empty |%s為必填 |參數缺失。請檢查錯誤訊息中指定的參數是否已傳入。 |
|403 |RequestForbidden |*  |因目前帳號下無請求資源（資源包括域名空間、域名、App名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.AccountIDNotAllowed |此AccountID無權限存取對應資源，請檢查請求參數 |因目前帳號下無請求資源（資源包括域名空間、域名、App名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.BillingStatus |AccountID的計費狀態不可用，請開通服務或充值。 |尚未啟用視頻直播服務或帳號欠費，導致帳單不可用。請檢查服務開通狀態及帳號欠費狀態。 |
|404 |ResourceNotFound |*  |未找到資源（包括域名空間、域名、App名稱、配置及憑證）。建議重試。若仍返回錯誤碼，請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|404 |ResourceNotFound.VhostNotExist |未找到vhost |未找到域名空間（Vhost）。請檢查傳入的域名空間是否與實際使用的一致。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |發生與資料庫相關的內部錯誤，請聯絡管理員。 |發生與資料庫相關的內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
