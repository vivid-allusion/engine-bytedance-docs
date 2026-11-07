---
title: "UpdatePullToPushTask"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatepulltopushtask-2023-zh-TW"
---

呼叫 `UpdatePullToPushTask` API 以更新中繼任務的資訊。

<span id="Requirements"></span>
## 需求

頻率限制：每個帳戶每秒 1 次查詢。

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=UpdatePullToPushTask&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 呼叫時，除了 API 專屬參數外，還必須包含 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型態** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`UpdatePullToPushTask` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型態** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|TaskId |String |是 |`8fde6aa0281*********59a6e242365` |任務 ID。可呼叫 [ListPullToPushTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listpulltopushtask-2023) API 取得任務 ID。 |
|Title |String |否 |`task001` |中繼任務名稱由 1 到 20 個中文字、大小寫字母及數字組成。預設為空，表示不修改任務名稱。 |
|StartTime |Integer |是 |`1640891476` |中繼任務的開始時間，單位為秒。UNIX 時間戳。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">中繼任務最長持續時間為 7 天。</div><br> |
|EndTime |Integer |是 |`1640891976` |中繼任務的結束時間，單位為秒。UNIX 時間戳。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">中繼任務最長持續時間為 7 天。</div><br> |
|CallbackURL |String |否 |`http://example.mtime.cn/live/example/callbackapi` |用於接收中繼任務事件的回調地址。最大長度：512 字元。 |
|Type |Integer |是 |`0` |串流來源類型。有效值包括：<br><br><br>* `0`: 串流內容從直播來源拉取。<br><br>* `1`: 串流內容從點播影片拉取。 |
|CycleMode |Integer |否 |`-1` |當 `Type` 設為 `1` 時，可設定點播影片的循環播放模式。值及含義如下。<br><br><br>* `-1`: 無限列表循環<br><br>* 大於 0 的整數表示循環播放次數。 |
|DstAddr |String |否 |`rtmp://example.mtime.cn/Video/2022/02/04/mp4/190204084208765161.mp4` |推流地址。 |
|Domain |String |否 |`push.example.com` |推流用的網域名稱。當推流地址（DstAddr）為空時必須傳入，否則此參數無效。 |
|App |String |否 |`live` |Appname 欄位推流。當推流地址（DstAddr）為空時必須傳入，否則此參數無效。 |
|Stream |String |否 |`stream-123` |StreamName 欄位推流。當推流地址（DstAddr）為空時必須傳入，否則此參數無效。 |
|SrcAddr |String |否 |`http://example.cn/Video/2003/02/04/mp4/190204084208765161.mp4` |當 `Type` 設為 `0` 時，必須設定直播影片的拉流地址。最大長度：1,000 字元。 |
|SrcAddrS |Array of String |否 |`["http://example.cn/Video/2003/02/04/mp4/190204084208765161.mp4"]` |當 `Type` 設為 `1` 時，必須設定點播影片列表。 |
|水印 |[Watermark](https://docs.byteplus.com/en/docs/24/107425#watermark) 物件 |否 |`-` |為中繼影片新增的水印配置資訊。 |
|GroupName |String |否 | |任務所屬的群組名稱。可呼叫 [ListPullToPushGroup](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listpulltopushgroup-2023) API 取得群組名稱。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">使用主帳號呼叫時，該欄位非必填，預設會加入<code>default</code>群組。當<code>default</code>群組不存在時，系統會自動建立並綁定至<code>default</code>專案。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">使用子帳號呼叫時，該欄位為必填。</div><br> |


<span id="watermark"></span>
### 水印


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|圖片 |字串 |是 |`data:image/png;base64,iVBORw0KGg****mCC` |浮水印圖片的資料 URL。允許的圖片檔案大小範圍為 100 B 至 2 MB。最大解析度：1080×1080 像素。資料 URL 格式：`data:[<mediatype>];[base64],<data>`，例如`data:png;base64,iVBORw0KGg****mCC`。<br><br><br>* `mediatype`：圖片格式，包括`png`、`jpg`和`jpeg`。<br><br>* `data`：圖片的 Base64 字串。 |
|RelativePosX |浮點數 |是 |`0.1` |水平偏移，指浮水印左邊與轉碼後影片左邊的距離除以影片寬度的比例。有效範圍：0–1。 |
|RelativePosY |浮點數 |是 |`0.1` |垂直偏移，指浮水印上邊與轉碼後影片上邊的距離除以影片高度的比例。有效範圍：0–1。 |
|Ratio |浮點數 |是 |`0.1` |浮水印寬度與轉碼後影片寬度的比例。有效範圍：0–1。浮水印高度會自動依寬度調整。 |


<span id="Response parameters"></span>
## 回應參數

此 API 僅在回應中返回 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://open.byteplusapi.com/?Action=UpdatePullToPushTask&Version=2023-01-01
{
    "Type": 0,
    "DstAddr": "rtmp://example.mtime.cn/Video/2022/02/04/mp4/190204084208765161.mp4",
    "EndTime": 1640891476,
    "SrcAddr": "http://example.mtime.cn/Video/2003/02/04/mp4/190204084208765161.mp4",
    "TaskId": "8fde6aa0281d9f6e15e6059a6e242365",
    "StartTime": 1640841476,
    "Title": "suexample007",
    "CallbackURL": "http://example.mtime.cn/live/example/callbackapi"
}
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "202112311522300102252431180946DD57",
        "Action": "UpdatePullToPushTask",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為與目前操作相關的錯誤碼。其他錯誤碼請參見 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**說明** |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回錯誤碼，請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考[請求參數](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatepulltopushtask-2023#request-parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料型別是否正確。 |
|400 |InvalidParam.Format |%s 格式錯誤 |參數格式不正確。請檢查錯誤訊息中指定的參數是否包含非法字元或 URL 格式錯誤。 |
|400 |InvalidParam.OutOfRange |%s 應為 {[%s]} 之一%s 應介於 %d 與 %d 之間 |參數超出允許範圍。請檢查錯誤訊息中指定的參數值是否超出範圍。 |
|403 |RequestForbidden |*  |因目前帳號下無請求資源（資源包括網域命名空間、網域名稱、應用名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.AccountIDNotAllow |此 AccountID 無權存取對應資源，請檢查請求參數 |因目前帳號下無請求資源（資源包括網域命名空間、網域名稱、應用名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.BillingStatus |AccountID 未開通計費狀態，請啟用服務或儲值。 |尚未啟用視訊直播服務或帳號欠費，導致帳單不可用。請檢查服務啟用狀態及帳號欠費狀態。 |
|404 |ResourceNotFound |*  |未找到資源（包括網域命名空間、網域名稱、應用名稱、配置及憑證）。建議重試。如果仍然返回錯誤代碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|429 |RequestLimitExceeded |*  |請求建立的資源（包括網域名稱空間、網域名稱、應用名稱、配置、憑證）超過限制。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
