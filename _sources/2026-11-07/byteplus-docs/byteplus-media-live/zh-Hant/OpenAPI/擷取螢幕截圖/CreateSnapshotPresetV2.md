---
title: "CreateSnapshotPresetV2"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/createsnapshotpresetv2-zh-TW"
---

新增螢幕截圖配置，用於在直播流落入螢幕截圖配置的有效範圍時，捕捉並保存直播流的螢幕截圖。

<span id="Usage scenario"></span>
## 使用場景

螢幕截圖配置會根據`Vhost`和`App`指定適用的直播流範圍。當直播流所使用的網域屬於已配置的`Vhost`，且直播流的`AppName`欄位與`App`配置相符時，該直播流將會被捕捉並保存螢幕截圖。

<span id="Requirements"></span>
## 需求


* 前提：若選擇將螢幕截圖檔案儲存於TOS，必須先開通TOS服務並聯絡[技術支援](https://console.byteplus.com/workorder/create)進行授權。

* 計費：直播流螢幕截圖功能需付費。更多資訊請參見[螢幕截圖捕捉](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-screenshot-capturing)。

* 頻率限制：每個帳戶每秒最多10次請求。

* 生效：若要使螢幕截圖配置的新增、更新或刪除生效，需在修改後3\-5分鐘再次推流。


<span id="HTTP request"></span>
## HTTP請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=CreateSnapshotPresetV2&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有API除了專屬參數外，皆需帶入[通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型態** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`CreateSnapshotPresetV2` |API操作名稱。 |
|Version |String |是 |`2023-01-01` |本API操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body參數


|**參數** |**資料型態** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |網域命名空間，即直播流地址所屬的網域命名空間。可呼叫[ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023)或前往**Domains**頁面於[BytePlus MediaLive 控制台](https://console.byteplus.com/live/main/domain/list)查詢直播流所用網域的命名空間。 |
|App |String |是 |`live` |應用名稱，與直播流地址中的`AppName`欄位值一致。名稱需為1\-30個字元，可包含以下字元：<br><br><br>* 大寫字母（A\-Z）<br><br>* 小寫字母（a\-z）<br><br>* 數字（0\-9）<br><br>* 底線（_）<br><br>* 連字號（\-）<br><br>* 句點（.） |
|Status |Integer |否 |`1` |螢幕截圖配置是否生效。預設值：`1`。有效值：<br><br><br>* `1`：生效。<br><br>* `0`：不生效。 |
|SnapshotPresetConfig |[SnapshotPresetConfig](https://docs.byteplus.com/en/docs/24/107323#snapshotpresetconfig)物件 |是 |`-` |螢幕截圖配置的詳細參數。 |


<span id="snapshotpresetconfig"></span>
### SnapshotPresetConfig


|**參數** |**資料型態** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|JpegParam |[JpegParam](https://docs.byteplus.com/en/docs/24/107323#jpegparam)物件 |否 |`-` |JPEG格式螢幕截圖的參數，啟用JPEG截圖時需設定。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">必須啟用JPEG或JPG截圖其中之一，不能同時啟用。</div><br> |
|JpgParam |[JpgParam](https://docs.byteplus.com/en/docs/24/107323#jpgparam)物件 |否 |`-` |JPG格式螢幕截圖的參數，啟用JPG截圖時需設定。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">必須啟用JPEG或JPG截圖其中之一，不能同時啟用。</div><br> |
|Interval |Integer |否 |`10` |螢幕截圖的間隔時間（秒）。預設值：`10`。值必須為正整數。 |


<span id="jpegparam"></span>
### JpegParam


|**參數** |**資料型態** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Enable |Boolean |否 |`true` |是否啟用當前格式的螢幕截圖。預設值：`false`。有效值：<br><br><br>* `true`：啟用。<br><br>* `false`：停用。 |
|TOSParam |[TOSParam](https://docs.byteplus.com/en/docs/24/107323#tosparam) 的物件 |否 |`-` |在 TOS 儲存螢幕截圖的配置。 |


<span id="jpgparam"></span>
### JpgParam


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Enable |Boolean |否 |`false` |是否啟用目前格式的螢幕截圖。預設值：`false`。有效值：<br><br><br>* `true`：啟用。<br><br>* `false`：停用。 |
|TOSParam |[TOSParam](https://docs.byteplus.com/en/docs/24/107323#tosparam) 的物件 |否 |`-` |在 TOS 儲存螢幕截圖的配置。 |


<span id="tosparam"></span>
### TOSParam


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Enable |Boolean |否 |`true` |是否使用 TOS 進行儲存。預設值：`false`。有效值：<br><br><br>* `true`：使用 TOS。<br><br>* `false`：不使用 TOS。 |
|Bucket |String |否 |`live-test-tos-example` |TOS 儲存的 bucket。例如，若儲存路徑為 `live-test-tos-example/live/liveapp`，則參數值為 `live-test-tos-example`。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">使用 TOS 儲存時，此參數為必填。</div><br> |
|StorageDir |String |否 |`live/liveapp` |TOS 儲存 bucket 下的儲存目錄。預設值為空。例如，若儲存路徑為 `live-test-tos-example/live/liveapp`，則參數值為 `live/liveapp`。 |
|ExactObject |String |否 |`{Domain}/{App}/{Stream}/{UnixTimestamp}` |螢幕截圖類型為非覆寫時的儲存規則。可依 {Domain}/{App}/{Stream}/{UnixTimestamp} 格式配置規則。支援以下字元：<br><br><br>* 小寫字母 (a\-z)<br><br>* 大寫字母 (A\-Z)<br><br>* 數字 (0\-9)<br><br>* 連字號 (\-)<br><br>* 驚嘆號 (!)<br><br>* 底線 (_)<br><br>* 句點 (.)<br><br>* 星號 (\*)<br><br>* 佔位符<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">必須傳入 <code>ExactObject</code> 或 <code>OverwriteObject</code>。</div><br> |
|OverwriteObject |String |否 |`{Domain}/{App}/{Stream}` |螢幕截圖類型為覆寫時的儲存規則。可依 {Domain}/{App}/{Stream} 格式配置規則。支援以下字元：<br><br><br>* 小寫字母 (a\-z)<br><br>* 大寫字母 (A\-Z)<br><br>* 數字 (0\-9)<br><br>* 連字號 (\-)<br><br>* 驚嘆號 (!)<br><br>* 底線 (_)<br><br>* 句點 (.)<br><br>* 星號 (\*)<br><br>* 佔位符<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">必須傳入 <code>ExactObject</code> 或 <code>OverwriteObject</code>。</div><br> |


<span id="Response parameters"></span>
## 回應參數

有關API專屬回應參數，請參見下表。更多細節請參考[請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)章節。


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|PresetName |String |`preset-123` |螢幕截圖配置名稱。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```json
POST https://open.byteplusapi.com/?Action=CreateSnapshotPresetV2&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "App": "live",
    "Status": 1,
    "SnapshotPresetConfig": {
        "JpegParam": {
            "Enable": true,
            "TOSParam": {
                "Enable": true,
                "Bucket": "live-test-tos-example",
                "StorageDir": " live/liveapp",
                "ExactObject": "{Domain}/{App}/{Stream}/{UnixTimestamp}"
            }
        },
        "Interval": 10
    }
}
```


<span id="Sample response"></span>
### 回應範例

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateSnapshotPresetV2",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "PresetName": "preset-123"
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為本操作相關的錯誤碼。其他錯誤碼請參見[BytePlus OpenAPI通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**說明** |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回錯誤碼，請 [聯繫技術支援](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考請求參數說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料型別是否正確。 |
|403 |RequestForbidden |*  |因目前帳戶下無請求資源（資源包括網域命名空間、網域、應用、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.AccountIDNotAllowed |此 AccountID 無權存取對應資源，請檢查請求參數 |因目前帳戶下無請求資源（資源包括網域命名空間、網域、應用、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.BillingStatus |AccountID 的計費狀態不可用，請開通服務或充值。 |BytePlus MediaLive 服務尚未開通或帳戶欠費，導致帳單不可用。請檢查服務開通狀態及帳戶欠費狀態。 |
|404 |ResourceNotFound |*  |未找到資源（包括網域命名空間、網域、應用、配置及憑證）。建議重試。若仍返回錯誤碼，請 [聯繫技術支援](https://console.byteplus.com/workorder/create)。 |
|429 |RequestLimitExceeded.Exist |%s 已存在 |您請求建立的資源（包括網域命名空間、網域、應用程式、設定及憑證）已存在。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡技術支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.Preset |發生與預設相關的內部錯誤，請聯絡管理員。 |發生與功能設定相關的內部錯誤。請[聯絡技術支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡技術支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡技術支援](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請[聯絡技術支援](https://console.byteplus.com/workorder/create)。 |
