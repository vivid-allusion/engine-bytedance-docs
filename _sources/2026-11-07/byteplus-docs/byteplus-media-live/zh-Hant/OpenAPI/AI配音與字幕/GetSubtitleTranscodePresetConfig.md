---
title: "GetSubtitleTranscodePresetConfig"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/GetSubtitleTranscodePresetConfig-zh-TW"
---

調用 `GetSubtitleTranscodePresetConfig` API，以獲取目前帳戶在字幕配置的 AI 配音模式下可用的字體和語言。

<span id="Requirements"></span>
## 需求

**速率限制**：每個帳戶每秒最多 10 次請求。

<span id="HTTP request"></span>
## HTTP 請求


* 方法：GET

* 端點：https://open.byteplusapi.com/?Action=GetSubtitleTranscodePresetConfig&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了需帶有 API 專屬參數外，還必須帶上 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`GetSubtitleTranscodePresetConfig` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Response parameters"></span>
## 回應參數

有關 API 專屬回應參數，請參見下表。更多細節請參考 [請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 部分。


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Code |Integer |`0` |狀態碼。 |
|Message |String |`success` |狀態訊息。 |
|Data |[Data](https://docs.byteplus.com/en/docs/24/118407#data) 物件 |`-` |配置資訊。 |


<span id="data"></span>
### 資料


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|AsrLang |JSON Map |`{"en": "英文","zh": "中文"}` |原始（ASR）字幕所支援的語言列表。<br><br>格式為 `"Key":"Value"`，每組 `"Key":"Value"` 以英文逗號（,）分隔。`Key` 為語言代碼，`Value` 為語言的中文名稱。<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">目前直播顯示僅支援中文與英文。整句顯示支援本參數回傳的所有語言。</div><br> |
|Font |JSON Map |`{"arial": {"Lang": ["en", "zh"], "Alias": ""}}` |支援的字體列表。<br><br>格式為 `"Key":"Value"`，每組 `"Key":"Value"` 以英文逗號（,）分隔。`Key` 為字體名稱，`Value` 為字體資訊。詳情請參見 [Font](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSubtitleTranscodePresetConfig?lang=en#font)。 |
|Lang |JSON Map |`{"en": "英文","zh": "中文"}` |支援的目標語言列表。<br><br>格式為 `"Key":"Value"`，每組 `"Key":"Value"` 以英文逗號（,）分隔。`Key` 為語言代碼，`Value` 為語言的中文名稱。 |
|OriginalLang |JSON Map |`{"en": "英文","zh": "中文"}` |字幕翻譯及配音所支援的原始語言列表。<br><br>格式為 `"Key":"Value"`，每組 `"Key":"Value"` 以英文逗號（,）分隔。`Key` 為語言代碼，`Value` 為語言的中文名稱。 |


<span id="font"></span>
### 字體


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Lang |字串陣列 |`["en", "zh"]` |字體所支援的語言代碼。 |
|Alias |String |`-` |字體的中文名稱。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
GET https://open.byteplusapi.com/?Action=GetSubtitleTranscodePresetConfig&Version=2023-01-01
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetSubtitleTranscodePresetConfig",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Code": 0,
        "Data": {
            "AsrLang": {
                "en": "英文",
                "zh": "中文"
            },
            "Font": {
                "arial": {
                    "Lang": [
                        "en",
                        "zh"
                    ],
                    "Alias": ""
                }
            },
            "Lang": {
                "en": "英文",
                "zh": "中文"
            },
            "OriginalLang": {
                "en": "英文",
                "zh": "中文"
            }
        },
        "Message": "success"
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

有關錯誤碼的更多資訊，請參見 [通用錯誤碼](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes)。
