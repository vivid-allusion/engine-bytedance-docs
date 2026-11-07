---
title: "GetSpeechConfig"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/GetSpeechConfig-zh-CN"
---

调用`GetSpeechConfig` API 获取当前账号可用的 AI 配音配置信息，包括支持的字体和语言。

<span id="Requirements"></span>
## 要求

**请求频率限制**：每个账号每秒最多 10 次请求。

<span id="HTTP request"></span>
## HTTP 请求


* 方法：GET

* Endpoint：https://open.byteplusapi.com/?Action=GetSpeechConfig&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 调用时，除 API 专有参数外，还必须携带[通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`GetSpeechConfig` |API 操作名称。 |
|Version |String |是 |`2023-01-01` |该 API 操作的版本号。当前版本：2023\-01\-01。 |


<span id="Response parameters"></span>
## 返回调用结果参数

关于 API 专有的返回调用结果参数，请参见下表。更多详情请参见[请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)部分。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Code |Integer |`0` |状态码。 |
|Message |String |`success` |状态信息。 |
|Data |[Data](https://docs.byteplus.com/en/docs/24/118390#data) 对象 |`-` |配置信息。 |


<span id="data"></span>
### 数据


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Font |JSON Map |`{"arial": {"Lang": ["en", "zh"], "Alias": ""}}` |支持的字体列表。<br><br>格式为`"Key":"Value"`，每组`"Key":"Value"`之间用英文逗号（,）分隔。`Key` 为字体名称，`Value` 为字体信息。更多信息请参见[Font](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSpeechConfig?lang=en#font)。 |
|OriginalLang |JSON Map |`{"en": "英文","zh": "中文"}` |支持的源语言列表。<br><br>格式为`"Key":"Value"`，每组`"Key":"Value"`之间用英文逗号（,）分隔。`Key` 为语言代码，`Value` 为语言的中文名称。 |
|Lang |JSON Map |`{"en": "英文","zh": "中文"}` |支持的目标语言列表。<br><br>格式为`"Key":"Value"`，每组`"Key":"Value"`之间用英文逗号（,）分隔。`Key` 为语言代码，`Value` 为语言的中文名称。 |
|AsrLang |JSON Map |`{"en": "英文","zh": "中文"}` |支持原文（ASR）字幕的语言列表。<br><br>格式为`"Key":"Value"`，每组`"Key":"Value"`之间用英文逗号（,）分隔。`Key` 为语言代码，`Value` 为语言的中文名称。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">当前直播展示仅支持中文和英文。整句展示支持本参数返回的所有语言。</div><br> |


<span id="font"></span>
### 字体


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Alias |String |`-` |字体的中文名称。 |
|Lang |Array of String |`["en", "zh"]` |该字体支持的语言代码。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
GET https://open.byteplusapi.com/?Action=GetSpeechConfig&Version=2023-01-01
```


<span id="Sample response"></span>
### 返回示例

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
## 错误码

关于错误码的更多信息，请参见[通用错误码](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes)。
