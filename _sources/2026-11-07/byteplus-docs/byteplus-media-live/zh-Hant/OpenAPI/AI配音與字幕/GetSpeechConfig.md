---
title: "GetSpeechConfig"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/GetSpeechConfig-zh-TW"
---

調用 `GetSpeechConfig` API 以獲取當前帳戶可用的 AI 配音配置，包括支援的字體和語言。

<span id="Requirements"></span>
## 需求

**速率限制**：每個帳戶每秒 10 次請求。

<span id="HTTP request"></span>
## HTTP 請求


* 方法：GET

* 端點：https://open.byteplusapi.com/?Action=GetSpeechConfig&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 調用時，除 API 專屬參數外，還必須帶上 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料類型** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |字串 |是 |`GetSpeechConfig` |API 操作名稱。 |
|Version |字串 |是 |`2023-01-01` |此 API 操作的版本。當前版本：2023\-01\-01。 |


<span id="Response parameters"></span>
## 回應參數

有關 API 專屬回應參數，請參見下表。更多詳情請參考 [請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 章節。


|**參數** |**資料類型** |**範例值** |**說明** |
|---|---|---|---|
|Code |整數 |`0` |狀態碼。 |
|Message |字串 |`success` |狀態訊息。 |
|Data |[Data](https://docs.byteplus.com/en/docs/24/118401#data) 物件 |`-` |配置信息。 |


<span id="data"></span>
### 資料


|**參數** |**資料類型** |**範例值** |**說明** |
|---|---|---|---|
|Font |JSON Map |`{"arial": {"Lang": ["en", "zh"], "Alias": ""}}` |支援的字體列表。<br><br>格式為 `"Key":"Value"`，每組 `"Key":"Value"` 之間以英文逗號（,）分隔。`Key` 為字體名稱，`Value` 為字體資訊。更多資訊請參見 [Font](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSpeechConfig?lang=en#font)。 |
|OriginalLang |JSON Map |`{"en": "英文","zh": "中文"}` |支援的來源語言列表。<br><br>格式為 `"Key":"Value"`，每組 `"Key":"Value"` 之間以英文逗號（,）分隔。`Key` 為語言代碼，`Value` 為語言的中文名稱。 |
|Lang |JSON Map |`{"en": "英文","zh": "中文"}` |支援的目標語言列表。<br><br>格式為 `"Key":"Value"`，每組 `"Key":"Value"` 之間以英文逗號（,）分隔。`Key` 為語言代碼，`Value` 為語言的中文名稱。 |
|AsrLang |JSON Map |`{"en": "英文","zh": "中文"}` |Original（ASR）字幕支援的語言列表。<br><br>格式為 `"Key":"Value"`，每組 `"Key":"Value"` 之間以英文逗號（,）分隔。`Key` 為語言代碼，`Value` 為語言的中文名稱。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">目前，直播顯示僅支援中文和英文。整句顯示支援本參數返回的所有語言。</div><br> |


<span id="font"></span>
### 字體


|**參數** |**資料類型** |**範例值** |**說明** |
|---|---|---|---|
|Alias |字串 |`-` |字體的中文名稱。 |
|Lang |字串陣列 |`["en", "zh"]` |該字體支援的語言代碼。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
GET https://open.byteplusapi.com/?Action=GetSpeechConfig&Version=2023-01-01
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestID": "20251117153036AE514BF03AA6032F086E",
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetSpeechConfig",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Code": 0,
        "Message": "success",
        "Data": {
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
            "AsrLang": {
                "en": "英文",
                "zh": "中文"
            },
            "OriginalLang": {
                "en": "英文",
                "zh": "中文"
            }
        }
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

有關錯誤碼的更多資訊，請參見 [通用錯誤碼](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes)。
