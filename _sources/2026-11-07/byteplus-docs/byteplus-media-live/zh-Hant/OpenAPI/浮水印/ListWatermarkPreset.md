---
title: "ListWatermarkPreset"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listwatermarkpreset-2023-zh-TW"
---

呼叫 `ListWatermarkPreset` API 以查詢浮水印配置的相關資訊。

<span id="Requirements"></span>
## 需求

頻率限制：每個帳戶每分鐘最多查詢 5 次。

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=ListWatermarkPreset&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了需帶入 API 專屬參數外，還必須帶入 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`ListWatermarkPreset` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |網域名稱空間。可呼叫 [ListVhostWatermarkPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostwatermarkpreset-2023) API，並以 `Vhost` 參數值取得該配置的網域名稱空間。 |
|App |String |是 |`live` |直播串流 URL 中的 `AppName` 欄位。可呼叫 [ListVhostWatermarkPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostwatermarkpreset-2023) API，並以 `App` 參數值取得該配置的 `AppName`。 |
|Stream |String |否 |`example_stream` |直播串流 URL 中的 `StreamName` 欄位。可呼叫 [ListVhostWatermarkPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostwatermarkpreset-2023) API，並以 `Stream` 參數值取得該配置的 `StreamName`。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">此參數留空時，會查詢指定 <code>AppName</code> 下所有串流的配置。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">指定串流名稱時，會查詢該串流在指定 <code>AppName</code> 下的配置。</div><br> |


<span id="Response parameters"></span>
## 回應參數

如需唯一的 API 專屬回應參數，請參閱下表。更多細節請參考 [請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)章節。


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Preset |[Preset](https://docs.byteplus.com/en/docs/24/107343#preset) 物件 |`-` |浮水印配置。 |


<span id="preset"></span>
### Preset


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|ID |Integer |`1234567` |浮水印範本 ID。 |
|AccountID |String |`****1` |BytePlus 帳戶 ID。 |
|Vhost |String |`push.example.com` |網域名稱空間。 |
|App |String |`example_app` |`AppName`。 |
|Stream |String |`test-stream` |`StreamName`。 |
|Picture |String |`data:image/png;base64,iVBORw0KGg****mCC` |浮水印圖片編碼字串。 |
|PictureKey |String |`testtesttest.png` |浮水印圖片檔案名稱。 |
|Orientation |String |`vertical` |浮水印影片的方向。有效值：<br><br><br>* `vertical`：直向。<br><br>* `horizontal`：橫向。 |
|PosX |Float |`1.0` |水平偏移，表示浮水印左邊與轉碼串流或 ABR（自適應碼率）子串流影像左邊的距離。採用相對比例。有效範圍：[0,1]。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">此參數僅於 <code>WatermarkMode</code> 設為 <code>static</code> 時有值。</div><br> |
|PosY |Float |`1.0` |垂直偏移，表示浮水印上邊與轉碼串流或 ABR 子串流影像上邊的距離。採用相對比例。有效範圍：[0,1]。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">此參數僅於 <code>WatermarkMode</code> 設為 <code>static</code> 時有值。</div><br> |
|RelativeWidth |Float |`1.0` |浮水印相對寬度，即浮水印寬度與轉碼串流或 ABR 子串流影像寬度的比例。有效範圍：[0,1]。浮水印高度會隨寬度等比例縮放。 |
|WatermarkMode |String |`dynamic` |浮水印類型。有效值：<br><br><br>* `static`：靜態浮水印。浮水印會固定於指定位置。<br><br>* `dynamic`：動態浮水印。浮水印會在播放期間移動，這增加了未經授權螢幕錄製和濫用的難度。 |
|DynamicMode |String |`dynamic_move_curve` |動態浮水印效果。有效值：<br><br><br>* `dynamic_move_curve`：動態曲線移動。浮水印會持續移動，並在到達影片邊緣時改變方向。<br><br>* `dynamic_blink`：動態閃爍。浮水印會以指定頻率出現在影片中的新隨機位置。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">僅當<code>WatermarkMode</code>設為<code>dynamic</code>時，此參數才有值。</div><br> |
|TransSuffixs |String |`_hd,_uhd` |適用於浮水印配置的轉碼串流或 ABR 子串流字尾。字尾以逗號（,）分隔。 |
|DynamicSpeedLevel |Integer |`1` |動態速度。有效值為 1 至 10 的整數。數值越大，變化越快。<br><br><br>* 當`DynamicMode`設為`dynamic_move_curve`時，此速度控制浮水印的移動速度。<br><br>* 當`DynamicMode`設為`dynamic_blink`時，此速度控制浮水印變換位置的頻率。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">僅當<code>WatermarkMode</code>設為<code>dynamic</code>時，此參數才有值。</div><br> |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://open.byteplusapi.com/?Action=ListWatermarkPreset&Version=2023-01-01
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
        "Action": "ListWatermarkPreset",
        "Region": "ap-singapore-1",
        "Service": "live",
        "Version": "2023-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "Preset": {
            "App": "example_app",
            "Orientation": "vertical",
            "Picture": "data:image/png;base64,iVBORw0KGg****mCC",
            "RelativeWidth": 1.0,
            "AccountID": "****1",
            "PictureKey": "testtesttest.png",
            "ID": 1****67,
            "Vhost": "push.example.com",
            "Stream": "test-stream",
            "WatermarkMode": "dynamic",
            "DynamicMode": "dynamic_move_curve",
            "TransSuffixs": "_hd,_uhd",
            "DynamicSpeedLevel": 1
        }
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為與本操作相關的錯誤碼。其他錯誤碼請參閱 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**描述** |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考[請求參數](https://docs.byteplus.com/en/docs/24/107343#request-parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料型別是否正確。 |
|403 |RequestForbidden |*  |因當前帳號下無請求資源（資源包括網域命名空間、網域名稱、App 名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.AccountIDNotAllowed |此 AccountID 無權存取對應資源，請檢查請求參數 |因當前帳號下無請求資源（資源包括網域命名空間、網域名稱、App 名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.BillingStatus |該 AccountID 的計費狀態不可用，請開通服務或儲值。 |尚未啟用影片直播服務或帳號欠費，導致帳單不可用。請檢查服務開通狀態及帳號欠費狀態。 |
|404 |ResourceNotFound |*  |未找到資源（包括網域命名空間、網域名稱、App 名稱、配置及憑證）。建議重試。若仍返回錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|404 |ResourceNotFound.PresetNotExist |未找到預設配置 |未找到配置。請檢查傳入的配置是否與已建立的配置一致。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.Preset |發生與預設配置相關的內部錯誤，請聯絡管理員。 |發生與預設配置相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
