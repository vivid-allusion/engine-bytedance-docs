---
title: "CreateSpeechTask"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/CreateSpeechTask"
---

Call the `CreateSpeechTask` API to create an AI Dubbing task. After the task is created, when you start pushing a stream during the relay time period from `StartTime` to `EndTime`, the task automatically pulls the live stream for AI Dubbing processing and pushes the processed live stream to the specific push stream address. For example, you can start a live stream with OBS, process the live stream through an AI Dubbing task, and then stream the processed content on TikTok. For more information, see [AI Dubbing](https://docs.byteplus.com/en/docs/byteplus-media-live/ai-liveinterpret-simultaneous-audio-and-video-interpretation).

## Usage scenario

Select the appropriate feature based on your scenario.

|Scenario |Recommended feature |Parameter configuration |Description |
|---|---|---|---|
|Provide basic subtitles for a live stream, helping viewers watch in muted or noisy environments. |Original (ASR) subtitles |* Whole\-sentence display: Subtitles are displayed sentence by sentence. Set `Pipe` to `mix` (subtitles only) and configure only `Original` (source subtitles), without configuring `Translation` (translated subtitles).<br><br>* Live streaming display: Subtitles appear character by character or word by word without waiting for the sentence to finish. Set `Pipe` to `realtime` (real\-time interpretation mode) and configure only `Original` (source subtitles), without configuring `Translation` (translated subtitles). |Overlays source subtitles on the video by using speech recognition.<br><br>> **说明**<br><br><br>> Currently, live streaming display only supports Chinese and English subtitles. Whole\-sentence display supports more languages.<br> |
|Enable cross\-language text communication and reach a global audience. |Subtitle translation |Set `Pipe` to `mix` (subtitles only) or `realtime` (real\-time interpretation mode), and configure both `Original` (source subtitles) and `Translation` (translated subtitles). |Overlays translated subtitles on the video by using speech recognition while retaining the original sound. |
|Provide a dubbing\-style translation experience, similar to watching a dubbed film. |Dubbed audio |Set `Pipe` to `realtime` (real\-time interpretation mode) and `VoiceShow` to `true`, or set `Pipe` to `si` (AI Dubbing mode), and configure the `Language` fields of `Original` (source subtitles) and `Translation` (translated subtitles). |Provides dubbed audio and replaces the original sound. In real\-time interpretation mode, you can choose to overlay the dubbed audio on the original sound or directly replace the original sound. |
|Provide an immersive human interpreter experience to enhance professionalism. |Dubbed audio + lip sync |Set `Pipe` to `si` (AI Dubbing mode), set `LipSync` to `true`, and configure the `Language` fields of `Original` (source subtitles) and `Translation` (translated subtitles). |Based on dubbed audio, AI technology synchronizes the speaker's lip movements with the dubbed audio, creating a highly realistic effect. |

## Requirements

* **Rate limit**: 10 requests per second per account.

* **Billing**: Only AI Dubbing fees are charged. AI Dubbing is billed based on the **actual stream push duration** of the task. For more information, see [AI Dubbing billing](https://docs.byteplus.com/en/docs/byteplus-media-live/ai_dubbing).

* **Concurrency limit**: Each account can run up to 2 tasks at the same time. To run more tasks at the same time, [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) to contact technical support.

* **Prerequisites**

   * Make sure that domain names for stream pushing and pulling have been added under the same domain name space. For more information, see [CreateDomain](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-dj3h3u96xn).

      > **注意**

      > This prerequisite is required only when you use MediaLive push and pull stream addresses.

   * Prepare the **Pull Stream URL** and **Push Stream URL**.

      * **Pull Stream URL**: Obtain a valid pull stream address for pulling the original live stream. RTMP and FLV formats are supported.

         If you use a MediaLive pull stream address as the **Pull Stream URL**, use the same `AppName` and `StreamName` and generate a pair of addresses by using [GeneratePushURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generatepushurl-2023) and [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023). This pair includes the pull stream address used as the **Pull Stream URL** and the push stream address used to push the original live stream.

      * **Push Stream URL**: Used to push the processed live stream. RTMP format is supported.

         * If you use a MediaLive push stream address as the **Push Stream URL**, use the same `AppName` and `StreamName` and generate a pair of addresses by using [GeneratePushURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generatepushurl-2023) and [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023). This pair includes the push stream address used as the **Push Stream URL** and the pull stream address used to pull the processed live stream.

         * If you use a push stream address from another cloud provider or a live platform such as TikTok as the **Push Stream URL**, see the official documentation of the corresponding platform or contact the platform's customer service to obtain a valid push stream address.

   > **说明**

   > The push stream address used to push the original live stream and the pull stream address used to pull the processed live stream are not restricted to a specific protocol. Select a protocol based on your actual needs.

## HTTP request

* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=CreateSpeechTask&Version=2023\-01\-01

## Request parameters

### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

### Query

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`CreateSpeechTask` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |

### Body parameters

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Name |String |Yes |`TaskA` |The task name. The name must be unique among all running tasks. The name must be 1 to 20 characters in length and can contain digits (0\-9), uppercase letters (A\-Z), lowercase letters (a\-z), Chinese characters, underscores (_), and hyphens (\-). |
|Rule |Object of [Rule](https://docs.byteplus.com/en/docs/24/117618#rule) |Yes |`-` |The task rule. |

### Rule

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Pipe |String |Yes |`si` |The task type. Valid values:<br><br><br>* `si`: AI Dubbing mode. Subtitles, dubbed audio, and video are fully synchronized. Lip sync is supported. This mode is suitable for conference live streams and other scenarios that require strong synchronization and immersion. This mode introduces some latency.<br><br>* `mix`: Subtitles only, including original (ASR) subtitles in whole\-sentence display.<br><br>* `realtime`: Real\-time interpretation mode, including original (ASR) subtitles in live streaming display.. This mode has low latency, but video may not be synchronized with subtitles or dubbed audio. This mode is suitable for latency\-sensitive scenarios such as sports live streams.<br><br><br>> **说明**<br><br><br>> When this parameter is set to `si`, dubbed audio is enabled by default and cannot be disabled.<br> |
|Delay |Integer |No |`20` |The playback delay, in seconds, used to allow enough time for dubbed audio and subtitle translation. Valid range: `[0,60]`. Recommended values vary by task type (`Pipe`) and feature:<br><br><br>* `si`:<br><br>   * Lip sync, dubbed audio, and subtitles enabled: `20`.<br><br>   * Dubbed audio and subtitles enabled: `12`.<br><br>* `mix`:<br><br>   * Original (ASR) subtitles in whole\-sentence display: `15`.<br><br>   * Subtitle translation: `8`.<br><br>* `realtime`: `2` or `3`.<br><br><br>For detailed feature configuration, see [Usage scenario](https://docs.byteplus.com/en/docs/byteplus-media-live/CreateSpeechTask?lang=en#usage-scenario).<br><br>> **说明**<br><br><br>> If subtitles appear earlier than the original sound or video, reduce the playback delay to align subtitles with the original sound or video, and vice versa.<br> |
|Source |Object of [Source](https://docs.byteplus.com/en/docs/24/117618#source) |Yes |`-` |The source stream configuration. |
|StartTime |String |No |`2025-11-17T11:30:06+08:00` |The task start time. The time is in RFC3339 format, uses UTC+8, and is accurate to seconds. If this parameter is not passed, the task starts immediately. |
|EndTime |String |No |`2025-11-17T12:11:06+08:00` |The task end time. The end time must be later than `StartTime`, and the time span between `StartTime` and `EndTime` cannot exceed 7 days. The time is in RFC3339 format, uses UTC+8, and is accurate to seconds. If this parameter is not passed, the task ends 7 days after the start time.<br><br>> **说明**<br><br><br>> When the task ends, the source stream disconnects, or stream pulling fails, relay stops automatically.<br> |
|Output |Object of [Output](https://docs.byteplus.com/en/docs/24/117618#output) |Yes |`-` |The push stream configuration. |
|SI |Object of [SI](https://docs.byteplus.com/en/docs/24/117618#si) |No |`-` |AI Dubbing mode configuration.<br><br>> **说明**<br><br><br>> This parameter takes effect only when `Pipe` is set to `si`.<br> |
|RealTime |Object of [RealTime](https://docs.byteplus.com/en/docs/24/117618#realtime) |No |`-` |Real\-time interpretation mode configuration.<br><br>> **说明**<br><br><br>> This parameter takes effect only when `Pipe` is set to `realtime`.<br> |
|Extra |Object of [Extra](https://docs.byteplus.com/en/docs/24/117618#extra) |No |`-` |Extra configuration.<br><br>> **说明**<br><br><br>> We recommend passing this parameter only when dubbed audio is enabled. For details about dubbed audio configuration, see [Usage scenario](https://docs.byteplus.com/en/docs/byteplus-media-live/CreateSpeechTask?lang=en#usage-scenario).<br> |
|Subtitle |Object of [Subtitle](https://docs.byteplus.com/en/docs/24/117618#subtitle) |No |`-` |The subtitle configuration. |

### Source

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Url |String |Yes |`https://xxx/live/xxx.flv` |The **Pull Stream URL**. RTMP and FLV formats are supported. The task pulls the original live stream from this URL and processes the stream.<br><br>> **说明**<br><br><br>> The URL cannot directly contain multibyte characters, such as Chinese characters. If such characters are needed, URL\-encode them.<br> |

### Output

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Url |Array of String |Yes |`["rtmp://push.example.com/live/test01","rtmp://push.example.com/live/test02"]` |The **Push Stream URL**. RTMP format is supported. The task pushes the processed live stream to this URL.<br><br>You can pass up to 8 push stream URLs.<br><br>> **说明**<br><br><br><br>* > The URL cannot directly contain multibyte characters, such as Chinese characters. If such characters are needed, URL\-encode them.<br><br><br>* > To play the processed live stream on TikTok or another third\-party platform, make sure that you use the push stream URL of the third\-party platform. For information about how to obtain the push stream URL, see the official documentation of the third\-party platform or contact the platform's customer service.<br> |
|Callback |Object of [Callback](https://docs.byteplus.com/en/docs/24/117618#callback) |No |`-` |Callback configuration. |
|Sei |Array of String |No |`["subtitle"]` |To write subtitles into SEI messages in the live stream, set this parameter to `["subtitle"]`.<br><br>> **说明**<br><br><br><br>* > This parameter takes effect only when `Pipe` is set to `si` or `mix`.<br><br><br>* > MediaLive uses `100` as the SEI `type` value when writing subtitles into SEI messages. If your stream pushing tool or app also writes custom SEI messages into the stream, avoid using the same SEI `type` value. Otherwise, the player may identify the custom data as subtitles.<br> |

### SI

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|LipSync |Boolean |No |`true` |Whether to enable lip sync. Default value: `false`. Valid values:<br><br><br>* `true`: Enables lip sync. After this feature is enabled, the speaker's lip movements are synchronized with the dubbed audio, making the live stream more immersive.<br><br>* `false`: Disables lip sync. |

### RealTime

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|VoiceShow |Boolean |No |`true` |Whether to enable dubbed audio. Default value: `false`. Valid values:<br><br><br>* `true`: Enables dubbed audio. After this feature is enabled, translated speech with voice cloning is provided.<br><br>* `false`: Disables dubbed audio. |

### Extra

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|AMix |Object of [AMix](https://docs.byteplus.com/en/docs/24/117618#amix) |No |`-` |The audio mixing configuration. |
|Separator |Object of [Separator](https://docs.byteplus.com/en/docs/24/117618#separator) |No |`-` |The human voice and background sound separation configuration. |

### Subtitle

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Position |Object of [Position](https://docs.byteplus.com/en/docs/24/117618#position) |No |`-` |The subtitle position. |
|Original |Object of [Original](https://docs.byteplus.com/en/docs/24/117618#original) |Yes |`-` |The source subtitle configuration.<br><br>> **说明**<br><br><br>> The source and target languages must be different.<br> |
|Translation |Array of [Translation](https://docs.byteplus.com/en/docs/24/117618#translation) |No |`-` |The translated subtitle configuration.<br><br>> **说明**<br><br><br><br>* > The source and target languages must be different.<br><br><br>* > Currently, you can pass only one translated subtitle language in each request.<br> |
|GlossaryMap |JSON Map |No |`{"赛事直播":"sports live streaming","实时字幕":"real-time subtitles"}` |The glossary. This parameter is empty by default.<br><br>Use the format `"original text":"translation"`, and separate multiple entries with English commas (,). Example: `{"赛事直播":"sports live streaming","实时字幕":"real-time subtitles"}`. The total number of characters cannot exceed 30,000.<br><br>Pass proprietary vocabulary and expected translations, such as brand names, personal names, product names, or feature names, as a reference for the translation model. This helps improve translation accuracy for proprietary vocabulary, **but the expected translations may not be used every time**. If mistranslations persist after you use the glossary, you can use `ReplaceMap` to configure possible mistranslations and their correct translations one by one to forcibly correct translated subtitles.<br><br>> **注意**<br><br><br><br>* > Original text or translation values cannot contain English commas (,).<br><br><br>* > This parameter takes effect only when `Translation` is configured and **applies only to translated subtitles**.<br> |
|ReplaceMap |JSON Map |No |`{"live core":"LiveCore","media life":"MediaLive"}` |The correction list. This parameter is empty by default.<br><br>Configure subtitle text that needs to be forcibly corrected. Add possible mistranslations or recognition errors and their correct text one by one.<br><br>The format is `"incorrect text":"correct text"`. Separate multiple corrections with English commas (,). Each incorrect text or correct text value must be 1 to 50 characters in length. You can pass up to 60 corrections.<br><br>When the system matches the incorrect text, it forcibly replaces the incorrect text with the correct text.<br><br><br>* **Original (ASR) subtitles**: Correct recognition errors. For example, if **MediaLive** is incorrectly recognized as **media life**, you can pass `{"media life":"MediaLive"}`.<br><br>* **Translated subtitles**: Correct mistranslations. **Corrections modify only translated subtitles and do not modify source subtitles or dubbed audio**. For example, if **LiveCore** is mistranslated as **live core**, you can pass `{"live core":"LiveCore"}`.<br><br><br>> **注意**<br><br><br><br>* > Incorrect text and correct text values cannot contain English commas (,).<br><br><br>* > `ReplaceMap` matches text only and does not determine the context. Use this parameter only when the incorrect text can be clearly identified as incorrect. Do not replace incorrect text with text that contains the incorrect text. For example, if you pass `{"stream":"live stream"}`, and the subtitle already correctly displays **live stream**, the system still replaces **stream** with **live stream**, resulting in **live live stream**.<br> |
|HotWords |Array of String |No |`["MediaLive","LiveCore"]` |The hotword list. This parameter is empty by default.<br><br>Hotwords must match the source language, and the total number of characters cannot exceed 30,000.<br><br>Pass hotwords, such as product names and popular phrases, as a reference for the speech recognition model. This helps improve recognition accuracy, **but hotwords may not be recognized accurately every time**. If recognition errors persist after you use hotwords, you can use `ReplaceMap` to configure possible recognition errors and their correct text one by one to forcibly correct Original (ASR) subtitles.<br><br>> **注意**<br><br><br>> This parameter takes effect only for **Original (ASR) subtitles**. For details, see [Usage scenario](https://docs.byteplus.com/en/docs/byteplus-media-live/CreateSpeechTask?lang=en#usage-scenario).<br> |

### Callback

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Url |String |Yes |`https://xxx` |The URL used to receive callback messages. The URL must start with `http://` or `https://`, be publicly accessible, and contain 1–100 characters. For more information about AI Dubbing callback messages, see [AI Dubbing](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-callback-description?lang=en#ai-dubbing). |

### AMix

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|BGVolume |Float |No |`1.0` |The volume of the original sound or background sound excluding human voice. Default value: `0.2`. Valid range: `[0, 1.0]`.<br><br><br>* When `Separator` is set to `true`, this parameter adjusts the background sound volume.<br><br>* When `Separator` is set to `false`, this parameter adjusts the original sound volume. If this parameter is set to `0`, only the human voice in the dubbed audio is retained.<br><br><br>> **说明**<br><br><br>> This parameter takes effect only when `Pipe` is set to `realtime`.<br> |
|AudioEnhance |Boolean |No |`true` |Whether to enable volume balance. Default value: `true`. Valid values:<br><br><br>* `true`: Enables volume balance. The system automatically adjusts the output audio volume to keep the volume stable and comfortable, helping avoid sudden volume changes or harsh bursts and improving the listening experience.<br><br>* `false`: Disables volume balance. |

### Separator

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|HandleType |Integer |No |`0` |Whether to enable noise reduction. Default value: `0`. Valid values:<br><br><br>* `0`: Disables noise reduction.<br><br>* `1`: Enables noise reduction. This can reduce background noise such as electrical noise and environmental noise in dubbed audio and improve final audio clarity.<br><br><br>> **注意**<br><br><br><br>* > Enabling noise reduction may cause background sound to disappear.<br><br><br>* > When `Pipe` is set to `realtime`, this parameter takes effect only when `Separator` is set to `true`.<br> |
|Separator |Boolean |No |`false` |Whether to replace the original sound with dubbed audio. Default value: `false`. Valid values:<br><br><br>* `true`: Completely removes the original sound and outputs only the translated speech. This is suitable for scenarios where the original sound is not needed.<br><br>* `false`: Overlays dubbed audio on the original sound. This is commonly used in sports live streams and other scenarios where the live atmosphere must be retained.<br><br><br>> **说明**<br><br><br>> This parameter takes effect only when `Pipe` is set to `realtime`.<br> |

### Position

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Relative |String |No |`bottom` |The subtitle position in the video. Default value: `bottom`. Valid values:<br><br><br>* `top`: Displays subtitles at the top of the video.<br><br>* `bottom`: Displays subtitles at the bottom of the video. |
|MarginTb |Float |No |`0.05` |The top or bottom margin of the subtitles, that is, the distance from subtitles to the top or bottom edge of the video. The value is a percentage of the video height. Valid range: `(0, 0.5]`.<br><br><br>* When `Relative` is set to `top`, this parameter specifies the top margin.<br><br>* When `Relative` is set to `bottom`, this parameter specifies the bottom margin. |
|MarginLr |Float |No |`0.2` |The left and right margins of the subtitles, that is, the distance from subtitles to the left and right edges of the video. The value is a percentage of the video width. Valid range: `(0, 0.3]`. |

### Original

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Language |String |Yes |`zh` |The source subtitle language. You can call [GetSpeechConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSpeechConfig) and use `OriginalLang` to obtain the source languages available to the current account for subtitle translation and dubbed audio, or use `AsrLang` to obtain the Original (ASR) subtitle languages available to the current account. Pass the `Key` value. |
|Font |String |No |`arial` |The source subtitle font. Default value: `arial`. You can call [GetSpeechConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSpeechConfig) and use `Font` to obtain the font list available to the current account. Pass the `Key` value. |
|FontSize |Integer |No |`32` |The source subtitle font size. Default value: `40`. Valid range: `[1,100]`. |
|FontColor |String |No |`0xFF0000@0.5` |The source subtitle font color. You can specify the color in one of the following ways:<br><br><br>* Start with `0x` or `#`, followed by a hexadecimal RGB color value, and append opacity with `@`. Opacity supports hexadecimal values such as `0x80` and decimal values such as `0.5`. For example, to specify red (`FF0000`) with 50% opacity, pass `0xFF0000@0x80`, `0xFF0000@0.5`, `#FF0000@0x80`, or `#FF0000@0.5`.<br><br>* Use an FFmpeg color keyword and append opacity with `@`. Opacity supports decimal values such as `0.5`. For example, to specify `0xF0F8FF` with 50% opacity, pass `AliceBlue@0.5`.<br><br><br>> **说明**<br><br><br><br>* > For color definitions and more color keywords, see [FFmpeg color syntax](https://ffmpeg.org/ffmpeg-utils.html#color-syntax).<br><br><br>* > A larger opacity value means less transparency.<br><br><br>* > When opacity is specified as a decimal, the valid range is `[0,1]`, with up to two decimal places supported.<br> |
|Alignment |Integer |No |`0` |The source subtitle alignment. Default value: `0`. Valid values:<br><br><br>* `0`: Center\-aligned.<br><br>* `1`: Left\-aligned.<br><br>* `2`: Right\-aligned. |
|MaxRowNumber |Integer |No |`2` |The maximum number of lines for source subtitles. Default value: `0`. Valid values:<br><br><br>* `0`: Automatically wraps lines based on the total number of subtitle characters and the maximum number of characters per line to ensure complete display.<br><br>* `1`: Displays up to one line for each language. Content may be truncated.<br><br>* `2`: Displays up to two lines for each language. Content may be truncated.<br><br><br>> **说明**<br><br><br>> Line limits for source and translated subtitles are calculated separately.<br> |
|MaxCharNumber |Integer |No |`60` |The maximum number of characters per line for source subtitles. Default value: `60`. Recommended value: `60`.<br><br>> **说明**<br><br><br><br>* > The system calculates the final maximum number of displayable characters per line based on this parameter, `MarginLr`, `Font`, `FontSize`, screen resolution, and other factors.<br><br><br>* > Each Chinese character, letter, symbol, or digit counts as one character.<br><br><br>* > When `MaxRowNumber` is set to `1` or `2`, if the total number of source subtitle characters exceeds the display range, the content is truncated. For example, if the maximum number of characters per line is 10 and `MaxRowNumber` is `2`, content after the 20th character is truncated.<br> |
|Hidden |Boolean |No |`false` |Whether to hide source subtitles. Default value: `false`. Valid values:<br><br><br>* `true`: Hides source subtitles.<br><br>* `false`: Displays source subtitles. |
|ShowPriority |Integer |No |`100` |The display priority of source subtitles. By default, source subtitles are displayed above translated subtitles. A larger value indicates a higher priority. For example, if the `ShowPriority` of source subtitles is `1` and `ShowPriority` of translated subtitles is `2`, translated subtitles are displayed above source subtitles. |
|Box |Object of [Box](https://docs.byteplus.com/en/docs/24/117618#box) |No |`-` |The font background of source subtitles. |
|Border |Object of [Border](https://docs.byteplus.com/en/docs/24/117618#border) |No |`-` |The font shadow of source subtitles. |

### Translation

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Language |String |Yes |`en` |The translated subtitle language. You can call [GetSpeechConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSpeechConfig) and use `Lang` to obtain the translated subtitle languages available to the current account. Pass the `Key` value. |
|Font |String |No |`arial` |The translated subtitle font. Default value: `arial`. You can call [GetSpeechConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSpeechConfig) and use `Font` to obtain the font list available to the current account. Pass the `Key` value. |
|FontSize |Integer |No |`32` |The translated subtitle font size. Default value: `40`. Valid range: `[1,100]`. |
|FontColor |String |No |`0xFF0000@0.5` |The translated subtitle font color. You can specify the color in one of the following ways:<br><br><br>* Start with `0x` or `#`, followed by a hexadecimal RGB color value, and append opacity with `@`. Opacity supports hexadecimal values such as `0x80` and decimal values such as `0.5`. For example, to specify red (`FF0000`) with 50% opacity, pass `0xFF0000@0x80`, `0xFF0000@0.5`, `#FF0000@0x80`, or `#FF0000@0.5`.<br><br>* Use an FFmpeg color keyword and append opacity with `@`. Opacity supports decimal values such as `0.5`. For example, to specify `0xF0F8FF` with 50% opacity, pass `AliceBlue@0.5`.<br><br><br>> **说明**<br><br><br><br>* > For color definitions and more color keywords, see [FFmpeg color syntax](https://ffmpeg.org/ffmpeg-utils.html#color-syntax).<br><br><br>* > A larger opacity value means less transparency.<br><br><br>* > When opacity is specified as a decimal, the valid range is `[0,1]`, with up to two decimal places supported.<br> |
|Alignment |Integer |No |`0` |The translated subtitle alignment. Default value: `0`. Valid values:<br><br><br>* `0`: Center\-aligned.<br><br>* `1`: Left\-aligned.<br><br>* `2`: Right\-aligned. |
|MaxRowNumber |Integer |No |`2` |The maximum number of lines for translated subtitles. Default value: `0`. Valid values:<br><br><br>* `0`: Automatically wraps lines based on the total number of subtitle characters and the maximum number of characters per line to ensure complete display.<br><br>* `1`: Displays up to one line for each language. Content may be truncated.<br><br>* `2`: Displays up to two lines for each language. Content may be truncated.<br><br><br>> **说明**<br><br><br>> Line limits for source and translated subtitles are calculated separately.<br> |
|MaxCharNumber |Integer |No |`60` |The maximum number of characters per line for translated subtitles. Default value: `60`. Recommended value: `60`.<br><br>> **说明**<br><br><br><br>* > The system calculates the final maximum number of displayable characters per line based on this parameter, `MarginLr`, `Font`, `FontSize`, screen resolution, and other factors.<br><br><br>* > Each Chinese character, letter, symbol, or digit counts as one character.<br><br><br>* > When `MaxRowNumber` is set to `1` or `2`, if the total number of translated subtitle characters exceeds the display range, the content is truncated. For example, if the maximum number of characters per line is 10 and `MaxRowNumber` is `2`, content after the 20th character is truncated<br> |
|Hidden |Boolean |No |`false` |Whether to hide translated subtitles. Default value: `false`. Valid values:<br><br><br>* `true`: Hides translated subtitles.<br><br>* `false`: Displays translated subtitles. |
|ShowPriority |Integer |No |`100` |The display priority of translated subtitles. By default, source subtitles are displayed above translated subtitles. A larger value indicates a higher priority. For example, if the `ShowPriority` of source subtitles is `1` and `ShowPriority` of translated subtitles is `2`, translated subtitles are displayed above source subtitles. |
|Box |Object of [Box](https://docs.byteplus.com/en/docs/24/117618#box) |No |`-` |The font background of translated subtitles. |
|Border |Object of [Border](https://docs.byteplus.com/en/docs/24/117618#border) |No |`-` |The font shadow of translated subtitles. |

### Box

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|W |Float |Yes |`1.0` |The width, in px. Recommended range: `[1,10]`. |
|Color |String |Yes |`0xFF0000@0.5` |The color. You can specify the color in one of the following ways:<br><br><br>* Start with `0x` or `#`, followed by a hexadecimal RGB color value, and append opacity with `@`. Opacity supports hexadecimal values such as `0x80` and decimal values such as `0.5`. For example, to specify red (`FF0000`) with 50% opacity, pass `0xFF0000@0x80`, `0xFF0000@0.5`, `#FF0000@0x80`, or `#FF0000@0.5`.<br><br>* Use an FFmpeg color keyword and append opacity with `@`. Opacity supports decimal values such as `0.5`. For example, to specify `0xF0F8FF` with 50% opacity, pass `AliceBlue@0.5`.<br><br><br>> **说明**<br><br><br><br>* > For color definitions and more color keywords, see [FFmpeg color syntax](https://ffmpeg.org/ffmpeg-utils.html#color-syntax).<br><br><br>* > A larger opacity value means less transparency.<br><br><br>* > When opacity is specified as a decimal, the valid range is `[0,1]`, with up to two decimal places supported.<br> |

### Border

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|W |Float |Yes |`1.0` |The width, in px. Recommended range: `[1,10]`. |
|Color |String |Yes |`0xFF0000@0.5` |The color. You can specify the color in one of the following ways:<br><br><br>* Start with `0x` or `#`, followed by a hexadecimal RGB color value, and append opacity with `@`. Opacity supports hexadecimal values such as `0x80` and decimal values such as `0.5`. For example, to specify red (`FF0000`) with 50% opacity, pass `0xFF0000@0x80`, `0xFF0000@0.5`, `#FF0000@0x80`, or `#FF0000@0.5`.<br><br>* Use an FFmpeg color keyword and append opacity with `@`. Opacity supports decimal values such as `0.5`. For example, to specify `0xF0F8FF` with 50% opacity, pass `AliceBlue@0.5`.<br><br><br>> **说明**<br><br><br><br>* > For color definitions and more color keywords, see [FFmpeg color syntax](https://ffmpeg.org/ffmpeg-utils.html#color-syntax).<br><br><br>* > A larger opacity value means less transparency.<br><br><br>* > When opacity is specified as a decimal, the valid range is `[0,1]`, with up to two decimal places supported.<br> |

## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Code |Integer |`0` |The status code. |
|Message |String |`success` |The status message. |
|Data |Object of [Data](https://docs.byteplus.com/en/docs/24/117618#data) |`-` |The task information. |

### Data

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|TaskID |String |`b71c61****24ae4f` |The task ID. |

## Samples

### Sample request

**Original (ASR) subtitles (whole\-sentence display)**

```json
POST https://open.byteplusapi.com/?Action=CreateSpeechTask&Version=2023-01-01
{
    "Name": "TaskA",
    "Rule": {
        "Pipe": "mix",
        "Delay": 15,
        "Source": {
            "Url": "https://pull.example.com/live/test.flv"
        },
        "StartTime": "2026-11-17T11:30:06+08:00",
        "EndTime": "2026-11-17T13:30:06+08:00",
        "Output": {
            "Url": [
                "rtmp://push.example.com/live/test01",
                "rtmp://push.example.com/live/test02"
            ],
            "Callback": {
                "Url": "https://example.com/callback"
            },
            "Sei": [
                "subtitle"
            ]
        },
        "Subtitle": {
            "Position": {
                "Relative": "bottom",
                "MarginTb": 0.05,
                "MarginLr": 0.2
            },
            "Original": {
                "Language": "en",
                "Font": "arial",
                "FontSize": 32,
                "FontColor": "0xFFFFFF@1",
                "Alignment": 0,
                "MaxRowNumber": 2,
                "MaxCharNumber": 60,
                "Hidden": false,
                "ShowPriority": 100,
                "Box": {
                    "W": 1.0,
                    "Color": "0x000000@0.5"
                },
                "Border": {
                    "W": 1.0,
                    "Color": "0x000000@0.5"
                }
            },
            "HotWords": [
                "MediaLive",
                "LiveCore"
            ],
            "ReplaceMap": {
                "media life": "MediaLive"
            }
        }
    }
}
```

**Original (ASR) subtitles (live streaming display)**

```json
POST https://open.byteplusapi.com/?Action=CreateSpeechTask&Version=2023-01-01
{
    "Name": "TaskB",
    "Rule": {
        "Pipe": "realtime",
        "Delay": 2,
        "Source": {
            "Url": "https://pull.example.com/live/test.flv"
        },
        "StartTime": "2026-11-17T11:30:06+08:00",
        "EndTime": "2026-11-17T13:30:06+08:00",
        "Output": {
            "Url": [
                "rtmp://push.example.com/live/test01",
                "rtmp://push.example.com/live/test02"
            ],
            "Callback": {
                "Url": "https://example.com/callback"
            }
        },
        "Subtitle": {
            "Position": {
                "Relative": "bottom",
                "MarginTb": 0.05,
                "MarginLr": 0.2
            },
            "Original": {
                "Language": "en",
                "Font": "arial",
                "FontSize": 32,
                "FontColor": "0xFFFFFF@1",
                "Alignment": 0,
                "MaxRowNumber": 2,
                "MaxCharNumber": 60,
                "Hidden": false,
                "ShowPriority": 100,
                "Box": {
                    "W": 1.0,
                    "Color": "0x000000@0.5"
                },
                "Border": {
                    "W": 1.0,
                    "Color": "0x000000@0.5"
                }
            },
            "HotWords": [
                "MediaLive",
                "LiveCore"
            ],
            "ReplaceMap": {
                "media life": "MediaLive"
            }
        }
    }
}
```

**Subtitle translation**

```json
POST https://open.byteplusapi.com/?Action=CreateSpeechTask&Version=2023-01-01
{
    "Name": "TaskC",
    "Rule": {
        "Pipe": "mix",
        "Delay": 8,
        "Source": {
            "Url": "https://pull.example.com/live/test.flv"
        },
        "StartTime": "2026-11-17T11:30:06+08:00",
        "EndTime": "2026-11-17T13:30:06+08:00",
        "Output": {
            "Url": [
                "rtmp://push.example.com/live/test01",
                "rtmp://push.example.com/live/test02"
            ],
            "Callback": {
                "Url": "https://example.com/callback"
            },
            "Sei": [
                "subtitle"
            ]
        },
        "Subtitle": {
            "Position": {
                "Relative": "bottom",
                "MarginTb": 0.05,
                "MarginLr": 0.2
            },
            "Original": {
                "Language": "zh",
                "Font": "arial",
                "FontSize": 32,
                "FontColor": "0xFFFFFF@1",
                "Alignment": 0,
                "MaxRowNumber": 2,
                "MaxCharNumber": 60,
                "Hidden": false,
                "ShowPriority": 100,
                "Box": {
                    "W": 1.0,
                    "Color": "0x000000@0.5"
                },
                "Border": {
                    "W": 1.0,
                    "Color": "0x000000@0.5"
                }
            },
            "Translation": [
                {
                    "Language": "en",
                    "Font": "arial",
                    "FontSize": 32,
                    "FontColor": "0xFFFFFF@1",
                    "Alignment": 0,
                    "MaxRowNumber": 2,
                    "MaxCharNumber": 60,
                    "Hidden": false,
                    "ShowPriority": 90,
                    "Box": {
                        "W": 1.0,
                        "Color": "0x000000@0.5"
                    },
                    "Border": {
                        "W": 1.0,
                        "Color": "0x000000@0.5"
                    }
                }
            ],
            "GlossaryMap": {
                "赛事直播": "sports live streaming",
                "实时字幕": "real-time subtitles"
            },
            "ReplaceMap": {
                "live core": "LiveCore"
            }
        }
    }
}
```

**Dubbed audio + bilingual subtitles**

```json
POST https://open.byteplusapi.com/?Action=CreateSpeechTask&Version=2023-01-01
{
    "Name": "TaskD",
    "Rule": {
        "Pipe": "realtime",
        "Delay": 3,
        "Source": {
            "Url": "https://pull.example.com/live/test.flv"
        },
        "StartTime": "2026-11-17T11:30:06+08:00",
        "EndTime": "2026-11-17T13:30:06+08:00",
        "Output": {
            "Url": [
                "rtmp://push.example.com/live/test01",
                "rtmp://push.example.com/live/test02"
            ],
            "Callback": {
                "Url": "https://example.com/callback"
            }
        },
        "RealTime": {
            "VoiceShow": true
        },
        "Extra": {
            "AMix": {
                "BGVolume": 0.2,
                "AudioEnhance": true
            },
            "Separator": {
                "HandleType": 1,
                "Separator": true
            }
        },
        "Subtitle": {
            "Position": {
                "Relative": "bottom",
                "MarginTb": 0.05,
                "MarginLr": 0.2
            },
            "Original": {
                "Language": "zh",
                "Font": "arial",
                "FontSize": 32,
                "FontColor": "0xFFFFFF@1",
                "Alignment": 0,
                "MaxRowNumber": 2,
                "MaxCharNumber": 60,
                "Hidden": false,
                "ShowPriority": 100,
                "Box": {
                    "W": 1.0,
                    "Color": "0x000000@0.5"
                },
                "Border": {
                    "W": 1.0,
                    "Color": "0x000000@0.5"
                }
            },
            "Translation": [
                {
                    "Language": "en",
                    "Font": "arial",
                    "FontSize": 32,
                    "FontColor": "0xFFFFFF@1",
                    "Alignment": 0,
                    "MaxRowNumber": 2,
                    "MaxCharNumber": 60,
                    "Hidden": false,
                    "ShowPriority": 90,
                    "Box": {
                        "W": 1.0,
                        "Color": "0x000000@0.5"
                    },
                    "Border": {
                        "W": 1.0,
                        "Color": "0x000000@0.5"
                    }
                }
            ],
            "GlossaryMap": {
                "赛事直播": "sports live streaming",
                "实时字幕": "real-time subtitles"
            },
            "ReplaceMap": {
                "live core": "LiveCore"
            }
        }
    }
}
```

**Dubbed audio + lip sync + bilingual subtitles**

```json
POST https://open.byteplusapi.com/?Action=CreateSpeechTask&Version=2023-01-01
{
    "Name": "TaskE",
    "Rule": {
        "Pipe": "si",
        "Delay": 20,
        "Source": {
            "Url": "https://pull.example.com/live/test.flv"
        },
        "StartTime": "2026-11-17T11:30:06+08:00",
        "EndTime": "2026-11-17T13:30:06+08:00",
        "Output": {
            "Url": [
                "rtmp://push.example.com/live/test01",
                "rtmp://push.example.com/live/test02"
            ],
            "Callback": {
                "Url": "https://example.com/callback"
            },
            "Sei": [
                "subtitle"
            ]
        },
        "SI": {
            "LipSync": true
        },
        "Subtitle": {
            "Position": {
                "Relative": "bottom",
                "MarginTb": 0.05,
                "MarginLr": 0.2
            },
            "Original": {
                "Language": "zh",
                "Font": "arial",
                "FontSize": 32,
                "FontColor": "0xFFFFFF@1",
                "Alignment": 0,
                "MaxRowNumber": 2,
                "MaxCharNumber": 60,
                "Hidden": false,
                "ShowPriority": 100,
                "Box": {
                    "W": 1.0,
                    "Color": "0x000000@0.5"
                },
                "Border": {
                    "W": 1.0,
                    "Color": "0x000000@0.5"
                }
            },
            "Translation": [
                {
                    "Language": "en",
                    "Font": "arial",
                    "FontSize": 32,
                    "FontColor": "0xFFFFFF@1",
                    "Alignment": 0,
                    "MaxRowNumber": 2,
                    "MaxCharNumber": 60,
                    "Hidden": false,
                    "ShowPriority": 90,
                    "Box": {
                        "W": 1.0,
                        "Color": "0x000000@0.5"
                    },
                    "Border": {
                        "W": 1.0,
                        "Color": "0x000000@0.5"
                    }
                }
            ],
            "GlossaryMap": {
                "赛事直播": "sports live streaming",
                "实时字幕": "real-time subtitles"
            },
            "ReplaceMap": {
                "live core": "LiveCore"
            }
        }
    }
}
```

### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateSpeechTask",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Code": 0,
        "Message": "success",
        "Data": {
            "TaskID": "b71c61****24ae4f"
        }
    }
}
```

## Error codes

For more information about error codes, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).
