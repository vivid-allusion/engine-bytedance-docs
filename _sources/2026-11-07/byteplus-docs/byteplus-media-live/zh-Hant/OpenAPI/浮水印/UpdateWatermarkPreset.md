---
title: "UpdateWatermarkPreset"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatewatermarkpreset-2023-zh-TW"
---

調用 `UpdateWatermarkPreset` API 以更新現有的浮水印配置。

<span id="Usage scenario"></span>
## 使用場景

請根據以下規則傳遞可選參數：


* 若要更新動態浮水印配置，或將靜態浮水印更新為動態浮水印，必須傳遞 `WatermarkMode`、`DynamicMode` 和 `DynamicSpeedLevel`。

* 若要將動態浮水印更新為靜態浮水印，必須傳遞 `PosX` 和 `PosY`。

* 僅在需要更新相關配置時，才傳遞其他可選參數。若未傳遞，則使用原有的浮水印配置值。


<span id="Requirements"></span>
## 要求


* 頻率限制：每個帳號每秒 1 次查詢。

* 生效時間：新增、更新或刪除浮水印配置後，變更會在 3 至 5 分鐘內生效。變更生效後產生的轉碼串流或 ABR（自適應碼率）子串流將使用最新的浮水印配置。變更生效前已產生的轉碼串流或 ABR 子串流不會自動套用更新。若變更前不存在轉碼串流或 ABR 子串流，請等待配置生效。若變更前已存在轉碼串流或 ABR 子串流且需要使用更新後的配置，請在配置新增、更新或刪除後等待 3 至 5 分鐘，然後重新推流。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=UpdateWatermarkPreset&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 調用時，除 API 專屬參數外，還必須帶上 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`UpdateWatermarkPreset` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。當前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |網域名稱空間。可調用 [ListVhostWatermarkPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostwatermarkpreset-2023) API 來獲取配置的網域名稱空間，作為 `Vhost` 參數的值。 |
|App |String |是 |`live` |直播串流 URL 中的 `AppName` 欄位。可調用 [ListVhostWatermarkPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostwatermarkpreset-2023) API 來獲取配置的 `AppName`，作為 `App` 參數的值。 |
|Stream |String |否 |`example_stream` |直播串流 URL 中的 `StreamName` 欄位。可調用 [ListVhostWatermarkPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostwatermarkpreset-2023) API 來獲取配置的 `StreamName`，作為 `Stream` 參數的值。 |
|Orientation |String |否 |`vertical` |浮水印影片的方向。有效值：<br><br><br>* `vertical`：直向。<br><br>* `horizontal`：橫向。 |
|Picture |String |否 |`data:image/png;base64,iVBORw0KGg****mCC` |已編碼的浮水印圖片字串。圖片大小不得超過 2 MB，最小為 100 bytes，解析度不得超過 1080 × 1080 px。PNG 圖片可包含透明度。圖片資料 URL 格式為：`data:[<mediatype>];[base64],<data>`。<br><br><br>* `mediatype`：圖片類型。支援 `png`、`jpg` 及 `jpeg` 格式。<br><br>* `data`：Base64 編碼的圖片字串。<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">若未更新浮水印圖片，更新配置時請勿傳遞此參數。否則浮水印可能無法顯示。</div><br> |
|PosX |Float |否 |`1.0` |水平偏移，表示浮水印左邊緣與轉碼串流或 ABR 子串流影像左邊緣之間的距離。使用相對比例。有效範圍：[0,1]。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">此參數僅對靜態浮水印生效。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">當您將動態浮水印更新為靜態浮水印時，此參數為必填。</div><br> |
|PosY |Float |否 |`1.0` |垂直偏移，表示浮水印頂部邊緣與轉碼串流或 ABR 子串流影像頂部邊緣之間的距離。使用相對比例。有效範圍：[0,1]。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">此參數僅對靜態浮水印生效。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">當您將動態浮水印更新為靜態浮水印時，此參數為必填。</div><br> |
|RelativeWidth |Float |否 |`1.0` |浮水印的相對寬度，即浮水印寬度與轉碼串流或 ABR 子串流影像寬度的比例。有效範圍：[0,1]。浮水印高度會隨寬度等比例縮放。 |
|WatermarkMode |String |否 |`dynamic` |浮水印類型。有效值：<br><br><br>* `static`：靜態浮水印。浮水印會固定在指定位置。<br><br>* `dynamic`：動態浮水印。浮水印會在播放過程中移動，增加未經授權螢幕錄製與濫用的難度。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">當您更新動態浮水印配置或將靜態浮水印更新為動態浮水印時，此參數為必填。</div><br> |
|DynamicMode |String |否 |`dynamic_move_curve` |動態浮水印效果。有效值：<br><br><br>* `dynamic_move_curve`：動態曲線移動。浮水印會持續移動，並在到達影片邊緣時改變方向。<br><br>* `dynamic_blink`：動態閃爍。浮水印會以指定頻率在影片中隨機出現於新位置。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">當您更新動態浮水印配置或將靜態浮水印更新為動態浮水印時，此參數為必填。</div><br> |
|DynamicSpeedLevel |Integer |否 |`1` |動態速度。有效值為 1 到 10 的整數。數值越大，變化越快。<br><br><br>* 當 `DynamicMode` 設為 `dynamic_move_curve` 時，此速度控制浮水印的移動速度。<br><br>* 當 `DynamicMode` 設為 `dynamic_blink` 時，此速度控制浮水印變換位置的頻率。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">當您更新動態浮水印配置或將靜態浮水印更新為動態浮水印時，此參數為必填。</div><br> |
|TransSuffixs |String |是 |`_hd,_uhd` |浮水印配置所適用的轉碼串流或 ABR 子串流字尾。可指定 1\-20 個字尾，以逗號（,）分隔。<br><br>您可呼叫 [ListVhostTransCodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhosttranscodepreset_1) 並從回傳參數 `SuffixName` 取得轉碼串流或 ABR 子串流字尾。 |


<span id="Response parameters"></span>
## 回應參數

此 API 僅在回應中返回 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```json
POST https://open.byteplusapi.com/?Action=UpdateWatermarkPreset&Version=2023-01-01
{
    "App": "live",
    "Vhost": "push.example.com",
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
        "RequestId": "201806041104200100100232280022D30",
        "Action": "UpdateWatermarkPreset",
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
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍回傳錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考[請求參數](https://docs.byteplus.com/en/docs/24/107446#request-parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料型態是否正確。 |
|400 |InvalidParam.Length |%s 不應長於 %d |參數長度不正確。請檢查錯誤訊息中指定參數的長度是否超出限制。 |
|403 |RequestForbidden |*  |請求被拒絕，因為當前帳戶下沒有請求的資源（資源包括網域名稱空間、網域名稱、應用名稱、配置和憑證）。 |
|403 |RequestForbidden.AccountIDNotAllowed |此 AccountID 無權存取對應資源，請檢查請求參數。 |請求被拒絕，因為當前帳戶下沒有請求的資源（資源包括網域名稱空間、網域名稱、應用名稱、配置和憑證）。 |
|403 |RequestForbidden.BillingStatus |該 AccountID 尚未開通計費狀態，請啟用服務或儲值。 |尚未啟用視訊直播服務或帳戶已欠費，導致無法取得帳單。請檢查服務啟用狀態及帳戶欠費狀態。 |
|404 |ResourceNotFound |*  |未找到資源（包括網域名稱空間、網域名稱、應用名稱、配置和憑證）。建議重試。若仍返回錯誤碼，請[聯繫支援](https://console.byteplus.com/workorder/create)。 |
|404 |ResourceNotFound.PresetNotExist |未找到預設配置 |未找到該配置。請檢查傳入的配置是否與已建立的配置一致。 |
|500 |InternalError |發生內部錯誤，請聯繫管理員。 |發生內部錯誤。請[聯繫支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.Preset |發生與預設配置相關的內部錯誤，請聯繫管理員。 |發生與預設配置相關的內部錯誤。請[聯繫支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯繫管理員。 |發生內部錯誤。請[聯繫支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯繫管理員。 |發生內部錯誤。請[聯繫支援](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯繫管理員。 |內部服務逾時。請[聯繫支援](https://console.byteplus.com/workorder/create)。 |
