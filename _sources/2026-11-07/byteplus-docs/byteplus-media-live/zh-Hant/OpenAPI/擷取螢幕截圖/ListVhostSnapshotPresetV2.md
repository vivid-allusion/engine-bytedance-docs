---
title: "ListVhostSnapshotPresetV2"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/listvhostsnapshotpresetv2-zh-TW"
---

獲取特定網域命名空間下的所有螢幕截圖配置資訊。

<span id="Requirements"></span>
## 需求

速率限制：每個帳號每秒 10 次請求。

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=ListVhostSnapshotPresetV2&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 必須同時帶上[通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)和 API 專屬參數。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**描述** |
|---|---|---|---|---|
|Action |String |是 |`ListVhostSnapshotPresetV2` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。當前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**描述** |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |網域命名空間，指直播流地址所屬的命名空間。可呼叫[ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023)或前往[BytePlus MediaLive 控制台](https://console.byteplus.com/live/main/domain/list)的**Domains**頁面，查詢直播流所用網域所屬的命名空間。 |
|Type |String |否 |`tos` |螢幕截圖檔案的儲存位置。預設情況下，不會根據儲存位置篩選螢幕截圖配置。目前僅可設為`tos`，表示將螢幕截圖儲存於 TOS。 |


<span id="Response parameters"></span>
## 回應參數

有關唯一的 API 專屬回應參數，請參見下表。更多詳情請參見[請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)章節。


|**參數** |**資料型別** |**範例值** |**描述** |
|---|---|---|---|
|PresetList |[PresetList](https://docs.byteplus.com/en/docs/24/107406#presetlist) 陣列 |`-` |螢幕截圖配置清單。 |


<span id="presetlist"></span>
### PresetList


|**參數** |**資料型別** |**範例值** |**描述** |
|---|---|---|---|
|Vhost |String |`push.example.com` |網域命名空間。 |
|App |String |`live` |應用名稱。 |
|SlicePresetV2 |[SlicePresetV2](https://docs.byteplus.com/en/docs/24/107406#slicepresetv2) 物件 |`-` |螢幕截圖配置的基本資訊。 |


<span id="slicepresetv2"></span>
### SlicePresetV2


|**參數** |**資料型別** |**範例值** |**描述** |
|---|---|---|---|
|SnapshotPresetConfig |[SnapshotPresetConfig](https://docs.byteplus.com/en/docs/24/107406#snapshotpresetconfig) 物件 |`-` |螢幕截圖配置的詳細資訊。 |
|Name |String |`preset-123` |螢幕截圖配置名稱。 |
|Status |Integer |`1` |螢幕截圖配置是否生效。有效值：<br><br><br>* `1`：生效。<br><br>* `0`：不生效。 |


<span id="snapshotpresetconfig"></span>
### SnapshotPresetConfig


|**參數** |**資料型別** |**範例值** |**描述** |
|---|---|---|---|
|JpegParam |[JpegParam](https://docs.byteplus.com/en/docs/24/107406#jpegparam) 物件 |`-` |JPEG 格式螢幕截圖的參數。 |
|JpgParam |[JpgParam](https://docs.byteplus.com/en/docs/24/107406#jpgparam) 物件 |`-` |JPG 格式螢幕截圖的參數。 |
|Interval |Integer |`10` |螢幕截圖的間隔時間，單位為秒。 |


<span id="jpegparam"></span>
### JpegParam


|**參數** |**資料型別** |**範例值** |**描述** |
|---|---|---|---|
|Enable |Boolean |`true` |是否啟用當前格式的螢幕截圖。有效值：<br><br><br>* `true`：啟用。<br><br>* `false`：未啟用。 |
|TOSParam |[TOSParam](https://docs.byteplus.com/en/docs/24/107406#tosparam) 物件 |`-` |TOS 的螢幕截圖儲存配置。 |


<span id="jpgparam"></span>
### JpgParam


|**參數** |**資料型別** |**範例值** |**描述** |
|---|---|---|---|
|Enable |Boolean |`false` |是否啟用當前格式的螢幕截圖。有效值：<br><br><br>* `true`：啟用。<br><br>* `false`：未啟用。 |
|TOSParam |[TOSParam](https://docs.byteplus.com/en/docs/24/107406#tosparam) 物件 |`-` |TOS 的螢幕截圖儲存配置。 |


<span id="tosparam"></span>
### TOSParam


|**參數** |**資料型別** |**範例值** |**描述** |
|---|---|---|---|
|Enable |Boolean |`true` |是否使用 TOS 儲存。有效值：<br><br><br>* `true`：使用。<br><br>* `false`：不使用。 |
|Bucket |String |`live-test-tos-example` |TOS 的儲存桶。例如，若儲存路徑為`live-test-tos-example/live/liveapp`，則參數值為`live-test-tos-example`。 |
|StorageDir |String |`live/liveapp` |TOS 儲存桶下的目錄。例如，若儲存路徑為`live-test-tos-example/live/liveapp`，則參數值為`live/liveapp`。 |
|ExactObject |String |`{Domain}/{App}/{Stream}/{UnixTimestamp}` |當螢幕截圖型別為非覆蓋模式時的儲存規則。您可以按照 {Domain}/{App}/{Stream}/{UnixTimestamp} 的格式配置規則。支援以下字元：<br><br><br>* 小寫字母 (a\-z)<br><br>* 大寫字母 (A\-Z)<br><br>* 數字 (0\-9)<br><br>* 連字號 (\-)<br><br>* 驚嘆號 (!)<br><br>* 底線 (_)<br><br>* 句點 (.)<br><br>* 星號 (\*)<br><br>* 佔位符 |
|OverwriteObject |字串 |`{Domain}/{App}/{Stream}` |當截圖類型為覆蓋時的儲存規則。您可以按照 {Domain}/{App}/{Stream} 的格式配置規則。支援以下字元：<br><br><br>* 小寫字母 (a\-z)<br><br>* 大寫字母 (A\-Z)<br><br>* 數字 (0\-9)<br><br>* 連字號 (\-)<br><br>* 驚嘆號 (!)<br><br>* 底線 (_)<br><br>* 句點 (.)<br><br>* 星號 (\*)<br><br>* 佔位符 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://open.byteplusapi.com/?Action=ListVhostSnapshotPresetV2&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "Type": "tos"
}
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListVhostSnapshotPresetV2",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "PresetList": [
            {
                "Vhost": "push.example.com",
                "App": "live",
                "SlicePreset": {
                    "SnapshotPresetConfig": {
                        "JpegParam": {
                            "Enable": true,
                            "TOSParam": {
                                "Enable": true,
                                "Bucket": "live-test-tos-example",
                                "StorageDir": "live/liveapp",
                                "ExactObject": "{Domain}/{App}/{Stream}/{UnixTimestamp}"
                            }
                        },
                        "Interval": 10
                    },
                    "Name": "preset-123",
                    "Status": "1"
                }
            }
        ]
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為本操作相關的錯誤碼。其他錯誤碼請參見[BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**說明** |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回錯誤碼，請[聯絡技術支援](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考請求參數說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料型別是否正確。 |
|403 |RequestForbidden |*  |請求被拒絕，因為當前帳號下無請求的資源（資源包括網域命名空間、網域、App、配置及憑證）。 |
|403 |RequestForbidden.AccountIDNotAllowed |此 AccountID 無權存取對應資源，請檢查請求參數 |請求被拒絕，因為當前帳號下無請求的資源（資源包括網域命名空間、網域、App、配置及憑證）。 |
|403 |RequestForbidden.BillingStatus |該 AccountID 未開通計費狀態，請開通服務或儲值。 |尚未開通 BytePlus MediaLive 服務或帳號欠費，導致帳單不可用。請檢查服務開通狀態及帳號欠費狀態。 |
|404 |ResourceNotFound |*  |未找到資源（包括網域命名空間、網域、App、配置及憑證）。建議重試。若仍返回錯誤碼，請[聯絡技術支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡技術支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.Preset |發生與預設相關的內部錯誤，請聯絡管理員。 |發生與功能配置相關的內部錯誤。請[聯絡技術支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡技術支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡技術支援](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請[聯絡技術支援](https://console.byteplus.com/workorder/create)。 |
