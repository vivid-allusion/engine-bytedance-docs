---
title: "CreateWatermarkPreset"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createwatermarkpreset-2023-zh-TW"
---

調用 `CreateWatermarkPreset` API，為轉碼流或 ABR（自適應碼率）子流新增浮水印配置。

<span id="Requirements"></span>
## 需求


* 頻率限制：每個帳號每秒 1 次查詢。

* 前置條件：

   * 你已在欲新增浮水印配置的網域名稱空間下，為指定的 `AppName` 新增轉碼配置或 ABR 配置。如需更多資訊，請參見 [CreateTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/createtranscodepresetv2023) 或 [CreateTranscodePresetBatch](https://docs.byteplus.com/en/docs/byteplus-media-live/CreateTranscodePresetBatch-2023)。

   * 準備一張 JPG 或 PNG 圖片作為浮水印。圖片大小不得超過 2 MB，解析度不得超過 1080 × 1080 像素。PNG 圖片可包含透明度。

* 生效時間：新增、更新或刪除浮水印配置後，變更會於 3 至 5 分鐘內生效。生效後產生的轉碼流或 ABR 子流會使用最新的浮水印配置。生效前已產生的轉碼流或 ABR 子流不會自動套用更新。若變更前不存在轉碼流或 ABR 子流，請等待配置生效。若變更前已存在轉碼流或 ABR 子流且需使用更新後的配置，請於配置新增、更新或刪除後等待 3 至 5 分鐘，再重新推流。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=CreateWatermarkPreset&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了需帶入 API 專屬參數外，還必須帶入 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`CreateWatermarkPreset` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本號。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |網域名稱空間，即直播串流 URL 中網域名稱所屬的網域名稱空間。你可以調用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或前往 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面，查詢網域名稱所屬的網域名稱空間。 |
|App |String |是 |`live` |直播串流 URL 中的 `AppName` 欄位。可包含大寫與小寫字母（A \- Z, a \- z）、數字（0 \- 9）、底線（_）、連字號（\-）及句點（.）。長度需為 1 至 30 個字元。 |
|Stream |String |否 |`example_stream` |直播串流 URL 中的 `StreamName` 欄位。可包含大寫與小寫字母（A \- Z, a \- z）、數字（0 \- 9）、底線（_）、連字號（\-）及句點（.）。長度需為 1 至 100 個字元。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">此參數留空時，浮水印配置將套用於指定 <code>AppName</code> 下的所有轉碼流與 ABR 子流。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">若指定 <code>StreamName</code>，則浮水印配置僅套用於指定 <code>AppName</code> 下的指定 <code>StreamName</code>。</div><br> |
|Orientation |String |否 |`vertical` |浮水印影片的方向。有效值：<br><br><br>* `vertical`：直式。<br><br>* `horizontal`：橫式。 |
|圖片 |字串 |否 |`data:image/png;base64,iVBORw0KGg****mCC` |已編碼的浮水印圖片字串。圖片大小不得超過 2 MB，最小大小為 100 位元組，解析度不得超過 1080 × 1080 像素。圖片資料 URL 格式為：`data:[<mediatype>];[base64],<data>`。<br><br><br>* `mediatype`：圖片類型。支援 `png`、`jpg` 和 `jpeg` 格式。<br><br>* `data`：base64 編碼的圖片字串。 |
|PosX |浮點數 |否 |`0` |水平偏移，表示浮水印左邊緣與轉碼串流或 ABR 子串流圖片左邊緣的距離。採用相對比例。有效範圍：[0,1]。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">當 <code>WatermarkMode</code> 設為 <code>static</code> 時，此參數為必填。</div><br> |
|PosY |浮點數 |否 |`1.0` |垂直偏移，表示浮水印上邊緣與轉碼串流或 ABR 子串流圖片上邊緣的距離。採用相對比例。有效範圍：[0,1]。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">當 <code>WatermarkMode</code> 設為 <code>static</code> 時，此參數為必填。</div><br> |
|RelativeWidth |浮點數 |否 |`1.0` |浮水印寬度比例，即浮水印寬度與轉碼串流或 ABR 子串流圖片寬度的比例。有效範圍：[0,1]。浮水印高度會隨寬度等比例縮放。 |
|WatermarkMode |字串 |否 |`dynamic` |浮水印類型。預設值為 `static`。有效值：<br><br><br>* `static`：靜態浮水印。浮水印固定於指定位置。<br><br>* `dynamic`：動態浮水印。浮水印於播放過程中移動，可增加未授權螢幕錄製及濫用的難度。 |
|DynamicMode |字串 |否 |`dynamic_move_curve` |動態浮水印效果。有效值：<br><br><br>* `dynamic_move_curve`：動態曲線移動。浮水印持續移動，並於到達影片邊緣時改變方向。<br><br>* `dynamic_blink`：動態閃爍。浮水印會以指定頻率於影片中隨機新位置出現。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">當 <code>WatermarkMode</code> 設為 <code>dynamic</code> 時，此參數為必填。</div><br> |
|DynamicSpeedLevel |整數 |否 |`1` |動態速度。預設值為 `1`。有效值為 1 到 10 的整數，數值越大變化越快。<br><br><br>* 當 `DynamicMode` 設為 `dynamic_move_curve` 時，此速度控制浮水印的移動速度。<br><br>* 當 `DynamicMode` 設為 `dynamic_blink` 時，此速度控制浮水印位置變化的頻率。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">此參數僅於 <code>WatermarkMode</code> 設為 <code>dynamic</code> 時生效。</div><br> |
|TransSuffixs |字串 |否 |`_hd,_uhd` |適用於浮水印配置的轉碼串流或 ABR 子串流後綴。預設情況下，浮水印配置適用於目前 `AppName` 下所有轉碼串流或 ABR 子串流後綴。可指定 1\-20 個後綴，並以逗號（,）分隔。<br><br>可呼叫 [ListVhostTransCodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhosttranscodepreset_1) 並從回傳參數 `SuffixName` 取得轉碼串流或 ABR 子串流後綴。 |


<span id="Response parameters"></span>
## 回應參數

如需 API 專屬回應參數，請參見下表。更多細節請參考 [請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 章節。


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|ID |整數 |`1234567` |浮水印範本 ID。 |
|PresetName |字串 |`preset` |浮水印範本名稱。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```json
POST https://open.byteplusapi.com/?Action=CreateWatermarkPreset&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "App": "live",
    "Orientation": "vertical",
    "RelativeWidth": 0.185,
    "Picture": "data:image/png;base64,iVBORw0KGg****mCC",
    "WatermarkMode": "dynamic",
    "DynamicMode": "dynamic_move_curve",
    "DynamicSpeedLevel": 1,
    "TransSuffixs": "_hd,_uhd"
}
```


<span id="Sample response"></span>
### 回應範例

```json
{
    "ResponseMetadata": {
        "Action": "CreateWatermarkPreset",
        "Region": "ap-singapore-1",
        "RequestId": "20230604110420****100232280022D31",
        "Service": "live",
        "Version": "2023-01-01"
    },
    "Result": {
        "ID": 1234567,
        "PresetName": "preset"
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為本操作相關的錯誤碼。其他錯誤碼請參見 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**說明** |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍回傳錯誤碼，請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考[請求參數](https://docs.byteplus.com/en/docs/24/107318#request-parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料型別是否正確。 |
|400 |InvalidParam.Empty |%s 為必填項 |缺少參數。請檢查錯誤訊息中指定的參數是否已傳入。 |
|403 |RequestForbidden |*  |因目前帳戶下無請求資源（資源包括網域名稱空間、網域名稱、應用名稱、配置與憑證），請求被拒絕。 |
|403 |RequestForbidden.AccountIDNotAllowed |此 AccountID 無權存取對應資源，請檢查請求參數 |因目前帳戶下無請求資源（資源包括網域名稱空間、網域名稱、應用名稱、配置與憑證），請求被拒絕。 |
|403 |RequestForbidden.BillingStatus |此 AccountID 的計費狀態不可用，請啟用服務或儲值。 |尚未啟用視訊直播服務或帳戶欠費，導致帳單不可用。請檢查服務啟用狀態及帳戶欠費狀態。 |
|404 |ResourceNotFound |*  |未找到資源（包括網域名稱空間、網域名稱、應用名稱、配置與憑證）。建議重新嘗試。若仍返回錯誤碼，請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.Preset |發生與預設相關的內部錯誤，請聯絡管理員。 |發生與預設相關的內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
