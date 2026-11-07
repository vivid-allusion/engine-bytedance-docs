---
title: "UpdateCarouselTask"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatecarouseltask-zh-TW"
---

調用 `UpdateCarouselTask` API 以修改指定的輪播任務配置，調整播放內容、播放規則或時間範圍，系統將於更新後依據新配置執行輪播任務。

<span id="Requirements"></span>
## 需求


* 頻率限制：每個帳戶每秒最多 10 次查詢。

* 保留原始配置：當未傳入非必填參數時，將維持目前輪播任務的原始配置，不會恢復為預設值。

* 僅支援更新執行中任務：僅支援更新處於 `running` 狀態的任務。可調用 `GetCarouselDetail` 與 `ListCarouselTask` API 查詢任務狀態。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=UpdateCarouselTask&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 必須同時傳入 API 專屬參數與 [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型態** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`UpdateCarouselTask` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型態** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|TaskID |String |是 |`44c5da50318440*********2d62c910b8` |待更新輪播任務的 ID，即任務的唯一識別碼。該值於調用 `CreateCarouselTask` 介面創建輪播任務時返回。 |
|Rule |[Rule](https://docs.byteplus.com/en/docs/24/107268#rule) 的物件 |是 |`-` |輪播規則用於指定輪播播放的素材及行為等。 |


<span id="rule"></span>
### Rule


|**參數** |**資料型態** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Loop |Integer |否 |`1` |指定此素材連續播放的次數。此欄位值必須大於或等於 `0`。若未傳入，將維持原輪播配置。支援的值及含義如下：<br><br><br>* `0`：不循環播放；<br><br>* 其他正整數：依指定次數循環播放。 |
|Source |[Source](https://docs.byteplus.com/en/docs/24/107268#source) 的陣列 |是 |`-` |輪播素材列表，用於指定輪播過程中播放的素材資源。 |
|SeekInfo |[SeekInfo](https://docs.byteplus.com/en/docs/24/107268#seekinfo) 的物件 |否 |`-` |用於控制素材更新後播放行為的配置參數。 |


<span id="source"></span>
### Source


|**參數** |**資料型態** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|ID |String |是 |`1` |輪播素材的唯一識別碼。同一播放列表中，每個素材的 `ID` 必須唯一，不可重複。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">若素材的 <code>ID</code> 未變（即更新後的 <code>ID</code> 與原素材的 <code>ID</code> 相同），僅可更新除 <code>Type</code> 與 <code>Url</code> 以外的其他參數。</div><br> |
|Type |String |是 |`vod` |輪播素材的檔案類型，用於指定素材的檔案來源類型。支援以下值：<br><br><br>* `vod`：點播 MP4 或 FLV 檔案；<br><br>* `m3u8`：點播 M3U8 檔案。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">如果素材的<code>ID</code>未變（即更新後的<code>ID</code>與原素材的<code>ID</code>相同），則<code>Type</code>的值應與原素材保持一致。</div><br> |
|Url |String |是 |`https://live.example.com/video.mp4` |輪播素材的公開可訪問地址。請確保所提供的地址可被公網正常訪問，以正確加載輪播素材內容。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">如果素材的<code>ID</code>未變（即更新後的<code>ID</code>與原素材的<code>ID</code>相同），則<code>Url</code>的值應與原素材保持一致。</div><br> |
|Seek |Integer |否 |`10` |用於控制播放當前素材時跳過開頭的一段時間。例如跳過片頭，單位為秒。僅當素材類型為點播（`type=vod`）時，此欄位有效。此欄位的使用規則如下：<br><br><br>* 如果`Seek`的值小於或等於`0`，或大於視頻實際時長，則此欄位不生效。<br><br>* 請根據點播素材的實際時長設置合適的值，以實現跳過片頭的效果。 |
|Loop |Integer |否 |`1` |指定該素材連續播放的次數。此欄位的值必須大於或等於`0`。如未傳入，則保持原有輪播配置。支持的值及含義如下：<br><br><br>* `0`：不循環播放；<br><br>* 其他正整數：按指定次數循環播放。 |


<span id="seekinfo"></span>
### SeekInfo


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Immediate |Long |否 |`1` |用於設置素材切換方式，預設值為`0`。支持的值及含義如下：<br><br><br>* `0`：播放完當前素材後切換到下一個素材；<br><br>* `1`：立即切換到指定素材，並從指定播放進度開始播放。 |
|SourceID |String |否 |`1f9f207a55a43f45` |更新後用於播放的素材ID，僅當`Immediate=1`時有效。<br><br><br>* 如未填寫，則直接從新素材的第一個素材開始播放。<br><br>* 如已填寫，則從對應的`SourceID`開始播放。 |
|SourceSeek |Long |否 |`10` |切換素材後的播放位置，單位為秒，表示從該位置開始播放，僅當`Immediate=1`時有效。如未填寫，則從`SourceID`對應素材的起始位置開始播放。 |


<span id="Response parameters"></span>
## 回應參數

有關 API 專屬回應參數，請參見下表。更多細節請參考 [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 章節。


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Data |[Data](https://docs.byteplus.com/en/docs/24/107268#data)的物件 |`-` |包含任務更新相關資訊的資料物件。 |


<span id="data"></span>
### 資料


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|OptID |Integer |`2` |當前生效任務配置的序號，用於標識最新的任務修改記錄。每次任務配置更新後，該值會自動遞增。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```json
POST https://open.byteplusapi.com/?Action=UpdateCarouselTask&Version=2023-01-01
{
    "TaskID": "44c5da50318440*********2d62c910b8",
    "Rule": {
        "Loop": 1,
        "Source": [
            {
                "ID": "1",
                "Type": "vod",
                "Url": "https://live.example.com/video.mp4",
                "Seek": 10,
                "Loop": 1
            }
        ],
        "SeekInfo": {
            "Immediate": 1,
            "SourceID": "1f9f207a55a43f45",
            "SourceSeek": 10
        }
    }
}
```


<span id="Sample response"></span>
### 回應範例

```json
{
    "ResponseMetadata": {
        "RequestID": "202410301532184E885F20A2263C133082",
        "RequestId": "20230604110420****100232280022D31",
        "Action": "UpdateCarouselTask",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Data": {
            "OptID": 2
        }
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為本操作相關的錯誤碼。其他錯誤碼請參見 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**說明** |
|---|---|---|---|
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參閱[請求參數](https://docs.byteplus.com/en/docs/24/107268#request-parameters)說明以進行檢查。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
