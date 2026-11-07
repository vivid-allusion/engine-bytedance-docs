---
title: "GetSubtitleTranscodePresetConfig"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/GetSubtitleTranscodePresetConfig-zh-CN"
---

调用`GetSubtitleTranscodePresetConfig` API，获取当前账号在字幕配置中AI配音模式下可用的字体和语言。

<span id="Requirements"></span>
## 要求

**请求频率限制**：每个账号每秒最多10次请求。

<span id="HTTP request"></span>
## HTTP请求


* 方法：GET

* Endpoint：https://open.byteplusapi.com/?Action=GetSubtitleTranscodePresetConfig&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有API调用时，除API专属参数外，还必须包含[通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`GetSubtitleTranscodePresetConfig` |API操作。 |
|Version |String |是 |`2023-01-01` |此API操作的版本。当前版本：2023\-01\-01。 |


<span id="Response parameters"></span>
## 返回调用结果参数

有关API专属返回调用结果参数，请参见下表。更多详情请参见[请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)部分。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Code |Integer |`0` |状态码。 |
|Message |String |`success` |状态信息。 |
|数据 |[数据](https://docs.byteplus.com/en/docs/24/118388#data)对象 |`-` |配置信息。 |


<span id="data"></span>
### 数据


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|AsrLang |JSON Map |`{"en": "英文","zh": "中文"}` |原始（ASR）字幕支持的语言列表。<br><br>格式为`"Key":"Value"`，每组`"Key":"Value"`之间用英文逗号（,）分隔。`Key`为语言代码，`Value`为语言的中文名称。<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">当前直播显示仅支持中文和英文。整句显示支持本参数返回的所有语言。</div><br> |
|字体 |JSON Map |`{"arial": {"Lang": ["en", "zh"], "Alias": ""}}` |支持的字体列表。<br><br>格式为`"Key":"Value"`，每组`"Key":"Value"`之间用英文逗号（,）分隔。`Key`为字体名称，`Value`为字体信息。详情请参见[字体](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSubtitleTranscodePresetConfig?lang=en#font)。 |
|Lang |JSON Map |`{"en": "英文","zh": "中文"}` |支持的目标语言列表。<br><br>格式为`"Key":"Value"`，每组`"Key":"Value"`之间用英文逗号（,）分隔。`Key`为语言代码，`Value`为语言的中文名称。 |
|OriginalLang |JSON Map |`{"en": "英文","zh": "中文"}` |字幕翻译及配音音频支持的源语言列表。<br><br>格式为`"Key":"Value"`，每组`"Key":"Value"`之间用英文逗号（,）分隔。`Key`为语言代码，`Value`为语言的中文名称。 |


<span id="font"></span>
### 字体


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Lang |String数组 |`["en", "zh"]` |该字体支持的语言代码。 |
|Alias |String |`-` |字体的中文名称。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
GET https://open.byteplusapi.com/?Action=GetSubtitleTranscodePresetConfig&Version=2023-01-01
```


<span id="Sample response"></span>
### 返回示例

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
## 错误码

关于错误码的更多信息，请参见[通用错误码](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes)。
