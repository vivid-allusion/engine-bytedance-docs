---
title: "CreateSubtitleTranscodePreset"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createsubtitletranscodepreset-2023"
---

Call the `CreateSubtitleTranscodePreset` API to add a subtitle configuration. After the configuration is added, viewers can watch the subtitle effect by pulling a transcoded stream associated with the subtitle configuration, or by pulling the source stream with the subtitle suffix appended. For more information, see [Subtitle configuration](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-manage-subtitle-configuration).

## Usage scenario

Select the appropriate feature based on your scenario.

|Scenario |Recommended feature |Parameter configuration |Description |
|---|---|---|---|
|Provide basic subtitles for a live stream, helping viewers watch in muted or noisy environments. |Original (ASR) subtitles |* Whole\-sentence display: Subtitles are displayed sentence by sentence. Set `Enable` under `SIConfig` to `true`, set `Pipe` to `mix` (subtitles only), and configure only `SourceLanguage` (source subtitles), without configuring `TargetLanguage` (translated subtitles).<br><br>* Live streaming display: Subtitles appear character by character or word by word without waiting for the sentence to finish. Set `Enable` under `SIConfig` to `true`, set `Pipe` to `realtime`, and configure only `SourceLanguage` (source subtitles), without configuring `TargetLanguage` (translated subtitles). |Overlays source subtitles on the video by using speech recognition.<br><br>> **说明**<br><br><br>> Currently, live streaming display only supports Chinese and English subtitles. Whole\-sentence display supports more languages.<br> |
|Enable cross\-language text communication and reach a global audience. |Subtitle translation |* AI Dubbing mode: Set `Enable` under `SIConfig` to `true`, set `Pipe` to `mix` (subtitles only), and configure `SourceLanguage`(source subtitles) and `TargetLanguage` (translated subtitles).<br><br>* Subtitle Only mode: Set `Enable` under `SIConfig` to `false` and configure `SourceLanguage`(source subtitles) and `TargetLanguage` (translated subtitles).<br><br><br>> **说明**<br><br><br>> We recommend AI Dubbing mode for better translation quality.<br> |Overlays translated subtitles on the video by using speech recognition while retaining the original sound. |
|Provide a dubbing\-style translation experience, similar to watching a dubbed film. |Dubbed audio |Set `Enable` under `SIConfig` to `true`, set `Pipe` to `si` (AI Dubbing), set `SpeakerRecognition` to a value greater than `0`, and configure the `Language` fields of `SourceLanguage` (source subtitles) and `TargetLanguage` (translated subtitles). |Provides dubbed audio and replaces the original sound. |
|Provide an immersive human interpreter experience to enhance professionalism. |Dubbed audio + lip sync |Set `Enable` under `SIConfig` to `true`, set `Pipe` to `si` (AI Dubbing), set `SpeakerRecognition` to a value greater than `0`, set `DigitalHumanMouthShape` to `true`, and configure the `Language` fields of `SourceLanguage` (source subtitles) and `TargetLanguage` (translated subtitles). |Based on dubbed audio, AI technology synchronizes the speaker's lip movements with the dubbed audio, creating a highly realistic effect. |

## Requirements

* **Rate limit**: 10 requests per second per account.

* **Billing**:

   * **Subtitle fees**: Billed based on the **actual running duration** of the subtitle task. For more information, see [Subtitle billing](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-billing-subtitle).

   * **Transcoding fees**: If you pull a transcoded stream, transcoding fees are incurred. Transcoding is billed based on the **actual transcoding duration**. For more information, see [Transcoding billing](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-transcoding).

* **Prerequisites**：

   * Make sure that domain names for stream pushing and pulling have been added under the same domain name space. For more information, see [CreateDomain](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-dj3h3u96xn).

   * A transcoding configuration has been added under the domain name space for later association. Make sure that the transcoding configuration and the subtitle configuration to add use the same domain name space and `AppName`. For more information, see [CreateTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/createtranscodepresetv2023).

* **Live latency**: To ensure stable and complete subtitles, an additional **15 to 30 seconds** of live latency is introduced to associated transcoded streams or source streams with the subtitle suffix appended.

* **Activation time**: After you add, edit, or delete a subtitle configuration, you must wait 3 to 5 minutes and restart stream pushing for the change to take effect.

## HTTP request

* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=CreateSubtitleTranscodePreset&Version=2023\-01\-01

## Request parameters

### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

### Query

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`CreateSubtitleTranscodePreset` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |

### Body parameters

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Vhost |String |Yes |`push.example.com` |The domain name space where the domains for stream pushing and pulling belong.<br><br>You can get the domain name space in any of the following ways:<br><br><br>* Call [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023), and get the domain name space by using the response parameter `Vhost`.<br><br>* On the [Domains](https://console.byteplus.com/live/main/domain) page in the MediaLive console, click **Settings** at the right of a specific domain and get the domain name space from the **Domain name space** field. |
|App |String |Yes |`live` |The `AppName` in the push stream address. For example, if the push stream address is `rtmp://push.example.com/live/test?authinfo`, the `AppName` is `live`.<br><br>> **注意**<br><br><br>> Make sure that this value is the same as the `AppName` of the transcoding configuration.<br> |
|Description |String |No |`subtitleconfig0001` |The description of the subtitle configuration. |
|SuffixName |String |Yes |`_subtitle` |The subtitle suffix. You can append this suffix to the source stream address to directly add subtitles, dubbed audio, and other effects to the original live stream without changing the resolution or bitrate.<br><br>To customize the suffix, the suffix must start with a hyphen (\-) or underscore ( *), be 1 to 100 characters in length, and can contain uppercase letters (A\-Z), lowercase letters (a\-z), hyphens (\-), and underscores (* ).<br><br>Example:<br><br><br>* Source stream address: `rtmp://pull.example.com/live/test`<br><br>* Subtitle stream (with subtitles, dubbed audio, and other effects) address: `rtmp://pull.example.com/live/test_subtitle`. |
|Suffixes |Array of String |Yes |`["_hd","_bd"]` |One or more transcoding suffixes under the current `AppName`. These suffixes add subtitles, dubbed audio, and other effects to transcoded streams, so viewers can experience these effects when switching quality levels.<br><br>You can call [ListVhostTransCodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/ListVhostTransCodePreset) and use `SuffixName` to get transcoding suffixes.<br><br>> **注意**<br><br><br>> Each transcoding suffix under an `AppName` can be bound to only one subtitle configuration.<br><br><br>Example:<br><br><br>* Source stream address: `rtmp://pull.example.com/live/test`<br><br>* Transcoded stream (with subtitles, dubbed audio, and other effects) address: `rtmp://pull.example.com/live/test_hd` |
|Delay |Integer |No |`8` |The playback delay, in seconds, used to allow enough time for dubbed audio and subtitle translation. Valid range: `[0,60]`. Recommended values vary by feature:<br><br><br>* `si`:<br><br>   * Lip sync, dubbed audio, and subtitles enabled: `20`.<br><br>   * Dubbed audio and subtitles enabled: `12`.<br><br>* `mix`:<br><br>   * Original (ASR) subtitles in whole\-sentence display: `15`.<br><br>   * Subtitle translation: `8`.<br><br>* `realtime` (Original (ASR) subtitles in live streaming display): `2` or `3`.<br><br>   For detailed feature configuration, see [Usage scenario](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createsubtitletranscodepreset-2023?lang=en#usage-scenario).<br><br><br>> **说明**<br><br><br><br>* > If subtitles appear earlier than the original sound or video, reduce the playback delay to align subtitles with the original sound or video, and vice versa.<br><br><br>* > This parameter takes effect only when `Enable` under `SIConfig` is set to `true`.<br> |
|DisplayPreset |String |No |`small` |Not recommended. The preset effect used for quick configuration.<br><br>After this parameter is passed, the system automatically adapts `Font`, `MaxRowNumber`, `MaxCharNumber`, and `Position`. The `MaxRowNumber`, `MaxCharNumber`, and `Position` parameters no longer take effect. By default, this parameter is empty, which means no preset effect is used. Valid values:<br><br><br>* `small`: Small\-sized subtitles.<br><br>* `medium`: Medium\-sized subtitles.<br><br>* `large`: Large\-sized subtitles. |
|MaxRowNumber |Integer |No |`0` |The maximum number of subtitle lines for each language. Default value: `0`. Valid values:<br><br><br>* `0`: Automatically wraps lines based on the total number of subtitle characters and the maximum number of characters per line to ensure complete display.<br><br>* `1`: Displays up to one line for each language. Content may be truncated.<br><br>* `2`: Displays up to two lines for each language. Content may be truncated.<br><br><br>> **说明**<br><br><br><br>* > If `DisplayPreset` is passed, this parameter is fixed to `0`.<br><br><br>* > This parameter applies separately to source and translated subtitles. Line limits for source and translated subtitles are calculated separately.<br> |
|Position |Object of [Position](https://docs.byteplus.com/en/docs/24/28042#position) |No |`-` |The subtitle position.<br><br>> **说明**<br><br><br>> If `DisplayPreset` is not passed, this parameter is required. If `DisplayPreset` is passed, this parameter does not take effect.<br> |
|SIConfig |Object of [SIConfig](https://docs.byteplus.com/en/docs/24/28042#siconfig) |No |`-` |The AI Dubbing mode configuration. |
|SIOutput |Object of [SIOutput](https://docs.byteplus.com/en/docs/24/28042#sioutput) |No |`-` |Output\-related configuration. |
|SourceLanguage |Object of [SourceLanguage](https://docs.byteplus.com/en/docs/24/28042#sourcelanguage) |Yes |`-` |The source subtitle configuration.<br><br>> **说明**<br><br><br>> When `Enable` under `SIConfig` is set to `true`, the source and target languages must be different.<br> |
|TargetLanguage |Array of [TargetLanguage](https://docs.byteplus.com/en/docs/24/28042#targetlanguage) |No |`-` |The translated subtitle configuration.<br><br>> **说明**<br><br><br><br>* > Currently, you can pass only one translated subtitle language in each request.<br><br><br>* > When `Enable` under `SIConfig` is set to `true`, the source and target languages must be different.<br> |
|HotWordList |Array of String |No |`["MediaLive","LiveCore"]` |The hotword list. This parameter is empty by default.<br><br>Hotwords must match the source language. The total number of characters cannot exceed 30,000.<br><br>Pass hotwords, such as product names and popular phrases, as a reference for the speech recognition model. This helps improve recognition accuracy, **but hotwords may not be recognized accurately every time**. If recognition errors persist after you use hotwords, you can use `ReplaceMap` to configure possible recognition errors and their correct text one by one to forcibly correct Original (ASR) subtitles.<br><br>> **注意**<br><br><br>> This parameter takes effect only for **Original (ASR) subtitles**. For details, see [Usage scenario](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createsubtitletranscodepreset-2023?lang=en#usage-scenario).<br> |
|GlossaryWordList |Array of String |No |`["赛事直播:sports live streaming","实时字幕:real-time subtitles"]` |The glossary. This parameter is empty by default.<br><br>Each array element must be in the format `"original text:translation"`. Example: `["赛事直播:sports live streaming","实时字幕:real-time subtitles"]`. The total number of characters cannot exceed 30,000.<br><br>Pass proprietary vocabulary and expected translations, such as brand names, personal names, product names, or feature names, as a reference for the translation model. This helps improve translation accuracy for proprietary vocabulary, **but the expected translations may not be used every time**. If mistranslations persist after you use the glossary, you can use `ReplaceMap` to configure possible mistranslations and their correct translations one by one to forcibly correct translated subtitles.<br><br>> **注意**<br><br><br><br>* > Original text or translation values cannot contain English commas (,).<br><br><br>* > This parameter takes effect only when `TargetLanguage` is configured and **applies only to translated subtitles**.<br> |
|ReplaceMap |JSON Map |No |`{"live core":"LiveCore","media life":"MediaLive"}` |The correction list. This parameter is empty by default.<br><br>Configure subtitle text that needs to be forcibly corrected. Add possible mistranslations or recognition errors and their correct text one by one.<br><br>The format is `"incorrect text":"correct text"`. Separate multiple corrections with English commas (,). Each incorrect text or correct text value must be 1 to 50 characters in length. You can pass up to 60 corrections.<br><br>When the system matches the incorrect text, it forcibly replaces the incorrect text with the correct text.<br><br><br>* **Original (ASR) subtitles**: Correct recognition errors. For example, if **MediaLive** is incorrectly recognized as **media life**, you can pass `{"media life":"MediaLive"}`.<br><br>* **Translated subtitles**: Correct mistranslations. **Corrections modify only translated subtitles and do not modify source subtitles or dubbed audio**. For example, if **LiveCore** is mistranslated as **live core**, you can pass `{"live core":"LiveCore"}`.<br><br><br>> **注意**<br><br><br><br>* > Incorrect text and correct text values cannot contain English commas (,).<br><br><br>* > `ReplaceMap` matches text only and does not determine the context. Use this parameter only when the incorrect text can be clearly identified as incorrect. Do not replace incorrect text with text that contains the incorrect text. For example, if you pass `{"stream":"live stream"}`, and the subtitle already correctly displays **live stream**, the system still replaces **stream** with **live stream**, resulting in **live live stream**.<br> |

### Position

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Relative |String |No |`top` |The subtitle position in the video. Default value: `bottom`. Valid values:<br><br><br>* `top`: Displays subtitles at the top of the video.<br><br>* `bottom`: Displays subtitles at the bottom of the video. |
|MarginVertical |Float |No |`0.5` |The top or bottom margin of the subtitles, that is, the distance from subtitles to the top or bottom edge of the video. The value is a percentage of the video height. Valid range: `(0, 0.5]`.<br><br><br>* When `Relative` is set to `top`, this parameter specifies the top margin.<br><br>* When `Relative` is set to `bottom`, this parameter specifies the bottom margin. |
|MarginHorizontal |Float |No |`0.2` |The left and right margins of the subtitles, that is, the distance from subtitles to the left and right edges of the video. The value is a percentage of the video width. Valid range: `(0, 0.3]`. |

### SIConfig

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Enable |Boolean |No |`false` |Whether to enable AI Dubbing mode. Default value: `false`. Valid values:<br><br><br>* `true`: Enables AI Dubbing mode. This mode supports subtitles, dubbed audio that replaces the original sound, and lip sync for an immersive experience.<br><br>* `false`: Disables AI Dubbing mode and enables Subtitle Only mode. After the AI Dubbing mode is disabled, other parameters in `SIConfig` do not take effect. |
|Pipe |String |No |`mix` |The AI Dubbing type. Valid values:<br><br><br>* `si`: Subtitles, dubbed audio, and video are fully synchronized. Lip sync is supported. This mode is suitable for conference live streams and other scenarios that require strong synchronization and immersion.<br><br>* `mix`: Subtitles only, including original (ASR) subtitles in whole\-sentence display.<br><br>* `realtime`: Original (ASR) subtitles in live streaming display. |
|DigitalHumanMouthShape |Boolean |No |`false` |Whether to enable lip sync. Default value: `false`. Valid values:<br><br><br>* `true`: Enables lip sync. After this feature is enabled, the speaker's lip movements are synchronized with the dubbed audio, making the live stream more immersive.<br><br>* `false`: Disables lip sync.<br><br><br>> **说明**<br><br><br><br>* > This parameter takes effect only when `Pipe` is empty or set to `si`.<br><br><br>* > When this parameter is set to `true`, dubbed audio is enabled by default.<br> |
|SpeakerRecognition |Integer |No |`1` |Whether to enable dubbed audio. This parameter is empty by default. Valid values:<br><br><br>* A value greater than `0`: Enables dubbed audio. After this feature is enabled, translated speech with voice cloning is provided to replace the original sound.<br><br>* `0`: Disables dubbed audio.<br><br><br>> **说明**<br><br><br>> This parameter takes effect only when `Pipe` is empty or set to `si`.<br> |
|PipeExtra |String |No |`{"Separator":{"HandleType":1},"Amix":{"AudioEnhance":false}}` |Extra configuration in JSON string format, including volume balance, noise reduction, and original sound volume. For more information, see the `Extra` parameter of [CreateSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/CreateSpeechTask).<br><br>> **说明**<br><br><br>> We recommend passing this parameter only when dubbed audio is enabled. For details about dubbed audio configuration, see [Usage scenario](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createsubtitletranscodepreset-2023?lang=en#usage-scenario).<br> |

### SIOutput

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Sei |Array of String |No |`["subtitle"]` |To write subtitles into SEI messages in the live stream, set this parameter to `["subtitle"]`.<br><br>> **说明**<br><br><br><br>* > This parameter takes effect only when `Pipe` is set to `si` or `mix`.<br><br><br>* > MediaLive uses `100` as the SEI `type` value when writing subtitles into SEI messages. If your stream pushing tool or app also writes custom SEI messages into the stream, avoid using the same SEI `type` value. Otherwise, the player may identify the custom data as subtitles.<br> |
|Callback |Object of [Callback](https://docs.byteplus.com/en/docs/24/28042#callback) |No |`-` |Callback configuration. |

### SourceLanguage

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Display |Boolean |Yes |`true` |Whether to display source subtitles. Valid values:<br><br><br>* `true`: Display. Both the source and translated subtitles will be displayed.<br><br>* `false`: Do not display. Only the translated subtitles will be displayed. |
|Language |String |No |`zh` |The source subtitle language.<br><br><br>* When the value of `Enable` under `SIConfig` is set to `true` and AI Dubbing mode is used, call [GetSubtitleTranscodePresetConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSubtitleTranscodePresetConfig) and use `OriginalLang` to get the list of languages available to the current account for subtitle translation and dubbed audio, or use `AsrLang` to get the list of languages available to the current account for Original (ASR) subtitles, and then pass the `Key` value.<br><br>* When the value of `Enable` under `SIConfig` is set to `false` and Subtitle Only mode is used, valid values are as follows:<br><br>   * `zh`: Mix of Chinese and English.<br><br>   * `en`: English.<br><br>   * `ko`: Korean.<br><br>   * `ja`: Japanese. |
|ShowPriority |Integer |No |`2` |The display priority of source subtitles. By default, source subtitles are displayed above translated subtitles. A larger value indicates a higher priority. For example, if the `ShowPriority` of source subtitles is `1` and `ShowPriority` of translated subtitles is `2`, translated subtitles are displayed above source subtitles. |
|MaxCharNumber |Integer |No |`60` |The maximum number of characters per line for source subtitles. Default value: `60`. Recommended value: `60`.<br><br>> **说明**<br><br><br><br>* > The system calculates the final maximum number of displayable characters per line based on this parameter, `MarginLr`, `Font`, `FontSize`, screen resolution, and other factors.<br><br><br>* > Each Chinese character, letter, symbol, or digit counts as one character.<br><br><br>* > When `MaxRowNumber` is set to `1` or `2`, if the total number of source subtitle characters exceeds the display range, the content is truncated. For example, if the maximum number of characters per line is 10 and `MaxRowNumber` is `2`, content after the 20th character is truncated.<br><br><br>* > If `DisplayPreset` is not passed, this parameter is required. If `DisplayPreset` is passed, this parameter does not take effect.<br> |
|Font |String |Yes |`siyuanheiti` |The source subtitle font.<br><br><br>* When the value of `Enable` under `SIConfig` is set to `true` and AI Dubbing mode is used, call [GetSubtitleTranscodePresetConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSubtitleTranscodePresetConfig) and use `Font` to get the list of fonts available to the current account, and then pass the `Key` value.<br><br>* When the value of `Enable` under `SIConfig` is set to `false` and Subtitle Only mode is used, valid values depend on the source subtitle language (`Language`).<br><br>   * If the source subtitle language is `zh`, the following fonts are supported:<br><br>      * `siyuanheiti`: Source Han Sans.<br><br>      * `songtixi`: Songti Light.<br><br>      * `songticu`: Songti Bold.<br><br>      * `heitifan`: Heiti Traditional.<br><br>      * `kaiti`: Kaiti.<br><br>   * If the source subtitle language is `en`, the following fonts are supported:<br><br>      * `inter`: Inter.<br><br>      * `roboto`: Roboto.<br><br>      * `opposans`: OPPOSans.<br><br>      * `siyuansongti`: Source Han Serif.<br><br>      * `montserrat`: Montserrat.<br><br>   * If the source subtitle language is `ko` or `ja`, `notosans` (Noto Sans) is supported. |
|FontSize |Integer |No |`18` |The source subtitle font size, in px.<br><br>> **说明**<br><br><br>> If `DisplayPreset` is not passed, this parameter is required. If `DisplayPreset` is passed, this parameter does not take effect.<br> |
|FontColor |String |No |`0xFF0000@0.5` |The source subtitle font color. You can specify the color in one of the following ways:<br><br><br>* Start with `0x` or `#`, followed by a hexadecimal RGB color value, and append opacity with `@`. Opacity supports hexadecimal values such as `0x80` and decimal values such as `0.5`. For example, to specify red (`FF0000`) with 50% opacity, pass `0xFF0000@0x80`, `0xFF0000@0.5`, `#FF0000@0x80`, or `#FF0000@0.5`.<br><br>* Use an FFmpeg color keyword and append opacity with `@`. Opacity supports decimal values such as `0.5`. For example, to specify `0xF0F8FF` with 50% opacity, pass `AliceBlue@0.5`.<br><br><br>> **说明**<br><br><br><br>* > For color definitions and more color keywords, see [FFmpeg color syntax](https://ffmpeg.org/ffmpeg-utils.html#color-syntax).<br><br><br>* > A larger opacity value means less transparency.<br><br><br>* > When opacity is specified as a decimal, the valid range is `[0,1]`, with up to two decimal places supported.<br> |
|Box |Object of [Box](https://docs.byteplus.com/en/docs/24/28042#box) |No |`-` |The font background of source subtitles. |
|Border |Object of [Border](https://docs.byteplus.com/en/docs/24/28042#border) |No |`-` |The font shadow of source subtitles. |

### TargetLanguage

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Language |String |No |`en` |The translated subtitle language.<br><br><br>* When the value of `Enable` under `SIConfig` is set to `true` and AI Dubbing mode is used, call [GetSubtitleTranscodePresetConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSubtitleTranscodePresetConfig) and use `Lang` to get the list of languages available to the current account, and then pass the `Key` value.<br><br>* When the value of `Enable` under `SIConfig` is set to `false` and Subtitle Only mode is used, valid values are as follows:<br><br>   * `zh`: Mix of Chinese and English.<br><br>   * `en`: English.<br><br>   * `ko`: Korean.<br><br>   * `ja`: Japanese. |
|ShowPriority |Integer |No |`1` |The display priority of translated subtitles. By default, source subtitles are displayed above translated subtitles. A larger value indicates a higher priority. For example, if the `ShowPriority` of source subtitles is `1` and `ShowPriority` of translated subtitles is `2`, translated subtitles are displayed above source subtitles. |
|MaxCharNumber |Integer |No |`60` |The maximum number of characters per line for translated subtitles. Default value: `60`. Recommended value: `60`.<br><br>> **说明**<br><br><br><br>* > The system calculates the final maximum number of displayable characters per line based on this parameter, `MarginLr`, `Font`, `FontSize`, screen resolution, and other factors.<br><br><br>* > Each Chinese character, letter, symbol, or digit counts as one character.<br><br><br>* > When `MaxRowNumber` is set to `1` or `2`, if the total number of translated subtitle characters exceeds the display range, the content is truncated. For example, if the maximum number of characters per line is 10 and `MaxRowNumber` is `2`, content after the 20th character is truncated.<br><br><br>* > If `DisplayPreset` is not passed, this parameter is required. If `DisplayPreset` is passed, this parameter does not take effect.<br> |
|Hidden |Boolean |No |`false` |Whether to hide translated subtitles. Default value: `false`. Valid values:<br><br><br>* `true`: Hides translated subtitles.<br><br>* `false`: Displays translated subtitles. |
|Font |String |Yes |`inter` |The translated subtitle font.<br><br><br>* When the value of `Enable` under `SIConfig` is set to `true` and AI Dubbing mode is used, call [GetSubtitleTranscodePresetConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSubtitleTranscodePresetConfig) and use `Font` to get the list of fonts available to the current account, and then pass the `Key` value.<br><br>* When the value of `Enable` under `SIConfig` is set to `false` and Subtitle Only mode is used, valid values depend on the translated subtitle language (`Language`).<br><br>   * If the translated subtitle language is `zh`, the following fonts are supported:<br><br>      * `siyuanheiti`: Source Han Sans.<br><br>      * `songtixi`: Songti Light.<br><br>      * `songticu`: Songti Bold.<br><br>      * `heitifan`: Heiti Traditional.<br><br>      * `kaiti`: Kaiti.<br><br>   * If the translated subtitle language is `en`, the following fonts are supported:<br><br>      * `inter`: Inter.<br><br>      * `roboto`: Roboto.<br><br>      * `opposans`: OPPOSans.<br><br>      * `siyuansongti`: Source Han Serif.<br><br>      * `montserrat`: Montserrat.<br><br>   * If the translated subtitle language is `ko` or `ja`, `notosans` (Noto Sans) is supported. |
|FontSize |Integer |No |`18` |The translated subtitle font size, in px.<br><br>> **说明**<br><br><br>> If `DisplayPreset` is not passed, this parameter is required. If `DisplayPreset` is passed, this parameter does not take effect.<br> |
|FontColor |String |Yes |`0xFF0000@0.5` |The translated subtitle font color. You can specify the color in one of the following ways:<br><br><br>* Start with `0x` or `#`, followed by a hexadecimal RGB color value, and append opacity with `@`. Opacity supports hexadecimal values such as `0x80` and decimal values such as `0.5`. For example, to specify red (`FF0000`) with 50% opacity, pass `0xFF0000@0x80`, `0xFF0000@0.5`, `#FF0000@0x80`, or `#FF0000@0.5`.<br><br>* Use an FFmpeg color keyword and append opacity with `@`. Opacity supports decimal values such as `0.5`. For example, to specify `0xF0F8FF` with 50% opacity, pass `AliceBlue@0.5`.<br><br><br>> **说明**<br><br><br><br>* > For color definitions and more color keywords, see [FFmpeg color syntax](https://ffmpeg.org/ffmpeg-utils.html#color-syntax).<br><br><br>* > A larger opacity value means less transparency.<br><br><br>* > When opacity is specified as a decimal, the valid range is `[0,1]`, with up to two decimal places supported.<br> |
|Border |Object of [Border](https://docs.byteplus.com/en/docs/24/28042#border) |No |`-` |The font shadow of translated subtitles. |
|Box |Object of [Box](https://docs.byteplus.com/en/docs/24/28042#box) |No |`-` |The font background of translated subtitles. |

### Callback

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Url |String |Yes |`https://xxx` |The URL used to receive callback messages. The URL must start with `http://` or `https://`, be publicly accessible, and contain 1\-100 characters. For more information about AI Dubbing callback messages, see [AI Dubbing](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-callback-description?lang=en#ai-dubbing). |

### Box

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|W |Float |Yes |`2` |The width, in px. Recommended range: `[1,10]`. |
|Color |String |Yes |`0xFF0000@0.5` |The color. You can specify the color in one of the following ways:<br><br><br>* Start with `0x` or `#`, followed by a hexadecimal RGB color value, and append opacity with `@`. Opacity supports hexadecimal values such as `0x80` and decimal values such as `0.5`. For example, to specify red (`FF0000`) with 50% opacity, pass `0xFF0000@0x80`, `0xFF0000@0.5`, `#FF0000@0x80`, or `#FF0000@0.5`.<br><br>* Use an FFmpeg color keyword and append opacity with `@`. Opacity supports decimal values such as `0.5`. For example, to specify `0xF0F8FF` with 50% opacity, pass `AliceBlue@0.5`.<br><br><br>> **说明**<br><br><br><br>* > For color definitions and more color keywords, see [FFmpeg color syntax](https://ffmpeg.org/ffmpeg-utils.html#color-syntax).<br><br><br>* > A larger opacity value means less transparency.<br><br><br>* > When opacity is specified as a decimal, the valid range is `[0,1]`, with up to two decimal places supported.<br> |

### Border

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Width |Float |Yes |`2` |The width, in px. Recommended range: `[1,10]`. |
|Color |String |Yes |`0xFF0000@0.5` |The color. You can specify the color in one of the following ways:<br><br><br>* Start with `0x` or `#`, followed by a hexadecimal RGB color value, and append opacity with `@`. Opacity supports hexadecimal values such as `0x80` and decimal values such as `0.5`. For example, to specify red (`FF0000`) with 50% opacity, pass `0xFF0000@0x80`, `0xFF0000@0.5`, `#FF0000@0x80`, or `#FF0000@0.5`.<br><br>* Use an FFmpeg color keyword and append opacity with `@`. Opacity supports decimal values such as `0.5`. For example, to specify `0xF0F8FF` with 50% opacity, pass `AliceBlue@0.5`.<br><br><br>> **说明**<br><br><br><br>* > For color definitions and more color keywords, see [FFmpeg color syntax](https://ffmpeg.org/ffmpeg-utils.html#color-syntax).<br><br><br>* > A larger opacity value means less transparency.<br><br><br>* > When opacity is specified as a decimal, the valid range is `[0,1]`, with up to two decimal places supported.<br> |

## Response parameters

This API only returns [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/request-response) in the response.

## Samples

### Sample request

**Original (ASR) subtitles (whole\-sentence display)**

```json
POST https://open.byteplusapi.com/?Action=CreateSubtitleTranscodePreset&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "App": "live",
    "Description": "Original ASR subtitles - whole-sentence display",
    "SuffixName": "_asr",
    "Suffixes": [
        "_hd",
        "_bd"
    ],
    "Delay": 15,
    "MaxRowNumber": 2,
    "Position": {
        "Relative": "bottom",
        "MarginVertical": 0.05,
        "MarginHorizontal": 0.2
    },
    "SourceLanguage": {
        "Display": true,
        "Language": "en",
        "Font": "inter",
        "FontSize": 18,
        "FontColor": "0xFFFFFF@1",
        "Border": {
            "Width": 2,
            "Color": "0x000000@0.5"
        },
        "Box": {
            "W": 1,
            "Color": "0x000000@0.5"
        },
        "MaxCharNumber": 60,
        "ShowPriority": 2
    },
    "HotWordList": [
        "MediaLive",
        "LiveCore"
    ],
    "SIConfig": {
        "Enable": true,
        "Pipe": "mix"
    },
    "SIOutput": {
        "Sei": [
            "subtitle"
        ],
        "Callback": {
            "Url": "https://example.com/callback"
        }
    },
    "ReplaceMap": {
        "media life": "MediaLive"
    }
}
```

**Original (ASR) subtitles (live streaming display)**

```json
POST https://open.byteplusapi.com/?Action=CreateSubtitleTranscodePreset&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "App": "live",
    "Description": "Original ASR subtitles - live streaming display",
    "SuffixName": "_asr_realtime",
    "Suffixes": [
        "_hd",
        "_bd"
    ],
    "Delay": 2,
    "MaxRowNumber": 2,
    "Position": {
        "Relative": "bottom",
        "MarginVertical": 0.05,
        "MarginHorizontal": 0.2
    },
    "SourceLanguage": {
        "Display": true,
        "Language": "en",
        "Font": "inter",
        "FontSize": 18,
        "FontColor": "0xFFFFFF@1",
        "Border": {
            "Width": 2,
            "Color": "0x000000@0.5"
        },
        "Box": {
            "W": 1,
            "Color": "0x000000@0.5"
        },
        "MaxCharNumber": 60,
        "ShowPriority": 2
    },
    "HotWordList": [
        "MediaLive",
        "LiveCore"
    ],
    "SIConfig": {
        "Enable": true,
        "Pipe": "realtime"
    },
    "SIOutput": {
        "Callback": {
            "Url": "https://example.com/callback"
        }
    },
    "ReplaceMap": {
        "media life": "MediaLive"
    }
}
```

**Subtitle translation**

```json
POST https://open.byteplusapi.com/?Action=CreateSubtitleTranscodePreset&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "App": "live",
    "Description": "Subtitle translation",
    "SuffixName": "_translate",
    "Suffixes": [
        "_hd",
        "_bd"
    ],
    "Delay": 8,
    "MaxRowNumber": 2,
    "Position": {
        "Relative": "bottom",
        "MarginVertical": 0.05,
        "MarginHorizontal": 0.2
    },
    "SourceLanguage": {
        "Display": true,
        "Language": "zh",
        "Font": "siyuanheiti",
        "FontSize": 18,
        "FontColor": "0xFFFFFF@1",
        "Border": {
            "Width": 2,
            "Color": "0x000000@0.5"
        },
        "Box": {
            "W": 1,
            "Color": "0x000000@0.5"
        },
        "MaxCharNumber": 60,
        "ShowPriority": 2
    },
    "TargetLanguage": [
        {
            "Language": "en",
            "Font": "inter",
            "FontSize": 18,
            "FontColor": "0xFFFFFF@1",
            "Hidden": false,
            "Border": {
                "Width": 2,
                "Color": "0x000000@0.5"
            },
            "Box": {
                "W": 1.0,
                "Color": "0x000000@0.5"
            },
            "MaxCharNumber": 60,
            "ShowPriority": 1
        }
    ],
    "GlossaryWordList": [
        "赛事直播:sports live streaming",
        "实时字幕:real-time subtitles"
    ],
    "SIConfig": {
        "Enable": true,
        "Pipe": "mix"
    },
    "SIOutput": {
        "Sei": [
            "subtitle"
        ],
        "Callback": {
            "Url": "https://example.com/callback"
        }
    },
    "ReplaceMap": {
        "live core": "LiveCore"
    }
}
```

**Dubbed audio + translated subtitles**

```json
POST https://open.byteplusapi.com/?Action=CreateSubtitleTranscodePreset&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "App": "live",
    "Description": "Dubbed audio + translated subtitles",
    "SuffixName": "_voice",
    "Suffixes": [
        "_hd",
        "_bd"
    ],
    "Delay": 12,
    "MaxRowNumber": 2,
    "Position": {
        "Relative": "bottom",
        "MarginVertical": 0.05,
        "MarginHorizontal": 0.2
    },
    "SourceLanguage": {
        "Display": false,
        "Language": "zh",
        "Font": "siyuanheiti",
        "FontSize": 18,
        "FontColor": "0xFFFFFF@1",
        "Border": {
            "Width": 2,
            "Color": "0x000000@0.5"
        },
        "Box": {
            "W": 1,
            "Color": "0x000000@0.5"
        },
        "MaxCharNumber": 60,
        "ShowPriority": 2
    },
    "TargetLanguage": [
        {
            "Language": "en",
            "Font": "inter",
            "FontSize": 18,
            "FontColor": "0xFFFFFF@1",
            "Hidden": false,
            "Border": {
                "Width": 2,
                "Color": "0x000000@0.5"
            },
            "Box": {
                "W": 1.0,
                "Color": "0x000000@0.5"
            },
            "MaxCharNumber": 60,
            "ShowPriority": 1
        }
    ],
    "GlossaryWordList": [
        "赛事直播:sports live streaming",
        "实时字幕:real-time subtitles"
    ],
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
            "Url": "https://example.com/callback"
        }
    },
    "ReplaceMap": {
        "live core": "LiveCore"
    }
}
```

**Dubbed audio + lip sync + translated subtitles**

```json
POST https://open.byteplusapi.com/?Action=CreateSubtitleTranscodePreset&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "App": "live",
    "Description": "Dubbed audio + lip sync + translated subtitles",
    "SuffixName": "_lipsync",
    "Suffixes": [
        "_hd",
        "_bd"
    ],
    "Delay": 20,
    "MaxRowNumber": 2,
    "Position": {
        "Relative": "bottom",
        "MarginVertical": 0.05,
        "MarginHorizontal": 0.2
    },
    "SourceLanguage": {
        "Display": false,
        "Language": "zh",
        "Font": "siyuanheiti",
        "FontSize": 18,
        "FontColor": "0xFFFFFF@1",
        "Border": {
            "Width": 2,
            "Color": "0x000000@0.5"
        },
        "Box": {
            "W": 1,
            "Color": "0x000000@0.5"
        },
        "MaxCharNumber": 60,
        "ShowPriority": 2
    },
    "TargetLanguage": [
        {
            "Language": "en",
            "Font": "inter",
            "FontSize": 18,
            "FontColor": "0xFFFFFF@1",
            "Hidden": false,
            "Border": {
                "Width": 2,
                "Color": "0x000000@0.5"
            },
            "Box": {
                "W": 1.0,
                "Color": "0x000000@0.5"
            },
            "MaxCharNumber": 60,
            "ShowPriority": 1
        }
    ],
    "GlossaryWordList": [
        "赛事直播:sports live streaming",
        "实时字幕:real-time subtitles"
    ],
    "SIConfig": {
        "Enable": true,
        "Pipe": "si",
        "SpeakerRecognition": 1,
        "DigitalHumanMouthShape": true,
        "PipeExtra": "{\"Separator\":{\"HandleType\":1},\"Amix\":{\"AudioEnhance\":false}}"
    },
    "SIOutput": {
        "Sei": [
            "subtitle"
        ],
        "Callback": {
            "Url": "https://example.com/callback"
        }
    },
    "ReplaceMap": {
        "live core": "LiveCore"
    }
}
```

### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateSubtitleTranscodePreset",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```

## Error codes

The following are the error codes related to the current operation. For other error codes, see [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes).

|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|200 |CommonErr |\- |Uncategorized error. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createsubtitletranscodepreset-2023#request-parameters) description for inspection. |
|400 |InvalidParam.BindError |Request parameter error, please check input data |The parameter failed validation. Please check if the data type is correct. |
|403 |RequestForbidden |\- |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.AccountIDNotAllow |this AccountID does not have permission to access the corresponding resource, please check the request parameters |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |The video live streaming service has not been enabled or the account is in arrears, resulting in an unavailable bill. Please check the service activation status and account arrears status. |
|404 |ResourceNotFound |\- |The resource (including domain name space, domain name, app name, configuration, and certificate) was not found. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError.Preset |an internal error related to preset occurred, please contact the administrator. |An internal error related to the preset occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |Internal service timed out. Please [contact support](https://console.byteplus.com/workorder/create). |
