---
title: "ListVhostWatermarkPreset"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostwatermarkpreset-2023-zh-TW"
---

呼叫 `ListVhostWatermarkPreset` API，以查詢特定網域名稱空間的所有浮水印配置。

<span id="Requirements"></span>
## 需求

頻率限制：每個帳戶每分鐘最多 5 次查詢。

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=ListVhostWatermarkPreset&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了 API 專屬參數外，還必須帶上 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`ListVhostWatermarkPreset` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |網域名稱空間，即直播串流 URL 中網域名稱所屬的網域名稱空間。你可以呼叫 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或前往 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面，取得網域名稱所屬的網域名稱空間。 |


<span id="Response parameters"></span>
## 回應參數

如需 API 專屬回應參數，請參見下表。更多細節請參考 [請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)章節。


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|WatermarkPresetList |[WatermarkPresetList](https://docs.byteplus.com/en/docs/24/107452#watermarkpresetlist) 陣列 |`-` |可正常使用的浮水印配置清單。 |
|WatermarkErrMsgList |[WatermarkErrMsgList](https://docs.byteplus.com/en/docs/24/107452#watermarkerrmsglist) 陣列 |`-` |無法正常使用的浮水印配置清單，例如因浮水印圖片獲取失敗而無法使用的配置。返回無法使用的浮水印配置資訊及其不可用原因。 |
|StaticsMsg |String |`successfully get all 1 watermark presets of current vhost` |統計訊息，提供可用與不可用配置的數量。 |


<span id="watermarkpresetlist"></span>
### WatermarkPresetList


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|ID |Long |`1234567` |浮水印模板 ID。 |
|AccountID |String |`****1` |BytePlus 帳戶 ID。 |
|Vhost |String |`push.example.com` |網域名稱空間。 |
|App |String |`example_app` |`AppName`。 |
|Stream |String |`test-stream` |`StreamName`。 |
|Picture |String |`data:image/png;base64,iVBORw0KGg****mCC` |已編碼的浮水印圖片字串。 |
|PictureKey |String |`testtesttest.png` |浮水印圖片檔名。 |
|Orientation |String |`vertical` |浮水印影片的方向。有效值：<br><br><br>* `vertical`：直向。<br><br>* `horizontal`：橫向。 |
|PosX |Float |`1.0` |水平偏移，表示浮水印左邊緣與轉碼串流或 ABR（自適應碼率）子串流圖片左邊緣的距離。採用相對比例。有效範圍：[0,1]。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">此參數僅在 <code>WatermarkMode</code> 設為 <code>static</code> 時有值。</div><br> |
|PosY |Float |`1.0` |垂直偏移，表示浮水印上邊緣與轉碼串流或 ABR 子串流圖片上邊緣的距離。採用相對比例。有效範圍：[0,1]。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">此參數僅在 <code>WatermarkMode</code> 設為 <code>static</code> 時有值。</div><br> |
|RelativeWidth |Float |`1.0` |浮水印寬度的相對值，即浮水印寬度與轉碼串流或 ABR 子串流圖片寬度的比例。有效範圍：[0,1]。浮水印高度會隨寬度等比例縮放。 |
|WatermarkMode |String |`dynamic` |浮水印類型。有效值：<br><br><br>* `static`：靜態浮水印。浮水印固定於指定位置。<br><br>* `dynamic`：動態浮水印。浮水印會在播放期間移動，這增加了未經授權螢幕錄製及濫用的難度。 |
|DynamicMode |String |`dynamic_move_curve` |動態浮水印效果。有效值：<br><br><br>* `dynamic_move_curve`：動態曲線移動。浮水印會持續移動，並在到達影片邊緣時改變方向。<br><br>* `dynamic_blink`：動態閃爍。浮水印會以指定頻率出現在影片中的新隨機位置。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">僅當<code>WatermarkMode</code>設為<code>dynamic</code>時，此參數才有值。</div><br> |
|DynamicSpeedLevel |Integer |`1` |動態速度。有效值為 1 到 10 的整數。數值越大，變化越快。<br><br><br>* 當`DynamicMode`設為`dynamic_move_curve`時，此速度控制浮水印的移動速度。<br><br>* 當`DynamicMode`設為`dynamic_blink`時，此速度控制浮水印變換位置的頻率。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">僅當<code>WatermarkMode</code>設為<code>dynamic</code>時，此參數才有值。</div><br> |
|TransSuffixs |String |`_hd,_uhd` |浮水印配置所適用的轉碼串流或 ABR 子串流字尾。字尾以逗號（,）分隔。 |


<span id="watermarkerrmsglist"></span>
### WatermarkErrMsgList


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|AccountID |String |`****1` |BytePlus 帳戶 ID。 |
|Vhost |String |`push.example.com` |網域名稱空間。 |
|App |String |`example_app` |`AppName`。 |
|ErrMsg |String |`[ListVhostWatermarkPreset] 從 tos 取得圖片失敗，app: testApp，錯誤：內部錯誤` |浮水印配置無法正常使用的原因。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://open.byteplusapi.com/?Action=ListVhostWatermarkPreset&Version=2023-01-01
{
    "Vhost": "push.example.com"
}
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "Action": "ListVhostWatermarkPreset",
        "Region": "ap-singapore-1",
        "RequestId": "20230604110420****100232280022D31",
        "Service": "live",
        "Version": "2023-01-01"
    },
    "Result": {
        "StaticsMsg": "successfully get all 1 watermark presets of current vhost",
        "WatermarkErrMsgList": [
            {
                "AccountID": "****1",
                "App": "example_app",
                "ErrMsg": "[ListVhostWatermarkPreset] fail to get picture from tos, app: testApp, err: internal error",
                "Vhost": "push.example.com"
            }
        ],
        "WatermarkPresetList": [
            {
                "AccountID": "****1",
                "App": "example_app",
                "ID": 1****67,
                "Orientation": "vertical",
                "Picture": "data:image/png;base64,iVBORw0KGg****mCC",
                "PictureKey": "testtesttest.png",
                "RelativeWidth": 1.0,
                "Vhost": "push.example.com",
                "Stream": "test-stream",
                "WatermarkMode": "dynamic",
                "DynamicMode": "dynamic_move_curve",
                "DynamicSpeedLevel": 1,
                "TransSuffixs": "_hd,_uhd"
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
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回錯誤碼，請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考[請求參數](https://docs.byteplus.com/en/docs/24/107452#request-parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料型別是否正確。 |
|403 |RequestForbidden |*  |因目前帳戶下無請求資源（資源包括網域名稱空間、網域名稱、App 名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.AccountIDNotAllowed |此 AccountID 無權存取對應資源，請檢查請求參數 |因目前帳戶下無請求資源（資源包括網域名稱空間、網域名稱、App 名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.BillingStatus |AccountID 未啟用計費狀態，請開通服務或儲值。 |尚未啟用影片直播服務或帳戶欠費，導致帳單不可用。請檢查服務開通狀態及帳戶欠費狀態。 |
|404 |ResourceNotFound |*  |未找到資源（包括網域名稱空間、網域名稱、App 名稱、配置及憑證）。建議重試。若仍返回錯誤碼，請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|404 |ResourceNotFound.PresetNotExist |未找到預設配置 |未找到配置。請檢查傳入的配置是否與已建立的配置一致。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.Preset |發生與預設配置相關的內部錯誤，請聯絡管理員。 |發生與預設配置相關的內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
