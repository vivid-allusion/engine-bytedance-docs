---
title: "CreatePullToPushTask"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createpulltopushtask-2023-zh-TW"
---

呼叫 `CreatePullToPushTask` API，以建立中繼任務，從直播來源或隨選影片拉取內容。

<span id="Requirements"></span>
## 需求


* 計費：有關中繼價格，請參閱 [Relay](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-relay-1)。

* 頻率限制：每個帳戶每秒 1 次查詢。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=CreatePullToPushTask&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了 API 專屬參數外，還必須帶上 [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型態** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`CreatePullToPushTask` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型態** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|GroupName |String |否 |`default` |任務所屬的群組名稱。你可以呼叫 [ListPullToPushGroup](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listpulltopushgroup-2023) API 取得群組名稱。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">以主帳戶呼叫時，此欄位為選填。預設為 <code>default</code> 群組。若 <code>default</code> 群組不存在，將自動建立並綁定至 <code>default</code> 專案。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">以子帳戶呼叫時，此欄位為必填。</div><br> |
|Title |String |否 |`task001` |中繼任務名稱。可包含中文、英文及數字。最大長度：20 字元。 |
|StartTime |Integer |是 |`1640891476` |中繼任務的開始時間，單位為秒。UNIX 時間戳。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">中繼任務最長持續時間為 7 天。</div><br> |
|EndTime |Integer |是 |`1640841476` |中繼任務的結束時間，單位為秒。UNIX 時間戳。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">中繼任務最長持續時間為 7 天。</div><br> |
|CallbackURL |String |否 |`http://example.mtime.cn/live/example/callbackapi` |用於接收中繼任務事件的回調地址。最大長度：512 字元。 |
|Type |Integer |是 |`0` |串流來源類型。有效值包括：<br><br><br>* `0`：串流內容從直播來源拉取。<br><br>* `1`：串流內容從隨選影片拉取。 |
|CycleMode |Integer |否 |`-1` |當 `Type` 設為 `1` 時，可設定隨選影片的循環播放模式。值及含義如下。<br><br><br>* `-1`：無限列表循環<br><br>* 大於 0 的整數表示循環播放次數。 |
|DstAddr |String |否 |`rtmp://example.mtime.cn/Video/2022/02/04/mp4/190204084208765161.mp4` |推流地址。 |
|Domain |String |否 |`example.mtime.cn` |推流用的網域名稱。當推流地址（DstAddr）為空時必須傳入，否則此參數無效。 |
|App |String |否 |`live` |直播串流 URL 中的 AppName 欄位。當推流地址（DstAddr）為空時必須傳入，否則此參數無效。 |
|Stream |String |否 |`stream-123` |直播串流 URL 中的 StreamName 欄位。當推流地址（DstAddr）為空時必須傳入，否則此參數無效。 |
|SrcAddr |String |否 |`http://example.cn/Video/2003/02/04/mp4/190204084208765161.mp4` |當 `Type` 設為 `0` 時，必須設定直播影片的拉流地址。最大長度：1,000 字元。 |
|SrcAddrS |字串陣列 |否 |`["https://pull.example.com/live/stream-123"]` |當你將 `Type` 設為 `1` 時，必須設定點播影片清單。 |
|Watermark |[Watermark](https://docs.byteplus.com/en/docs/24/107373#watermark) 物件 |否 |`-` |為轉播影片新增的浮水印配置資訊。 |
|PullRequestHeaders |[PullRequestHeaders](https://docs.byteplus.com/en/docs/24/107373#pullrequestheaders) 物件 |否 |`-` |在拉流請求中包含的 HTTP 請求標頭。若直播源或點播源會驗證拉流請求中的 Referer 或 User\-Agent 標頭，可使用此參數配置所需標頭。 |


<span id="watermark"></span>
### Watermark


|**參數** |**資料型別** |**必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Picture |字串 |是 |`data:image/png;base64,iVBORw0KGg****mCC` |浮水印圖片的資料 URL。允許的圖片檔案大小範圍為 100 B 至 2 MB。最大解析度：1080×1080 像素。資料 URL 格式：`data:[<mediatype>];[base64],<data>`，例如 `data:png;base64,iVBORw0KGg****mCC`。<br><br><br>* `mediatype`：圖片格式，包括 `png`、`jpg` 和 `jpeg`。<br><br>* `data`：圖片的 Base64 字串。 |
|RelativePosX |浮點數 |是 |`0.1` |水平偏移量，即浮水印左邊緣與轉碼影片左邊緣之間距離與影片寬度的比例。有效範圍：0–1。 |
|RelativePosY |浮點數 |是 |`0.1` |垂直偏移量，即浮水印上邊緣與轉碼影片上邊緣之間距離與影片高度的比例。有效範圍：0–1。 |
|Ratio |浮點數 |是 |`0.1` |浮水印寬度與轉碼影片寬度的比例。有效範圍：0–1。浮水印高度會自動依寬度調整。 |


<span id="pullrequestheaders"></span>
### PullRequestHeaders


|**參數** |**資料型別** |**必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Referer |字串 |否 |`http://test.com` |在拉流請求中包含的 Referer 標頭。若直播源或點播源會驗證請求來源，請指定所需的 Referer。 |
|UserAgent |字串 |否 |`example-agent` |在拉流請求中包含的 User\-Agent 標頭。若直播源或點播源要求拉流請求攜帶特定 User\-Agent，請指定所需的 User\-Agent。 |


<span id="Response parameters"></span>
## 回應參數

如需唯一的 API 專屬回應參數，請參閱下表。更多詳細資訊，請參閱 [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 章節。


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|TaskId |字串 |`8fde6aa0281d9f6e15e6059a6e242365` |任務的唯一識別碼。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://open.byteplusapi.com/?Action=CreatePullToPushTask&Version=2023-01-01
{
    "Title": "task001",
    "StartTime": 1640891476,
    "EndTime": 1640841476,
    "CallbackURL": "http://example.com/live/callback",
    "Type": 0,
    "DstAddr": "rtmp://push.example.com/live/example_stream",
    "SrcAddr": "http://pull.example.com/live/example_stream.mp4",
    "PullRequestHeaders": {
        "Referer": "http://test.com",
        "UserAgent": "user-agent"
    }
}
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "202112311457430101742350380352BCB2",
        "Action": "CreatePullToPushTask",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "TaskId": "8fde6aa0281d*******9a6e242365"
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為與目前操作相關的錯誤碼。其他錯誤碼請參閱 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**說明** |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回錯誤碼，請 [聯絡客服](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考 [請求參數](https://docs.byteplus.com/en/docs/24/107373#request-parameters) 說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料型別是否正確。 |
|400 |InvalidParam.Format |%s 格式錯誤 |參數格式不正確。請檢查錯誤訊息中指定參數是否有非法字元或 URL 格式錯誤。 |
|400 |InvalidParam.OutOfRange |%s 應為 {[%s]} 之一%s 應介於 %d 與 %d 之間 |參數超出允許範圍。請檢查錯誤訊息中指定參數的值是否超出範圍。 |
|403 |RequestForbidden |*  |因目前帳戶下無請求資源（資源包括網域名稱空間、網域名稱、App 名稱、配置與憑證），請求被拒絕。 |
|403 |RequestForbidden.AccountIDNotAllow |此 AccountID 無權存取對應的資源，請檢查請求參數 |由於當前帳戶下沒有請求的資源（資源包括網域名稱空間、網域名稱、應用名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.BillingStatus |該 AccountID 無法取得計費狀態，請啟用服務或儲值。 |尚未啟用視訊直播服務或帳戶欠費，導致無法取得帳單。請檢查服務啟用狀態及帳戶欠費狀態。 |
|404 |ResourceNotFound |*  |未找到資源（包括網域名稱空間、網域名稱、應用名稱、配置及憑證）。建議重試。若仍返回錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|429 |RequestLimitExceeded |*  |請求建立的資源（包括網域名稱空間、網域名稱、應用名稱、配置、憑證）超出限制。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
