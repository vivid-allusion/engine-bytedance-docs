---
title: "ListVhostSubtitleTranscodePreset"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostsubtitletranscodepreset-2023"
---

Call the `ListVhostSubtitleTranscodePreset` API to query all subtitle configurations under a specific domain name space.

## Requirements

**Rate limit**: 10 requests per second per account.

## HTTP request

* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=ListVhostSubtitleTranscodePreset&Version=2023\-01\-01

## Request parameters

### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

### Query

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`ListVhostSubtitleTranscodePreset` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |

### Body parameters

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Vhost |String |Yes |`push.example.com` |The domain name space where the domains for stream pushing and pulling belong.<br><br>You can get the domain name space in any of the following ways:<br><br><br>* Call [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023), and get the domain name space by using the response parameter `Vhost`.<br><br>* On the [Domains](https://console.byteplus.com/live/main/domain) page in the MediaLive console, click **Settings** at the right of a specific domain and get the domain name space from the **Domain name space** field. |

## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|PresetList |Array of [PresetList](https://docs.byteplus.com/en/docs/24/28045#presetlist) |`-` |The list of subtitle configurations. |

### PresetList

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Vhost |String |`push.example.com` |The domain name space. |
|App |String |`live` |The `AppName`. |
|Suffixes |Array of String |`["_hd","_bd"]` |The transcoding suffixes. For example, if the transcoded stream address is `rtmp://pull.example.com/live/test_hd`, the transcoding suffix is `_hd`. |
|TranscodePreset |Object of [TranscodePreset](https://docs.byteplus.com/en/docs/24/28045#transcodepreset) |`-` |The details of the subtitle configuration. |

### TranscodePreset

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|PresetName |String |`OriginPreset` |The name of the subtitle configuration. |
|Description |String |`subtitleconfig0001` |The description of the subtitle configuration. |
|SuffixName |String |`_subtitle` |The subtitle suffix. For example, if the subtitle stream address is `rtmp://pull.example.com/live/test_subtitle`, the subtitle suffix is `_subtitle`. |
|Delay |Integer |`12` |The playback delay, in seconds, used to allow enough time for dubbed audio and subtitle translation.<br><br>> **说明**<br><br><br><br>* > If subtitles appear earlier than the original sound or video, reduce the playback delay to align subtitles with the original sound or video, and vice versa.<br><br><br>* > This parameter takes effect only when `Enable` under `SIConfig` is set to `true`.<br> |
|DisplayPreset |String |`small` |Not recommended. The preset effect used for quick configuration.<br><br>After this parameter is passed, the system automatically adapts `Font`, `MaxRowNumber`, `MaxCharNumber`, and `Position`. The `MaxRowNumber`, `MaxCharNumber`, and `Position` parameters no longer take effect. Valid values:<br><br><br>* `small`: Small\-sized subtitles.<br><br>* `medium`: Medium\-sized subtitles.<br><br>* `large`: Large\-sized subtitles. |
|MaxRowNumber |Integer |`0` |The maximum number of subtitle lines for each language. Valid values:<br><br><br>* `0`: Automatically wraps lines based on the total number of subtitle characters and the maximum number of characters per line to ensure complete display.<br><br>* `1`: Displays up to one line for each language. Content may be truncated.<br><br>* `2`: Displays up to two lines for each language. Content may be truncated.<br><br><br>> **说明**<br><br><br><br>* > If `DisplayPreset` is passed, this parameter is fixed to `0`.<br><br><br>* > This parameter applies separately to source and translated subtitles. Line limits for source and translated subtitles are calculated separately.<br> |
|Position |Object of [Position](https://docs.byteplus.com/en/docs/24/28045#position) |`-` |The subtitle position.<br><br>> **说明**<br><br><br>> If `DisplayPreset` is passed, this parameter does not take effect.<br> |
|SIConfig |Object of [SIConfig](https://docs.byteplus.com/en/docs/24/28045#siconfig) |`-` |The AI Dubbing mode configuration. |
|SourceLanguage |Object of [SourceLanguage](https://docs.byteplus.com/en/docs/24/28045#sourcelanguage) |`-` |The source subtitle configuration. |
|TargetLanguage |Array of [TargetLanguage](https://docs.byteplus.com/en/docs/24/28045#targetlanguage) |`-` |The translated subtitle configuration. |
|HotWordList |Array of String |`["MediaLive","LiveCore"]` |The hotword list.<br><br>Hotwords must match the source language and are used as a reference for the speech recognition model to help improve recognition accuracy for Original (ASR) subtitles, **but hotwords may not be recognized accurately every time**.<br><br>> **注意**<br><br><br>> This parameter takes effect only for **Original (ASR) subtitles**.<br> |
|GlossaryWordList |Array of String |`["赛事直播:sports live streaming","实时字幕:real-time subtitles"]` |The glossary.<br><br>Each array element must be in the format `"original text:translation"` and records proprietary vocabulary and expected translations, such as brand names, personal names, product names, or feature names. Glossary entries are used as a reference for the translation model to help improve translation accuracy for proprietary vocabulary, **but the expected translations may not be used every time**.<br><br>> **注意**<br><br><br>> This parameter takes effect only when `TargetLanguage` is configured and **applies only to translated subtitles**.<br> |
|ReplaceMap |JSON Map |`{"live core":"LiveCore","media life":"MediaLive"}` |The correction list.<br><br>Forced replacement rules for subtitle text. The format is `"incorrect text":"correct text"`. When the system matches the incorrect text, it forcibly replaces the incorrect text with the correct text.<br><br><br>* **Original (ASR) subtitles**: Corrects recognition errors.<br><br>* **Translated subtitles**: Corrects mistranslations. **Corrections modify only translated subtitles and do not modify source subtitles or dubbed audio**. |
|SIOutput |Object of [SIOutput](https://docs.byteplus.com/en/docs/24/28045#sioutput) |`-` |Output\-related configuration. |

### Position

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Relative |String |`bottom` |The subtitle position in the video. Valid values:<br><br><br>* `top`: Displays subtitles at the top of the video.<br><br>* `bottom`: Displays subtitles at the bottom of the video. |
|MarginVertical |Float |`0.5` |The top or bottom margin of the subtitles, that is, the distance from subtitles to the top or bottom edge of the video. The value is a percentage of the video height. Valid range: `(0, 0.5]`.<br><br><br>* When `Relative` is set to `top`, this parameter specifies the top margin.<br><br>* When `Relative` is set to `bottom`, this parameter specifies the bottom margin. |
|MarginHorizontal |Float |`0.2` |The left and right margins of the subtitles, that is, the distance from subtitles to the left and right edges of the video. The value is a percentage of the video width. Valid range: `(0, 0.3]`. |

### SIConfig

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Enable |Boolean |`true` |Whether to enable AI Dubbing mode. Valid values:<br><br><br>* `true`: Enables AI Dubbing mode. This mode supports subtitles, dubbed audio that replaces the original sound, and lip sync for an immersive experience.<br><br>* `false`: Disables AI Dubbing mode and enables Subtitle Only mode. After the AI Dubbing mode is disabled, other parameters in `SIConfig` do not take effect. |
|Pipe |String |`si` |The AI Dubbing type. Valid values:<br><br><br>* `si`: Subtitles, dubbed audio, and video are fully synchronized. Lip sync is supported. This mode is suitable for conference live streams and other scenarios that require strong synchronization and immersion.<br><br>* `mix`: Subtitles only.<br><br>* `realtime`: Original (ASR) subtitles in live streaming display. |
|SpeakerRecognition |Integer |`1` |Whether to enable dubbed audio. Valid values:<br><br><br>* A value greater than `0`: Enables dubbed audio. After this feature is enabled, translated speech with voice cloning is provided to replace the original sound.<br><br>* `0`: Disables dubbed audio.<br><br><br>> **说明**<br><br><br>> This parameter takes effect only when `Pipe` is empty or set to `si`.<br> |
|DigitalHumanMouthShape |Boolean |`false` |Whether to enable lip sync. Valid values:<br><br><br>* `true`: Enables lip sync. After this feature is enabled, the speaker's lip movements are synchronized with the dubbed audio, making the live stream more immersive.<br><br>* `false`: Disables lip sync.<br><br><br>> **说明**<br><br><br><br>* > This parameter takes effect only when `Pipe` is empty or set to `si`.<br><br><br>* > When this parameter is set to `true`, dubbed audio is enabled by default.<br> |
|PipeExtra |String |`{"Separator":{"HandleType":1},"Amix":{"AudioEnhance":false}}` |Extra configuration in JSON string format, including volume balance, noise reduction, and original sound volume. For more information, see the `Extra` parameter of [CreateSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/CreateSpeechTask).<br><br>> **说明**<br><br><br>> This parameter takes effect only when `SpeakerRecognition` is greater than `0`, that is, when dubbed audio is enabled.<br> |

### SourceLanguage

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Display |Boolean |`true` |Whether to display source subtitles. Valid values:<br><br><br>* `true`: Display. Both the source and translated subtitles will be displayed.<br><br>* `false`: Do not display. Only the translated subtitles will be displayed. |
|Language |String |`zh` |The source subtitle language.<br><br><br>* When the value of `Enable` under `SIConfig` is set to `true` and AI Dubbing mode is used, you can call [GetSubtitleTranscodePresetConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSubtitleTranscodePresetConfig) and use `OriginalLang` to get the display names of source subtitle languages, or use `AsrLang` to get the display names of Original (ASR) subtitle languages.<br><br>* When the value of `Enable` under `SIConfig` is set to `false` and Subtitle Only mode is used, valid values are as follows:<br><br>   * `zh`: Mix of Chinese and English.<br><br>   * `en`: English.<br><br>   * `ko`: Korean.<br><br>   * `ja`: Japanese. |
|ShowPriority |Integer |`2` |The display priority of source subtitles. A larger value indicates a higher priority. For example, if the `ShowPriority` of source subtitles is `1` and `ShowPriority` of translated subtitles is `2`, translated subtitles are displayed above source subtitles. |
|MaxCharNumber |Integer |`60` |The maximum number of characters per line for source subtitles.<br><br>> **说明**<br><br><br><br>* > The system calculates the final maximum number of displayable characters per line based on this parameter, `MarginLr`, `Font`, `FontSize`, screen resolution, and other factors.<br><br><br>* > Each Chinese character, letter, symbol, or digit counts as one character.<br><br><br>* > When `MaxRowNumber` is set to `1` or `2`, if the total number of source subtitle characters exceeds the display range, the content is truncated. For example, if the maximum number of characters per line is 10 and `MaxRowNumber` is `2`, content after the 20th character is truncated.<br><br><br>* > If `DisplayPreset` is passed, this parameter does not take effect.<br> |
|Font |String |`siyuanheiti` |The source subtitle font.<br><br><br>* When the value of `Enable` under `SIConfig` is set to `true` and AI Dubbing mode is used, you can call [GetSubtitleTranscodePresetConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSubtitleTranscodePresetConfig) and use `Alias` to get the display name of the font.<br><br>* When the value of `Enable` under `SIConfig` is set to `false` and Subtitle Only mode is used, valid values depend on the source subtitle language (`Language`).<br><br>   * If the source subtitle language is `zh`, the following fonts are supported:<br><br>      * `siyuanheiti`: Source Han Sans.<br><br>      * `songtixi`: Songti Light.<br><br>      * `songticu`: Songti Bold.<br><br>      * `heitifan`: Heiti Traditional.<br><br>      * `kaiti`: Kaiti.<br><br>   * If the source subtitle language is `en`, the following fonts are supported:<br><br>      * `inter`: Inter.<br><br>      * `roboto`: Roboto.<br><br>      * `opposans`: OPPOSans.<br><br>      * `siyuansongti`: Source Han Serif.<br><br>      * `montserrat`: Montserrat.<br><br>   * If the source subtitle language is `ko` or `ja`, `notosans` (Noto Sans) is supported. |
|FontSize |Integer |`18` |The source subtitle font size, in px.<br><br>> **说明**<br><br><br>> If `DisplayPreset` is passed, this parameter does not take effect.<br> |
|FontColor |String |`0xFF0000@0.5` |The source subtitle font color. You can specify the color in one of the following ways:<br><br><br>* Start with `0x` or `#`, followed by a hexadecimal RGB color value, and append opacity with `@`. Opacity supports hexadecimal values such as `0x80` and decimal values such as `0.5`. For example, to specify red (`FF0000`) with 50% opacity, pass `0xFF0000@0x80`, `0xFF0000@0.5`, `#FF0000@0x80`, or `#FF0000@0.5`.<br><br>* Use an FFmpeg color keyword and append opacity with `@`. Opacity supports decimal values such as `0.5`. For example, to specify `0xF0F8FF` with 50% opacity, pass `AliceBlue@0.5`.<br><br><br>> **说明**<br><br><br><br>* > For color definitions and more color keywords, see [FFmpeg color syntax](https://ffmpeg.org/ffmpeg-utils.html#color-syntax).<br><br><br>* > A larger opacity value means less transparency.<br> |
|Border |Object of [Border](https://docs.byteplus.com/en/docs/24/28045#border) |`-` |The font shadow of source subtitles. |
|Box |Object of [Box](https://docs.byteplus.com/en/docs/24/28045#box) |`-` |The font background of source subtitles. |

### TargetLanguage

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Language |String |`en` |The translated subtitle language.<br><br><br>* When the value of `Enable` under `SIConfig` is set to `true` and AI Dubbing mode is used, you can call [GetSubtitleTranscodePresetConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSubtitleTranscodePresetConfig) and use `Lang` to get the display names of translated subtitle languages.<br><br>* When the value of `Enable` under `SIConfig` is set to `false` and Subtitle Only mode is used, valid values are as follows:<br><br>   * `zh`: Mix of Chinese and English.<br><br>   * `en`: English.<br><br>   * `ko`: Korean.<br><br>   * `ja`: Japanese. |
|ShowPriority |Integer |`1` |The display priority of translated subtitles. A larger value indicates a higher priority. For example, if the `ShowPriority` of source subtitles is `1` and `ShowPriority` of translated subtitles is `2`, translated subtitles are displayed above source subtitles. |
|MaxCharNumber |Integer |`60` |The maximum number of characters per line for translated subtitles.<br><br>> **说明**<br><br><br><br>* > The system calculates the final maximum number of displayable characters per line based on this parameter, `MarginLr`, `Font`, `FontSize`, screen resolution, and other factors.<br><br><br>* > Each Chinese character, letter, symbol, or digit counts as one character.<br><br><br>* > When `MaxRowNumber` is set to `1` or `2`, if the total number of translated subtitle characters exceeds the display range, the content is truncated. For example, if the maximum number of characters per line is 10 and `MaxRowNumber` is `2`, content after the 20th character is truncated.<br><br><br>* > If `DisplayPreset` is passed, this parameter does not take effect.<br> |
|Hidden |Boolean |`false` |Whether to hide translated subtitles. Valid values:<br><br><br>* `true`: Hides translated subtitles.<br><br>* `false`: Displays translated subtitles. |
|Font |String |`inter` |The translated subtitle font.<br><br><br>* When the value of `Enable` under `SIConfig` is set to `true` and AI Dubbing mode is used, you can call [GetSubtitleTranscodePresetConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSubtitleTranscodePresetConfig) and use `Alias` to get the display name of the font.<br><br>* When the value of `Enable` under `SIConfig` is set to `false` and Subtitle Only mode is used, valid values depend on the translated subtitle language (`Language`).<br><br>   * If the translated subtitle language is `zh`, the following fonts are supported:<br><br>      * `siyuanheiti`: Source Han Sans.<br><br>      * `songtixi`: Songti Light.<br><br>      * `songticu`: Songti Bold.<br><br>      * `heitifan`: Heiti Traditional.<br><br>      * `kaiti`: Kaiti.<br><br>   * If the translated subtitle language is `en`, the following fonts are supported:<br><br>      * `inter`: Inter.<br><br>      * `roboto`: Roboto.<br><br>      * `opposans`: OPPOSans.<br><br>      * `siyuansongti`: Source Han Serif.<br><br>      * `montserrat`: Montserrat.<br><br>   * If the translated subtitle language is `ko` or `ja`, `notosans` (Noto Sans) is supported. |
|FontSize |Integer |`18` |The translated subtitle font size, in px.<br><br>> **说明**<br><br><br>> If `DisplayPreset` is passed, this parameter does not take effect.<br> |
|FontColor |String |`0xFF0000@0.5` |The translated subtitle font color. You can specify the color in one of the following ways:<br><br><br>* Start with `0x` or `#`, followed by a hexadecimal RGB color value, and append opacity with `@`. Opacity supports hexadecimal values such as `0x80` and decimal values such as `0.5`. For example, to specify red (`FF0000`) with 50% opacity, pass `0xFF0000@0x80`, `0xFF0000@0.5`, `#FF0000@0x80`, or `#FF0000@0.5`.<br><br>* Use an FFmpeg color keyword and append opacity with `@`. Opacity supports decimal values such as `0.5`. For example, to specify `0xF0F8FF` with 50% opacity, pass `AliceBlue@0.5`.<br><br><br>> **说明**<br><br><br><br>* > For color definitions and more color keywords, see [FFmpeg color syntax](https://ffmpeg.org/ffmpeg-utils.html#color-syntax).<br><br><br>* > A larger opacity value means less transparency.<br> |
|Border |Object of [Border](https://docs.byteplus.com/en/docs/24/28045#border) |`-` |The font shadow of translated subtitles. |
|Box |Object of [Box](https://docs.byteplus.com/en/docs/24/28045#box) |`-` |The font background of translated subtitles. |

### SIOutput

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Sei |Array of String |`["subtitle"]` |The parameter value `["subtitle"]` means to write subtitles into SEI messages in the live stream.<br><br>> **说明**<br><br><br>> This parameter takes effect only when `Pipe` is set to `si` or `mix`.<br> |
|Callback |Object of [Callback](https://docs.byteplus.com/en/docs/24/28045#callback) |`-` |Callback configuration. |

### Border

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Width |Float |`1.0` |The width, in px. |
|Color |String |`0xFF0000@0.5` |The color. You can specify the color in one of the following ways:<br><br><br>* Start with `0x` or `#`, followed by a hexadecimal RGB color value, and append opacity with `@`. Opacity supports hexadecimal values such as `0x80` and decimal values such as `0.5`. For example, to specify red (`FF0000`) with 50% opacity, pass `0xFF0000@0x80`, `0xFF0000@0.5`, `#FF0000@0x80`, or `#FF0000@0.5`.<br><br>* Use an FFmpeg color keyword and append opacity with `@`. Opacity supports decimal values such as `0.5`. For example, to specify `0xF0F8FF` with 50% opacity, pass `AliceBlue@0.5`.<br><br><br>> **说明**<br><br><br><br>* > For color definitions and more color keywords, see [FFmpeg color syntax](https://ffmpeg.org/ffmpeg-utils.html#color-syntax).<br><br><br>* > A larger opacity value means less transparency.<br> |

### Box

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|W |Float |`2` |The width, in px. |
|Color |String |`0xFF0000@0.5` |The color. You can specify the color in one of the following ways:<br><br><br>* Start with `0x` or `#`, followed by a hexadecimal RGB color value, and append opacity with `@`. Opacity supports hexadecimal values such as `0x80` and decimal values such as `0.5`. For example, to specify red (`FF0000`) with 50% opacity, pass `0xFF0000@0x80`, `0xFF0000@0.5`, `#FF0000@0x80`, or `#FF0000@0.5`.<br><br>* Use an FFmpeg color keyword and append opacity with `@`. Opacity supports decimal values such as `0.5`. For example, to specify `0xF0F8FF` with 50% opacity, pass `AliceBlue@0.5`.<br><br><br>> **说明**<br><br><br><br>* > For color definitions and more color keywords, see [FFmpeg color syntax](https://ffmpeg.org/ffmpeg-utils.html#color-syntax).<br><br><br>* > A larger opacity value means less transparency.<br> |

### Callback

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Url |String |`https://xxx` |The URL used to receive callback messages. For more information about AI Dubbing callback messages, see [AI Dubbing](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-callback-description?lang=en#ai-dubbing). |

## Samples

### Sample request

```json
POST https://open.byteplusapi.com/?Action=ListVhostSubtitleTranscodePreset&Version=2023-01-01
{
    "Vhost": "push.example.com"
}
```

### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListVhostSubtitleTranscodePreset",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "PresetList": [
            {
                "Vhost": "push.example.com",
                "App": "live",
                "Suffixes": [
                    "_hd",
                    "_bd"
                ],
                "TranscodePreset": {
                    "PresetName": "OriginPreset",
                    "Description": "subtitleconfig0001",
                    "SuffixName": "_subtitle",
                    "Delay": 12,
                    "DisplayPreset": "small",
                    "MaxRowNumber": 0,
                    "Position": {
                        "Relative": "bottom",
                        "MarginVertical": 0.5,
                        "MarginHorizontal": 0.2
                    },
                    "SourceLanguage": {
                        "Display": true,
                        "Language": "zh",
                        "Font": "siyuanheiti",
                        "FontSize": 18,
                        "Border": {
                            "Width": 1,
                            "Color": "0xFF0000@0.5"
                        },
                        "FontColor": "0xFF0000@0.5",
                        "Box": {
                            "W": 2,
                            "Color": "0xFF0000@0.5"
                        },
                        "MaxCharNumber": 60,
                        "ShowPriority": 2
                    },
                    "TargetLanguage": [
                        {
                            "Language": "en",
                            "Font": "inter",
                            "FontSize": 18,
                            "FontColor": "0xFF0000@0.5",
                            "Border": {
                                "Width": 1.0,
                                "Color": "0xFF0000@0.5"
                            },
                            "Box": {
                                "W": 1.0,
                                "Color": "0xFF0000@0.5"
                            },
                            "Hidden": false,
                            "MaxCharNumber": 60,
                            "ShowPriority": 1
                        }
                    ],
                    "GlossaryWordList": [
                        "赛事直播:sports live streaming",
                        "实时字幕:real-time subtitles"
                    ],
                    "ReplaceMap": {
                        "live core": "LiveCore",
                        "media life": "MediaLive"
                    },
                    "SIConfig": {
                        "Enable": true,
                        "Pipe": "si",
                        "SpeakerRecognition": 1,
                        "DigitalHumanMouthShape": false,
                        "PipeExtra": "{\"Separator\":{\"HandleType\":1},\"Amix\":{\"AudioEnhance\":false}}"
                    },
                    "SIOutput": {
                        "Sei": [
                            "subtitle"
                        ],
                        "Callback": {
                            "Url": "https://xxx"
                        }
                    }
                }
            }
        ]
    }
}
```

## Error codes

The following are the error codes related to the current operation. For other error codes, see [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes).

|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|200 |CommonErr |\- |Uncategorized error. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/24/28045#request-parameters) description for inspection. |
|400 |InvalidParam.BindError |Request parameter error, please check input data |The parameter failed validation. Please check if the data type is correct. |
|400 |InvalidParam.Empty |%s is required |The parameter is missing. Please check if the parameter specified in the error message is passed in. |
|403 |RequestForbidden |\- |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.AccountIDNotAllow |this AccountID does not have permission to access the corresponding resource, please check the request parameters |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |The video live streaming service has not been enabled or the account is in arrears, resulting in an unavailable bill. Please check the service activation status and account arrears status. |
|404 |ResourceNotFound |\- |The resource (including domain name space, domain name, app name, configuration, and certificate) was not found. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError.Preset |an internal error related to preset occurred, please contact the administrator. |An internal error related to the preset occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |Internal service timed out. Please [contact support](https://console.byteplus.com/workorder/create). |
