---
title: "ListCommonTransPresetDetail"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listcommontranspresetdetail-2023-zh-TW"
---

呼叫 `ListCommonTransPresetDetail` API 以查詢預設轉碼配置的詳細資訊。

<span id="Requirements"></span>
## 需求

速率限制：每個帳戶每秒最多 10 次查詢。

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=ListCommonTransPresetDetail&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了專屬參數外，還必須帶上 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**描述** |
|---|---|---|---|---|
|Action |String |是 |`ListCommonTransPresetDetail` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**描述** |
|---|---|---|---|---|
|PresetList |String 陣列 |否 |`["preser1","preset2"]` |轉碼模板列表。若未指定，將查詢所有預設轉碼模板。 |


<span id="Response parameters"></span>
## 回應參數

有關專屬於 API 的回應參數，請參見下表。更多細節請參考 [請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)章節。


|**參數** |**資料型別** |**範例值** |**描述** |
|---|---|---|---|
|NarrowBandHDPresetDetail |[PresetDetail](https://docs.byteplus.com/en/docs/24/107445#presetdetail) 陣列 |`-` |低碼率高清模板的詳細資訊。 |
|StandardPresetDetail |[PresetDetail](https://docs.byteplus.com/en/docs/24/107445#presetdetail) 陣列 |`-` |標準模板的詳細資訊。 |


<span id="presetdetail"></span>
### PresetDetail


|**參數** |**資料型別** |**範例值** |**描述** |
|---|---|---|---|
|SuffixName |String |`hd` |轉碼串流的後綴。 |
|VideoBitrate |Integer |`1000000` |視訊位元率。單位：Kbps。 |
|Vcodec |String |`h265` |視訊編碼格式。<br><br><br>* `h264`：H.264。<br><br>* `h265`：H.265。<br><br>* `copy`：不轉碼視訊串流。 |
|AudioBitrate |Integer |`30` |音訊位元率。單位：Kbps。 |
|Acodec |String |`aac` |音訊編碼格式。<br><br><br>* `aac`：AAC。<br><br>* `copy`：不轉碼音訊串流。<br><br>* `opus`：OPUS。 |
|FPS |Integer |`60` |視訊幀率。單位：fps。 |
|GOP |Integer |`2` |IDR 幀的最大間隔。單位：秒。 |
|Width |Integer |`100` |視訊寬度（像素 px）。當 Vcodec 設為 h264 或 h265 且 As 設為 0 時有效。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">視訊將依據 Width 與 Height 拉伸。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">當 Width 或 Height 任一設為 0 時，將保留原始視訊尺寸。</div><br> |
|Height |Integer |`50` |視訊高度（像素 px）。當 Vcodec 設為 h264 或 h265 且 As 設為 0 時有效。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">視訊將依據 Width 與 Height 拉伸。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">當 Width 或 Height 任一設為 0 時，將保留原始視訊尺寸。</div><br> |
|As |String |`1` |是否自動調整視訊尺寸。<br><br><br>* `0`：關閉自動調整，視訊將依據 `Width` 與 `Height` 拉伸。<br><br>* `1`：開啟自動調整，視訊將依據 `ShortSide` 或 `LongSide` 等比例縮放。 |
|ShortSide |Integer |`100` |視訊短邊（像素 px）。當 As 設為 1 時有效。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">若 LongSide 與 ShortSide 均設為 0，將保留原始視訊尺寸。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">若 LongSide 與 ShortSide 均設為非 0 值，視訊將依據 ShortSide 拉伸。</div><br> |
|LongSide |Integer |`200` |視訊長邊（像素 px）。當 As 設為 1 時有效。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">若 LongSide 與 ShortSide 均設為 0，將保留原始視訊尺寸。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">若 LongSide 與 ShortSide 均設為非 0 值，視訊將依據 ShortSide 拉伸。</div><br> |
|BFrames |整數 |`3` |兩個參考幀之間最多的 B 幀數。0 表示移除 B 幀。 |
|Roi |布林值 |`true` |是否以低碼率高清模式轉碼。<br><br><br>* `true`：低碼率高清模式。<br><br>* `false`：（預設）標準模式。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://open.byteplusapi.com/?Action=ListCommonTransPresetDetail&Version=2023-01-01
{
    "PresetList": [
        "preset1",
        "preset2"
    ]
}
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestID": "20220426203705010211197144119377C1",
        "Action": "ListCommonTransPresetDetail",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "cn-north-1"
    },
    "Result": {
        "StandardPresetDetail": [],
        "NarrowBandHDPresetDetail": []
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為與本操作相關的錯誤碼。其他錯誤碼請參見 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**描述** |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回錯誤碼，請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考[請求參數](https://docs.byteplus.com/en/docs/24/107445#request-parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料型態是否正確。 |
|400 |InvalidParam.OutOfRange |%s 應為 {[%s]} 之一%s 應介於 %d 與 %d 之間 |參數超出允許範圍。請檢查錯誤訊息中指定參數的值是否超出範圍。 |
|403 |RequestForbidden |*  |因目前帳戶下無請求資源（資源包括域名空間、域名、App 名稱、配置與憑證），請求被拒絕。 |
|403 |RequestForbidden.AccountIDNotAllow |此 AccountID 無權存取對應資源，請檢查請求參數 |因目前帳戶下無請求資源（資源包括域名空間、域名、App 名稱、配置與憑證），請求被拒絕。 |
|403 |RequestForbidden.BillingStatus |AccountID 的計費狀態不可用，請開通服務或充值。 |尚未開通視頻直播服務或帳戶欠費，導致帳單不可用。請檢查服務開通狀態及帳戶欠費狀態。 |
|404 |ResourceNotFound |*  |未找到資源（包括域名空間、域名、App 名稱、配置與憑證）。建議重試。若仍返回錯誤碼，請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.Preset |發生與預設相關的內部錯誤，請聯絡管理員。 |發生與服務或帳單相關的內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
