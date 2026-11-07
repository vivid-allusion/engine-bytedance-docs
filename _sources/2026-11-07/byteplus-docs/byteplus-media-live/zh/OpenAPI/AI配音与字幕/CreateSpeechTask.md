---
title: "CreateSpeechTask"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/CreateSpeechTask-zh-CN"
---

调用 `CreateSpeechTask` API 创建 AI 配音任务。任务创建后，当您在 `StartTime` 到 `EndTime` 的转推时间段内开始推送流时，任务会自动拉取直播流进行 AI 配音处理，并将处理后的直播流推送到指定推流地址。例如，您可以使用 OBS 发起直播，通过 AI 配音任务处理直播流，然后在 TikTok 上直播处理后的内容。更多信息，请参见 [AI 配音](https://docs.byteplus.com/en/docs/byteplus-media-live/ai-liveinterpret-simultaneous-audio-and-video-interpretation)。

## 使用场景

根据您的场景选择合适的功能。

|场景 |推荐功能 |参数配置 |描述 |
|---|---|---|---|
|为直播流提供基础字幕，帮助观众在静音或嘈杂环境中观看。 |原文（ASR）字幕 |* 整句展示：字幕按句显示。将 `Pipe` 设置为 `mix`（仅字幕），并仅配置 `Original`（源字幕），不配置 `Translation`（译文字幕）。<br><br>* 直播展示：字幕不等待句子结束，按字或按词显示。将 `Pipe` 设置为 `realtime`（实时传译模式），并仅配置 `Original`（源字幕），不配置 `Translation`（译文字幕）。 |使用语音识别在视频上叠加源字幕。<br><br>> **说明**<br><br><br>> 目前，直播展示仅支持中文和英文字幕。整句展示支持更多语言。<br> |
|支持跨语言文字交流，触达全球受众。 |字幕翻译 |将 `Pipe` 设置为 `mix`（仅字幕）或 `realtime`（实时传译模式），并同时配置 `Original`（源字幕）和 `Translation`（译文字幕）。 |使用语音识别在保留原声的同时，在视频上叠加译文字幕。 |
|提供类似观看配音电影的配音式翻译体验。 |配音音频 |将 `Pipe` 设置为 `realtime`（实时传译模式）并将 `VoiceShow` 设置为 `true`，或将 `Pipe` 设置为 `si`（AI 配音模式），并配置 `Original`（源字幕）和 `Translation`（译文字幕）的 `Language` 字段。 |提供配音音频并替换原声。在实时传译模式下，您可以选择将配音音频叠加到原声上，或直接替换原声。 |
|提供沉浸式真人译员体验，提升专业感。 |配音音频 + 唇形同步 |将 `Pipe` 设置为 `si`（AI 配音模式），将 `LipSync` 设置为 `true`，并配置 `Original`（源字幕）和 `Translation`（译文字幕）的 `Language` 字段。 |基于配音音频，AI 技术会将说话人的唇部动作与配音音频同步，营造高度逼真的效果。 |

## 要求

* **速率限制**：每个账号每秒 10 次请求。

* **计费**：仅收取 AI 配音费用。AI 配音按任务的**实际推流时长**计费。更多信息，请参见 [AI 配音计费](https://docs.byteplus.com/en/docs/byteplus-media-live/ai_dubbing)。

* **并发限制**：每个账号最多可同时运行 2 个任务。如需同时运行更多任务，请[提交工单](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)联系技术支持。

* **前提条件**

   * 确保推流和拉流域名已添加到同一域名空间下。更多信息，请参见 [CreateDomain](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-dj3h3u96xn)。

      > **注意**

      > 仅当您使用 MediaLive 推流和拉流地址时，才需要满足此前提条件。

   * 准备好**拉流 URL** 和**推流 URL**。

      * **拉流 URL**：获取有效的拉流地址，用于拉取原始直播流。支持 RTMP 和 FLV 格式。

         如果您使用 MediaLive 拉流地址作为**拉流 URL**，请使用相同的 `AppName` 和 `StreamName`，并通过 [GeneratePushURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generatepushurl-2023) 和 [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) 生成一对地址。该地址对包括作为**拉流 URL** 使用的拉流地址，以及用于推送原始直播流的推流地址。

      * **推流 URL**：用于推送处理后的直播流。支持 RTMP 格式。

         * 如果您使用 MediaLive 推流地址作为**推流 URL**，请使用相同的 `AppName` 和 `StreamName`，并通过 [GeneratePushURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generatepushurl-2023) 和 [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) 生成一对地址。该地址对包括作为**推流 URL** 使用的推流地址，以及用于拉取处理后直播流的拉流地址。

         * 如果您使用其他云服务商或 TikTok 等直播平台的推流地址作为**推流 URL**，请参见对应平台的官方文档，或联系平台客服获取有效的推流地址。

   > **说明**

   > 用于推送原始直播流的推流地址，以及用于拉取处理后直播流的拉流地址，不受特定协议限制。请根据实际需求选择协议。

## HTTP 请求

* 方法：POST

* 端点：https://open.byteplusapi.com/?Action=CreateSpeechTask&Version=2023\-01\-01

## 请求参数

### 公共参数

调用所有 API 时，除 API 专用参数外，还必须传入[公共参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

### Query

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Action |String |是 |`CreateSpeechTask` |API 操作。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。当前版本：2023\-01\-01。 |

### Body 参数

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Name |String |是 |`TaskA` |任务名称。该名称在所有运行中的任务中必须唯一。名称长度必须为 1 到 20 个字符，可包含数字（0\-9）、大写字母（A\-Z）、小写字母（a\-z）、中文字符、下划线（_）和连字符（\-）。 |
|Rule |[Rule](https://docs.byteplus.com/en/docs/24/118396#rule) 对象 |是 |`-` |任务规则。 |

### Rule

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Pipe |String |是 |`si` |任务类型。有效值：<br><br><br>* `si`：AI 配音模式。字幕、配音音频和视频完全同步。支持唇形同步。此模式适用于会议直播等需要强同步和沉浸感的场景。此模式会引入一定延迟。<br><br>* `mix`：仅字幕，包括整句展示的原文（ASR）字幕。<br><br>* `realtime`：实时传译模式，包括直播展示的原文（ASR）字幕。此模式延迟较低，但视频可能无法与字幕或配音音频同步。此模式适用于体育直播等延迟敏感场景。<br><br><br>> **说明**<br><br><br>> 当此参数设置为 `si` 时，默认启用配音音频，且无法关闭。<br> |
|Delay |Integer |否 |`20` |播放延迟，单位为秒，用于为配音音频和字幕翻译预留足够时间。有效范围：`[0,60]`。推荐值因任务类型（`Pipe`）和功能而异：<br><br><br>* `si`：<br><br>   * 启用唇形同步、配音音频和字幕：`20`。<br><br>   * 启用配音音频和字幕：`12`。<br><br>* `mix`：<br><br>   * 整句展示的原文（ASR）字幕：`15`。<br><br>   * 字幕翻译：`8`。<br><br>* `realtime`：`2` 或 `3`。<br><br><br>有关详细功能配置，请参见[使用场景](https://docs.byteplus.com/en/docs/byteplus-media-live/CreateSpeechTask?lang=en#usage-scenario)。<br><br>> **说明**<br><br><br>> 如果字幕早于原声或视频出现，请降低播放延迟，使字幕与原声或视频对齐，反之亦然。<br> |
|Source |[Source](https://docs.byteplus.com/en/docs/24/118396#source) 对象 |是 |`-` |源流配置。 |
|StartTime |String |否 |`2025-11-17T11:30:06+08:00` |任务开始时间。时间采用 RFC3339 格式，使用 UTC+8，精确到秒。如果未传入此参数，任务会立即开始。 |
|EndTime |String |否 |`2025-11-17T12:11:06+08:00` |任务结束时间。结束时间必须晚于 `StartTime`，且 `StartTime` 与 `EndTime` 之间的时间跨度不能超过 7 天。时间采用 RFC3339 格式，使用 UTC+8，精确到秒。如果未传入此参数，任务会在开始时间后 7 天结束。<br><br>> **说明**<br><br><br>> 当任务结束、源流断开或拉流失败时，转推会自动停止。<br> |
|Output |[Output](https://docs.byteplus.com/en/docs/24/118396#output) 对象 |是 |`-` |推流配置。 |
|SI |[SI](https://docs.byteplus.com/en/docs/24/118396#si) 对象 |否 |`-` |AI 配音模式配置。<br><br>> **说明**<br><br><br>> 此参数仅在 `Pipe` 设置为 `si` 时生效。<br> |
|RealTime |[RealTime](https://docs.byteplus.com/en/docs/24/118396#realtime) 对象 |否 |`-` |实时传译模式配置。<br><br>> **说明**<br><br><br>> 此参数仅在 `Pipe` 设置为 `realtime` 时生效。<br> |
|Extra |[Extra](https://docs.byteplus.com/en/docs/24/118396#extra) 对象 |否 |`-` |额外配置。<br><br>> **说明**<br><br><br>> 建议仅在启用配音音频时传入此参数。有关配音音频配置的详细信息，请参见[使用场景](https://docs.byteplus.com/en/docs/byteplus-media-live/CreateSpeechTask?lang=en#usage-scenario)。<br> |
|Subtitle |[Subtitle](https://docs.byteplus.com/en/docs/24/118396#subtitle) 对象 |否 |`-` |字幕配置。 |

### Source

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Url |String |是 |`https://xxx/live/xxx.flv` |**拉流 URL**。支持 RTMP 和 FLV 格式。任务会从此 URL 拉取原始直播流并处理该流。<br><br>> **说明**<br><br><br>> URL 不能直接包含中文字符等多字节字符。如果需要使用此类字符，请对其进行 URL 编码。<br> |

### Output

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Url |Array of String |是 |`["rtmp://push.example.com/live/test01","rtmp://push.example.com/live/test02"]` |**推流 URL**。支持 RTMP 格式。任务会将处理后的直播流推送到此 URL。<br><br>最多可传入 8 个推流 URL。<br><br>> **说明**<br><br><br><br>* > URL 不能直接包含中文字符等多字节字符。如果需要使用此类字符，请对其进行 URL 编码。<br><br><br>* > 如需在 TikTok 或其他第三方平台播放处理后的直播流，请确保使用第三方平台的推流 URL。有关如何获取推流 URL 的信息，请参见第三方平台的官方文档，或联系平台客服。<br> |
|Callback |[Callback](https://docs.byteplus.com/en/docs/24/118396#callback) 对象 |否 |`-` |回调配置。 |
|Sei |Array of String |否 |`["subtitle"]` |如需将字幕写入直播流中的 SEI 消息，请将此参数设置为 `["subtitle"]`。<br><br>> **说明**<br><br><br><br>* > 此参数仅在 `Pipe` 设置为 `si` 或 `mix` 时生效。<br><br><br>* > MediaLive 将字幕写入 SEI 消息时，使用 `100` 作为 SEI `type` 值。如果您的推流工具或应用也会向流中写入自定义 SEI 消息，请避免使用相同的 SEI `type` 值。否则，播放器可能会将自定义数据识别为字幕。<br> |

### SI

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|LipSync |Boolean |否 |`true` |是否启用唇形同步。默认值：`false`。有效值：<br><br><br>* `true`：启用唇形同步。启用此功能后，说话人的唇部动作会与配音音频同步，使直播流更具沉浸感。<br><br>* `false`：禁用唇形同步。 |

### RealTime

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|VoiceShow |Boolean |否 |`true` |是否启用配音音频。默认值：`false`。有效值：<br><br><br>* `true`：启用配音音频。启用此功能后，会提供带有声音克隆效果的翻译语音。<br><br>* `false`：禁用配音音频。 |

### Extra

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|AMix |[AMix](https://docs.byteplus.com/en/docs/24/118396#amix) 对象 |否 |`-` |混音配置。 |
|Separator |[Separator](https://docs.byteplus.com/en/docs/24/118396#separator) 对象 |否 |`-` |人声和背景声分离配置。 |

### Subtitle

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Position |[Position](https://docs.byteplus.com/en/docs/24/118396#position) 对象 |否 |`-` |字幕位置。 |
|Original |[Original](https://docs.byteplus.com/en/docs/24/118396#original) 对象 |是 |`-` |源字幕配置。<br><br>> **说明**<br><br><br>> 源语言和目标语言必须不同。<br> |
|Translation |[Translation](https://docs.byteplus.com/en/docs/24/118396#translation) 数组 |否 |`-` |译文字幕配置。<br><br>> **说明**<br><br><br><br>* > 源语言和目标语言必须不同。<br><br><br>* > 目前，每个请求只能传入一种译文字幕语言。<br> |
|GlossaryMap |JSON Map |否 |`{"赛事直播":"sports live streaming","实时字幕":"real-time subtitles"}` |术语表。此参数默认为空。<br><br>使用 `"原文":"译文"` 格式，并使用英文逗号（,）分隔多个条目。示例：`{"赛事直播":"sports live streaming","实时字幕":"real-time subtitles"}`。总字符数不能超过 30,000。<br><br>传入专有词汇及期望译文，例如品牌名称、人名、产品名称或功能名称，作为翻译模型的参考。这有助于提升专有词汇的翻译准确性，**但期望译文并非每次都会被使用**。如果使用术语表后仍存在误译，您可以使用 `ReplaceMap` 逐一配置可能的误译及其正确译文，以强制纠正译文字幕。<br><br>> **警告**<br><br><br><br>* > 原文或译文值不能包含英文逗号（,）。<br><br><br>* > 此参数仅在配置 `Translation` 时生效，且**仅适用于译文字幕**。<br> |
|ReplaceMap |JSON Map |否 |`{"live core":"LiveCore","media life":"MediaLive"}` |纠错列表。此参数默认为空。<br><br>配置需要强制纠正的字幕文本。逐一添加可能的误译或识别错误及其正确文本。<br><br>格式为 `"错误文本":"正确文本"`。使用英文逗号（,）分隔多个纠错项。每个错误文本或正确文本值的长度必须为 1 到 50 个字符。最多可传入 60 个纠错项。<br><br>当系统匹配到错误文本时，会强制将错误文本替换为正确文本。<br><br><br>* **原文（ASR）字幕**：纠正识别错误。例如，如果 **MediaLive** 被错误识别为 **media life**，您可以传入 `{"media life":"MediaLive"}`。<br><br>* **译文字幕**：纠正误译。**纠错仅修改译文字幕，不会修改源字幕或配音音频**。例如，如果 **LiveCore** 被误译为 **live core**，您可以传入 `{"live core":"LiveCore"}`。<br><br><br>> **警告**<br><br><br><br>* > 错误文本和正确文本值不能包含英文逗号（,）。<br><br><br>* > `ReplaceMap` 仅进行文本匹配，不判断上下文。仅当错误文本可明确识别为错误时，才使用此参数。不要将错误文本替换为包含该错误文本的文本。例如，如果传入 `{"stream":"live stream"}`，且字幕已正确显示 **live stream**，系统仍会将 **stream** 替换为 **live stream**，导致出现 **live live stream**。<br> |
|HotWords |Array of String |否 |`["MediaLive","LiveCore"]` |热词列表。此参数默认为空。<br><br>热词必须与源语言匹配，且总字符数不能超过 30,000。<br><br>传入产品名称、流行短语等热词，作为语音识别模型的参考。这有助于提升识别准确性，**但热词并非每次都能被准确识别**。如果使用热词后仍存在识别错误，您可以使用 `ReplaceMap` 逐一配置可能的识别错误及其正确文本，以强制纠正原文（ASR）字幕。<br><br>> **警告**<br><br><br>> 此参数仅对**原文（ASR）字幕**生效。详情请参见[使用场景](https://docs.byteplus.com/en/docs/byteplus-media-live/CreateSpeechTask?lang=en#usage-scenario)。<br> |

### Callback

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Url |String |是 |`https://xxx` |用于接收回调消息的 URL。该 URL 必须以 `http://` 或 `https://` 开头，可公开访问，且包含 1–100 个字符。有关 AI 配音回调消息的更多信息，请参见 [AI 配音](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-callback-description?lang=en#ai-dubbing)。 |

### AMix

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|BGVolume |Float |否 |`1.0` |原声或除人声以外的背景声的音量。默认值：`0.2`。有效范围：`[0, 1.0]`。<br><br><br>* 当 `Separator` 设置为 `true` 时，此参数调整背景声音量。<br><br>* 当 `Separator` 设置为 `false` 时，此参数调整原声音量。如果此参数设置为 `0`，则仅保留配音音频中的人声。<br><br><br>> **说明**<br><br><br>> 此参数仅在 `Pipe` 设置为 `realtime` 时生效。<br> |
|AudioEnhance |Boolean |否 |`true` |是否启用音量均衡。默认值：`true`。有效值：<br><br><br>* `true`：启用音量均衡。系统会自动调整输出音频音量，使音量保持稳定舒适，帮助避免音量突变或刺耳爆音，并提升收听体验。<br><br>* `false`：禁用音量均衡。 |

### Separator

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|HandleType |Integer |否 |`0` |是否启用降噪。默认值：`0`。有效值：<br><br><br>* `0`：禁用降噪。<br><br>* `1`：启用降噪。可减少配音音频中的电流噪声、环境噪声等背景噪声，并提升最终音频清晰度。<br><br><br>> **警告**<br><br><br><br>* > 启用降噪可能导致背景声消失。<br><br><br>* > 当 `Pipe` 设置为 `realtime` 时，此参数仅在 `Separator` 设置为 `true` 时生效。<br> |
|Separator |Boolean |否 |`false` |是否使用配音音频替换原声。默认值：`false`。有效值：<br><br><br>* `true`：完全移除原声，仅输出翻译语音。适用于不需要原声的场景。<br><br>* `false`：将配音音频叠加到原声上。常用于体育直播等需要保留现场氛围的场景。<br><br><br>> **说明**<br><br><br>> 此参数仅在 `Pipe` 设置为 `realtime` 时生效。<br> |

### Position

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Relative |String |否 |`bottom` |字幕在视频中的位置。默认值：`bottom`。有效值：<br><br><br>* `top`：在视频顶部显示字幕。<br><br>* `bottom`：在视频底部显示字幕。 |
|MarginTb |Float |否 |`0.05` |字幕的顶部或底部边距，即字幕到视频顶部或底部边缘的距离。该值为视频高度的百分比。有效范围：`(0, 0.5]`。<br><br><br>* 当 `Relative` 设置为 `top` 时，此参数指定顶部边距。<br><br>* 当 `Relative` 设置为 `bottom` 时，此参数指定底部边距。 |
|MarginLr |Float |否 |`0.2` |字幕的左右边距，即字幕到视频左右边缘的距离。该值为视频宽度的百分比。有效范围：`(0, 0.3]`。 |

### Original

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Language |String |是 |`zh` |源字幕语言。您可以调用 [GetSpeechConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSpeechConfig)，并使用 `OriginalLang` 获取当前账号可用于字幕翻译和配音音频的源语言，或使用 `AsrLang` 获取当前账号可用的原文（ASR）字幕语言。传入 `Key` 值。 |
|Font |String |否 |`arial` |源字幕字体。默认值：`arial`。您可以调用 [GetSpeechConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSpeechConfig)，并使用 `Font` 获取当前账号可用的字体列表。传入 `Key` 值。 |
|FontSize |Integer |否 |`32` |源字幕字号。默认值：`40`。有效范围：`[1,100]`。 |
|FontColor |String |否 |`0xFF0000@0.5` |源字幕字体颜色。您可以通过以下任一方式指定颜色：<br><br><br>* 以 `0x` 或 `#` 开头，后跟十六进制 RGB 颜色值，并使用 `@` 追加不透明度。不透明度支持 `0x80` 等十六进制值，以及 `0.5` 等十进制值。例如，要指定 50% 不透明度的红色（`FF0000`），请传入 `0xFF0000@0x80`、`0xFF0000@0.5`、`#FF0000@0x80` 或 `#FF0000@0.5`。<br><br>* 使用 FFmpeg 颜色关键字，并使用 `@` 追加不透明度。不透明度支持 `0.5` 等十进制值。例如，要指定 50% 不透明度的 `0xF0F8FF`，请传入 `AliceBlue@0.5`。<br><br><br>> **说明**<br><br><br><br>* > 有关颜色定义和更多颜色关键字，请参见 [FFmpeg 颜色语法](https://ffmpeg.org/ffmpeg-utils.html#color-syntax)。<br><br><br>* > 不透明度值越大，透明度越低。<br><br><br>* > 当不透明度指定为十进制时，有效范围为 `[0,1]`，最多支持两位小数。<br> |
|Alignment |Integer |否 |`0` |源字幕对齐方式。默认值：`0`。有效值：<br><br><br>* `0`：居中对齐。<br><br>* `1`：左对齐。<br><br>* `2`：右对齐。 |
|MaxRowNumber |Integer |否 |`2` |源字幕的最大行数。默认值：`0`。有效值：<br><br><br>* `0`：根据字幕总字符数和每行最大字符数自动换行，确保完整显示。<br><br>* `1`：每种语言最多显示一行。内容可能被截断。<br><br>* `2`：每种语言最多显示两行。内容可能被截断。<br><br><br>> **说明**<br><br><br>> 源字幕和译文字幕的行数限制会分别计算。<br> |
|MaxCharNumber |Integer |否 |`60` |源字幕每行最大字符数。默认值：`60`。推荐值：`60`。<br><br>> **说明**<br><br><br><br>* > 系统会基于此参数、`MarginLr`、`Font`、`FontSize`、屏幕分辨率等因素，计算最终每行可显示的最大字符数。<br><br><br>* > 每个中文字符、字母、符号或数字均计为一个字符。<br><br><br>* > 当 `MaxRowNumber` 设置为 `1` 或 `2` 时，如果源字幕总字符数超出显示范围，内容会被截断。例如，如果每行最大字符数为 10，且 `MaxRowNumber` 为 `2`，则第 20 个字符之后的内容会被截断。<br> |
|Hidden |Boolean |否 |`false` |是否隐藏源字幕。默认值：`false`。有效值：<br><br><br>* `true`：隐藏源字幕。<br><br>* `false`：显示源字幕。 |
|ShowPriority |Integer |否 |`100` |源字幕的显示优先级。默认情况下，源字幕显示在译文字幕上方。值越大表示优先级越高。例如，如果源字幕的 `ShowPriority` 为 `1`，译文字幕的 `ShowPriority` 为 `2`，则译文字幕显示在源字幕上方。 |
|Box |[Box](https://docs.byteplus.com/en/docs/24/118396#box) 对象 |否 |`-` |源字幕的字体背景。 |
|Border |[Border](https://docs.byteplus.com/en/docs/24/118396#border) 对象 |否 |`-` |源字幕的字体阴影。 |

### Translation

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Language |String |是 |`en` |译文字幕语言。您可以调用 [GetSpeechConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSpeechConfig)，并使用 `Lang` 获取当前账号可用的译文字幕语言。传入 `Key` 值。 |
|Font |String |否 |`arial` |译文字幕字体。默认值：`arial`。您可以调用 [GetSpeechConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSpeechConfig)，并使用 `Font` 获取当前账号可用的字体列表。传入 `Key` 值。 |
|FontSize |Integer |否 |`32` |译文字幕字号。默认值：`40`。有效范围：`[1,100]`。 |
|FontColor |String |否 |`0xFF0000@0.5` |译文字幕字体颜色。您可以通过以下任一方式指定颜色：<br><br><br>* 以 `0x` 或 `#` 开头，后跟十六进制 RGB 颜色值，并使用 `@` 追加不透明度。不透明度支持 `0x80` 等十六进制值，以及 `0.5` 等十进制值。例如，要指定 50% 不透明度的红色（`FF0000`），请传入 `0xFF0000@0x80`、`0xFF0000@0.5`、`#FF0000@0x80` 或 `#FF0000@0.5`。<br><br>* 使用 FFmpeg 颜色关键字，并使用 `@` 追加不透明度。不透明度支持 `0.5` 等十进制值。例如，要指定 50% 不透明度的 `0xF0F8FF`，请传入 `AliceBlue@0.5`。<br><br><br>> **说明**<br><br><br><br>* > 有关颜色定义和更多颜色关键字，请参见 [FFmpeg 颜色语法](https://ffmpeg.org/ffmpeg-utils.html#color-syntax)。<br><br><br>* > 不透明度值越大，透明度越低。<br><br><br>* > 当不透明度指定为十进制时，有效范围为 `[0,1]`，最多支持两位小数。<br> |
|Alignment |Integer |否 |`0` |译文字幕对齐方式。默认值：`0`。有效值：<br><br><br>* `0`：居中对齐。<br><br>* `1`：左对齐。<br><br>* `2`：右对齐。 |
|MaxRowNumber |Integer |否 |`2` |译文字幕的最大行数。默认值：`0`。有效值：<br><br><br>* `0`：根据字幕总字符数和每行最大字符数自动换行，确保完整显示。<br><br>* `1`：每种语言最多显示一行。内容可能被截断。<br><br>* `2`：每种语言最多显示两行。内容可能被截断。<br><br><br>> **说明**<br><br><br>> 源字幕和译文字幕的行数限制会分别计算。<br> |
|MaxCharNumber |Integer |否 |`60` |译文字幕每行最大字符数。默认值：`60`。推荐值：`60`。<br><br>> **说明**<br><br><br><br>* > 系统会基于此参数、`MarginLr`、`Font`、`FontSize`、屏幕分辨率等因素，计算最终每行可显示的最大字符数。<br><br><br>* > 每个中文字符、字母、符号或数字均计为一个字符。<br><br><br>* > 当 `MaxRowNumber` 设置为 `1` 或 `2` 时，如果译文字幕总字符数超出显示范围，内容会被截断。例如，如果每行最大字符数为 10，且 `MaxRowNumber` 为 `2`，则第 20 个字符之后的内容会被截断<br> |
|Hidden |Boolean |否 |`false` |是否隐藏译文字幕。默认值：`false`。有效值：<br><br><br>* `true`：隐藏译文字幕。<br><br>* `false`：显示译文字幕。 |
|ShowPriority |Integer |否 |`100` |译文字幕的显示优先级。默认情况下，源字幕显示在译文字幕上方。值越大表示优先级越高。例如，如果源字幕的 `ShowPriority` 为 `1`，译文字幕的 `ShowPriority` 为 `2`，则译文字幕显示在源字幕上方。 |
|Box |[Box](https://docs.byteplus.com/en/docs/24/118396#box) 对象 |否 |`-` |译文字幕的字体背景。 |
|Border |[Border](https://docs.byteplus.com/en/docs/24/118396#border) 对象 |否 |`-` |译文字幕的字体阴影。 |

### Box

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|W |Float |是 |`1.0` |宽度，单位为 px。推荐范围：`[1,10]`。 |
|Color |String |是 |`0xFF0000@0.5` |颜色。您可以通过以下任一方式指定颜色：<br><br><br>* 以 `0x` 或 `#` 开头，后跟十六进制 RGB 颜色值，并使用 `@` 追加不透明度。不透明度支持 `0x80` 等十六进制值，以及 `0.5` 等十进制值。例如，要指定 50% 不透明度的红色（`FF0000`），请传入 `0xFF0000@0x80`、`0xFF0000@0.5`、`#FF0000@0x80` 或 `#FF0000@0.5`。<br><br>* 使用 FFmpeg 颜色关键字，并使用 `@` 追加不透明度。不透明度支持 `0.5` 等十进制值。例如，要指定 50% 不透明度的 `0xF0F8FF`，请传入 `AliceBlue@0.5`。<br><br><br>> **说明**<br><br><br><br>* > 有关颜色定义和更多颜色关键字，请参见 [FFmpeg 颜色语法](https://ffmpeg.org/ffmpeg-utils.html#color-syntax)。<br><br><br>* > 不透明度值越大，透明度越低。<br><br><br>* > 当不透明度指定为十进制时，有效范围为 `[0,1]`，最多支持两位小数。<br> |

### Border

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|W |Float |是 |`1.0` |宽度，单位为 px。推荐范围：`[1,10]`。 |
|Color |String |是 |`0xFF0000@0.5` |颜色。您可以通过以下任一方式指定颜色：<br><br><br>* 以 `0x` 或 `#` 开头，后跟十六进制 RGB 颜色值，并使用 `@` 追加不透明度。不透明度支持 `0x80` 等十六进制值，以及 `0.5` 等十进制值。例如，要指定 50% 不透明度的红色（`FF0000`），请传入 `0xFF0000@0x80`、`0xFF0000@0.5`、`#FF0000@0x80` 或 `#FF0000@0.5`。<br><br>* 使用 FFmpeg 颜色关键字，并使用 `@` 追加不透明度。不透明度支持 `0.5` 等十进制值。例如，要指定 50% 不透明度的 `0xF0F8FF`，请传入 `AliceBlue@0.5`。<br><br><br>> **说明**<br><br><br><br>* > 有关颜色定义和更多颜色关键字，请参见 [FFmpeg 颜色语法](https://ffmpeg.org/ffmpeg-utils.html#color-syntax)。<br><br><br>* > 不透明度值越大，透明度越低。<br><br><br>* > 当不透明度指定为十进制时，有效范围为 `[0,1]`，最多支持两位小数。<br> |

## 响应参数

有关 API 专用的唯一响应参数，请参见下表。更多详情，请参见[请求响应](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)部分。

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|Code |Integer |`0` |状态码。 |
|Message |String |`success` |状态消息。 |
|Data |[Data](https://docs.byteplus.com/en/docs/24/118396#data) 对象 |`-` |任务信息。 |

### Data

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|TaskID |String |`b71c61****24ae4f` |任务 ID。 |

## 示例

### 示例请求

**原文（ASR）字幕（整句展示）**

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

**原文（ASR）字幕（直播展示）**

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

**字幕翻译**

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

**配音音频 + 双语字幕**

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

**配音音频 + 唇形同步 + 双语字幕**

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

### 示例响应

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

## 错误码

有关错误码的更多信息，请参见[通用错误码](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes)。
