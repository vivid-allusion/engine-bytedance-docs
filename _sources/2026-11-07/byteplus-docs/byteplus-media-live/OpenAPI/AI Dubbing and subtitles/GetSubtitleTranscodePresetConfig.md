---
title: "GetSubtitleTranscodePresetConfig"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/GetSubtitleTranscodePresetConfig"
---

Call the `GetSubtitleTranscodePresetConfig` API to get the fonts and languages that are available to the current account for AI Dubbing mode in subtitle configurations.

<span id="requirements"></span>
## Requirements

**Rate limit**: 10 requests per second per account.

<span id="http-request"></span>
## HTTP request


* Method: GET

* Endpoint: https://open.byteplusapi.com/?Action=GetSubtitleTranscodePresetConfig&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`GetSubtitleTranscodePresetConfig` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Code |Integer |`0` |The status code. |
|Message |String |`success` |The status message. |
|Data |Object of [Data](https://docs.byteplus.com/en/docs/24/117625#data) |`-` |The configuration information. |


<span id="data"></span>
### Data


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|AsrLang |JSON Map |`{"en": "英文","zh": "中文"}` |The list of languages supported by Original (ASR) subtitles.<br><br>The format is `"Key":"Value"`, and each `"Key":"Value"` pair is separated by an English comma (,). `Key` is the language code, and `Value` is the Chinese name of the language.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Currently, live streaming display only supports Chinese and English. Whole\-sentence display supports all languages returned by this parameter.</div><br> |
|Font |JSON Map |`{"arial": {"Lang": ["en", "zh"], "Alias": ""}}` |The list of supported fonts.<br><br>The format is `"Key":"Value"`, and each `"Key":"Value"` pair is separated by an English comma (,). `Key` is the font name, and `Value` is the font information. For details, see [Font](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSubtitleTranscodePresetConfig?lang=en#font). |
|Lang |JSON Map |`{"en": "英文","zh": "中文"}` |The list of supported target languages.<br><br>The format is `"Key":"Value"`, and each `"Key":"Value"` pair is separated by an English comma (,). `Key` is the language code, and `Value` is the Chinese name of the language. |
|OriginalLang |JSON Map |`{"en": "英文","zh": "中文"}` |The list of source languages supported by subtitle translation and dubbed audio.<br><br>The format is `"Key":"Value"`, and each `"Key":"Value"` pair is separated by an English comma (,). `Key` is the language code, and `Value` is the Chinese name of the language. |


<span id="font"></span>
### Font


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Lang |Array of String |`["en", "zh"]` |The language codes supported by the font. |
|Alias |String |`-` |The Chinese name of the font. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
GET https://open.byteplusapi.com/?Action=GetSubtitleTranscodePresetConfig&Version=2023-01-01
```


<span id="sample-response"></span>
### Sample response

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


<span id="error-codes"></span>
## Error codes

For more information about error codes, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).
