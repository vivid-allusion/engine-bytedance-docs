---
title: "CreateSubtitleTranscodePreset"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createsubtitletranscodepreset-2023-zh-CN"
---

调用 `CreateSubtitleTranscodePreset` API 添加字幕配置。添加配置后，观众可以拉取关联该字幕配置的转码流来观看字幕效果，也可以拉取附加字幕后缀的源流来观看。更多信息，请参见[字幕配置](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-manage-subtitle-configuration)。

## 使用场景

请根据您的场景选择合适的功能。

|场景 |推荐功能 |参数配置 |描述 |
|---|---|---|---|
|为直播流提供基础字幕，帮助观众在静音或嘈杂环境中观看。 |原始（ASR）字幕 |* 整句显示：字幕按句显示。将 `SIConfig` 下的 `Enable` 设置为 `true`，将 `Pipe` 设置为 `mix`（仅字幕），并且仅配置 `SourceLanguage`（源字幕），不配置 `TargetLanguage`（翻译字幕）。<br><br>* 直播显示：字幕无需等待句子结束，按字符或单词逐个显示。将 `SIConfig` 下的 `Enable` 设置为 `true`，将 `Pipe` 设置为 `realtime`，并且仅配置 `SourceLanguage`（源字幕），不配置 `TargetLanguage`（翻译字幕）。 |通过语音识别在视频上叠加源字幕。<br><br>> **说明**<br><br><br>> 目前，直播显示仅支持中文字幕和英文字幕。整句显示支持更多语言。<br> |
|实现跨语言文本沟通，触达全球受众。 |字幕翻译 |* AI 配音模式：将 `SIConfig` 下的 `Enable` 设置为 `true`，将 `Pipe` 设置为 `mix`（仅字幕），并配置 `SourceLanguage`（源字幕）和 `TargetLanguage`（翻译字幕）。<br><br>* 仅字幕模式：将 `SIConfig` 下的 `Enable` 设置为 `false`，并配置 `SourceLanguage`（源字幕）和 `TargetLanguage`（翻译字幕）。<br><br><br>> **说明**<br><br><br>> 我们建议使用 AI 配音模式，以获得更好的翻译质量。<br> |通过语音识别在保留原声的同时，在视频上叠加翻译字幕。 |
|提供类似观看配音电影的配音式翻译体验。 |配音音频 |将 `SIConfig` 下的 `Enable` 设置为 `true`，将 `Pipe` 设置为 `si`（AI 配音），将 `SpeakerRecognition` 设置为大于 `0` 的值，并配置 `SourceLanguage`（源字幕）和 `TargetLanguage`（翻译字幕）的 `Language` 字段。 |提供配音音频并替换原声。 |
|提供沉浸式真人口译体验，提升专业感。 |配音音频 + 唇形同步 |将 `SIConfig` 下的 `Enable` 设置为 `true`，将 `Pipe` 设置为 `si`（AI 配音），将 `SpeakerRecognition` 设置为大于 `0` 的值，将 `DigitalHumanMouthShape` 设置为 `true`，并配置 `SourceLanguage`（源字幕）和 `TargetLanguage`（翻译字幕）的 `Language` 字段。 |基于配音音频，AI 技术将说话人的唇部动作与配音音频同步，营造高度逼真的效果。 |

## 要求

* **频率限制**：每个账号每秒 10 次请求。

* **计费**：

   * **字幕费用**：根据字幕任务的**实际运行时长**计费。更多信息，请参见[字幕计费](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-billing-subtitle)。

   * **转码费用**：如果拉取转码流，会产生转码费用。转码根据**实际转码时长**计费。更多信息，请参见[转码计费](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-transcoding)。

* **前提条件**：

   * 确保推流和拉流的域名已添加到同一域名空间下。更多信息，请参见 [CreateDomain](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-dj3h3u96xn)。

   * 已在该域名空间下添加转码配置，以便后续关联。确保要添加的转码配置和字幕配置使用相同的域名空间和 `AppName`。更多信息，请参见 [CreateTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/createtranscodepresetv2023)。

* **直播延迟**：为确保字幕稳定且完整，关联的转码流或附加字幕后缀的源流会引入额外 **15 到 30 秒**的直播延迟。

* **生效时间**：添加、编辑或删除字幕配置后，您必须等待 3 到 5 分钟，并重新推流，变更才会生效。

## HTTP 请求

* 方法：POST

* 接入点：https://open.byteplusapi.com/?Action=CreateSubtitleTranscodePreset&Version=2023\-01\-01

## 请求参数

### 公共参数

调用所有 API 时，除 API 专用参数外，还必须传入[公共参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

### Query

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Action |String |是 |`CreateSubtitleTranscodePreset` |API 操作。 |
|Version |String |是 |`2023-01-01` |该 API 操作的版本。当前版本：2023\-01\-01。 |

### Body 参数

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |推流和拉流域名所属的域名空间。<br><br>您可以通过以下任一方式获取域名空间：<br><br><br>* 调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023)，并使用响应参数 `Vhost` 获取域名空间。<br><br>* 在 MediaLive 控制台的[域名](https://console.byteplus.com/live/main/domain)页面，单击特定域名右侧的**设置**，并从**域名空间**字段获取域名空间。 |
|App |String |是 |`live` |推流地址中的 `AppName`。例如，如果推流地址为 `rtmp://push.example.com/live/test?authinfo`，则 `AppName` 为 `live`。<br><br>> **警告**<br><br><br>> 确保该值与转码配置的 `AppName` 相同。<br> |
|Description |String |否 |`subtitleconfig0001` |字幕配置的描述。 |
|SuffixName |String |是 |`_subtitle` |字幕后缀。您可以将该后缀附加到源流地址，在不更改分辨率或码率的情况下，直接向原始直播流添加字幕、配音音频和其他效果。<br><br>如需自定义后缀，后缀必须以连字符 (\-) 或下划线 ( *) 开头，长度为 1 到 100 个字符，并且可以包含大写字母 (A\-Z)、小写字母 (a\-z)、连字符 (\-) 和下划线 (* )。<br><br>示例：<br><br><br>* 源流地址：`rtmp://pull.example.com/live/test`<br><br>* 字幕流（带字幕、配音音频和其他效果）地址：`rtmp://pull.example.com/live/test_subtitle`。 |
|Suffixes |Array of String |是 |`["_hd","_bd"]` |当前 `AppName` 下的一个或多个转码后缀。这些后缀会为转码流添加字幕、配音音频和其他效果，因此观众在切换清晰度时可以体验这些效果。<br><br>您可以调用 [ListVhostTransCodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/ListVhostTransCodePreset)，并使用 `SuffixName` 获取转码后缀。<br><br>> **警告**<br><br><br>> 一个 `AppName` 下的每个转码后缀只能绑定一个字幕配置。<br><br><br>示例：<br><br><br>* 源流地址：`rtmp://pull.example.com/live/test`<br><br>* 转码流（带字幕、配音音频和其他效果）地址：`rtmp://pull.example.com/live/test_hd` |
|Delay |Integer |否 |`8` |播放延迟，单位为秒，用于为配音音频和字幕翻译预留足够时间。取值范围： `[0,60]`。推荐值因功能而异：<br><br><br>* `si`：<br><br>   * 启用唇形同步、配音音频和字幕： `20`。<br><br>   * 启用配音音频和字幕：`12`。<br><br>* `mix`：<br><br>   * 原始（ASR）字幕整句显示：`15`。<br><br>   * 字幕翻译：`8`。<br><br>* `realtime`（原始（ASR）字幕直播显示）：`2` 或 `3`。<br><br>   有关详细功能配置，请参见 [使用场景](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createsubtitletranscodepreset-2023?lang=en#usage-scenario)。<br><br><br>> **说明**<br><br><br><br>* > 如果字幕早于原声或视频出现，请降低播放延迟，使字幕与原声或视频对齐；反之亦然。<br><br><br>* > 仅当 `SIConfig` 下的 `Enable` 设置为 `true` 时，该参数才生效。<br> |
|DisplayPreset |String |否 |`small` |不推荐使用。用于快速配置的预设效果。<br><br>传入该参数后，系统会自动适配 `Font`、`MaxRowNumber`、`MaxCharNumber` 和 `Position`。`MaxRowNumber`、`MaxCharNumber` 和 `Position` 参数不再生效。默认情况下，该参数为空，表示不使用预设效果。取值：<br><br><br>* `small`：小号字幕。<br><br>* `medium`：中号字幕。<br><br>* `large`：大号字幕。 |
|MaxRowNumber |Integer |否 |`0` |每种语言的最大字幕行数。默认值：`0`。取值：<br><br><br>* `0`：根据字幕总字符数和每行最大字符数自动换行，确保完整显示。<br><br>* `1`：每种语言最多显示一行。内容可能被截断。<br><br>* `2`：每种语言最多显示两行。内容可能被截断。<br><br><br>> **说明**<br><br><br><br>* > 如果传入 `DisplayPreset`，该参数固定为 `0`。<br><br><br>* > 该参数分别作用于源字幕和翻译字幕。源字幕和翻译字幕的行数限制会分别计算。<br> |
|Position |Object of [Position](https://docs.byteplus.com/en/docs/24/106963#position) |否 |`-` |字幕位置。<br><br>> **说明**<br><br><br>> 如果未传入 `DisplayPreset`，该参数必填。如果传入 `DisplayPreset`，该参数不生效。<br> |
|SIConfig |Object of [SIConfig](https://docs.byteplus.com/en/docs/24/106963#siconfig) |否 |`-` |AI 配音模式配置。 |
|SIOutput |Object of [SIOutput](https://docs.byteplus.com/en/docs/24/106963#sioutput) |否 |`-` |输出相关配置。 |
|SourceLanguage |Object of [SourceLanguage](https://docs.byteplus.com/en/docs/24/106963#sourcelanguage) |是 |`-` |源字幕配置。<br><br>> **说明**<br><br><br>> 当 `SIConfig` 下的 `Enable` 设置为 `true` 时，源语言和目标语言必须不同。<br> |
|TargetLanguage |Array of [TargetLanguage](https://docs.byteplus.com/en/docs/24/106963#targetlanguage) |否 |`-` |翻译字幕配置。<br><br>> **说明**<br><br><br><br>* > 目前，每个请求只能传入一种翻译字幕语言。<br><br><br>* > 当 `SIConfig` 下的 `Enable` 设置为 `true` 时，源语言和目标语言必须不同。<br> |
|HotWordList |Array of String |否 |`["MediaLive","LiveCore"]` |热词列表。默认情况下，该参数为空。<br><br>热词必须与源语言匹配。总字符数不能超过 30,000。<br><br>传入产品名称和热门短语等热词，作为语音识别模型的参考。这有助于提高识别准确率，**但热词不一定每次都能被准确识别**。如果使用热词后识别错误仍然存在，您可以使用 `ReplaceMap` 逐一配置可能的识别错误及其正确文本，强制纠正原始（ASR）字幕。<br><br>> **警告**<br><br><br>> 该参数仅对**原始（ASR）字幕**生效。详情请参见 [使用场景](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createsubtitletranscodepreset-2023?lang=en#usage-scenario)。<br> |
|GlossaryWordList |Array of String |否 |`["赛事直播:sports live streaming","实时字幕:real-time subtitles"]` |术语表。默认情况下，该参数为空。<br><br>每个数组元素必须采用 `"原文:译文"` 格式。示例： `["赛事直播:sports live streaming","实时字幕:real-time subtitles"]`。总字符数不能超过 30,000。<br><br>传入专有词汇及期望译文，如品牌名称、人名、产品名称或功能名称，作为翻译模型的参考。这有助于提高专有词汇的翻译准确率，**但期望译文不一定每次都会被使用**。如果使用术语表后误译仍然存在，您可以使用 `ReplaceMap` 逐一配置可能的误译及其正确译文，强制纠正翻译字幕。<br><br>> **警告**<br><br><br><br>* > 原文或译文值不能包含英文逗号 (,)。<br><br><br>* > 该参数仅在配置 `TargetLanguage` 时生效，并且**仅适用于翻译字幕**。<br> |
|ReplaceMap |JSON Map |否 |`{"live core":"LiveCore","media life":"MediaLive"}` |纠正列表。默认情况下，该参数为空。<br><br>配置需要强制纠正的字幕文本。逐一添加可能的误译或识别错误及其正确文本。<br><br>格式为 `"错误文本":"正确文本"`。使用英文逗号 (,) 分隔多个纠正项。每个错误文本或正确文本值长度必须为 1 到 50 个字符。最多可以传入 60 个纠正项。<br><br>当系统匹配到错误文本时，会强制将错误文本替换为正确文本。<br><br><br>* **原始（ASR）字幕**：纠正识别错误。例如，如果 **MediaLive** 被错误识别为 **media life**，可以传入 `{"media life":"MediaLive"}`。<br><br>* **翻译字幕**：纠正误译。**纠正项仅修改翻译字幕，不修改源字幕或配音音频**。例如，如果 **LiveCore** 被误译为 **live core**，可以传入 `{"live core":"LiveCore"}`。<br><br><br>> **警告**<br><br><br><br>* > 错误文本和正确文本值不能包含英文逗号 (,)。<br><br><br>* > `ReplaceMap` 仅匹配文本，不判断上下文。仅当可以明确识别错误文本确实错误时，才使用该参数。不要将错误文本替换为包含该错误文本的文本。例如，如果传入 `{"stream":"live stream"}`，而字幕已正确显示 **live stream**，系统仍会将 **stream** 替换为 **live stream**，导致显示为 **live live stream**。<br> |

### Position

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Relative |String |否 |`top` |字幕在视频中的位置。默认值： `bottom`。取值：<br><br><br>* `top`：在视频顶部显示字幕。<br><br>* `bottom`：在视频底部显示字幕。 |
|MarginVertical |Float |否 |`0.5` |字幕的顶部或底部边距，即字幕到视频顶部或底部边缘的距离。该值为视频高度的百分比。取值范围： `(0, 0.5]`。<br><br><br>* 当 `Relative` 设置为 `top` 时，该参数指定顶部边距。<br><br>* 当 `Relative` 设置为 `bottom` 时，该参数指定底部边距。 |
|MarginHorizontal |Float |否 |`0.2` |字幕的左右边距，即字幕到视频左右边缘的距离。该值为视频宽度的百分比。取值范围： `(0, 0.3]`。 |

### SIConfig

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Enable |Boolean |否 |`false` |是否启用 AI 配音模式。默认值：`false`。取值：<br><br><br>* `true`：启用 AI 配音模式。该模式支持字幕、替换原声的配音音频和唇形同步，以提供沉浸式体验。<br><br>* `false`：禁用 AI 配音模式并启用仅字幕模式。禁用 AI 配音模式后，`SIConfig` 中的其他参数不生效。 |
|Pipe |String |否 |`mix` |AI 配音类型。取值：<br><br><br>* `si`：字幕、配音音频和视频完全同步。支持唇形同步。该模式适用于会议直播等要求强同步和沉浸感的场景。<br><br>* `mix`：仅字幕，包括整句显示的原始（ASR）字幕。<br><br>* `realtime`：直播显示的原始（ASR）字幕。 |
|DigitalHumanMouthShape |Boolean |否 |`false` |是否启用唇形同步。默认值：`false`。取值：<br><br><br>* `true`：启用唇形同步。启用该功能后，说话人的唇部动作会与配音音频同步，使直播更具沉浸感。<br><br>* `false`：禁用唇形同步。<br><br><br>> **说明**<br><br><br><br>* > 仅当 `Pipe` 为空或设置为 `si` 时，该参数才生效。<br><br><br>* > 当该参数设置为 `true` 时，默认启用配音音频。<br> |
|SpeakerRecognition |Integer |否 |`1` |是否启用配音音频。默认情况下，该参数为空。取值：<br><br><br>* 大于 `0` 的值：启用配音音频。启用该功能后，会提供带语音克隆的翻译语音来替换原声。<br><br>* `0`：禁用配音音频。<br><br><br>> **说明**<br><br><br>> 仅当 `Pipe` 为空或设置为 `si` 时，该参数才生效。<br> |
|PipeExtra |String |否 |`{"Separator":{"HandleType":1},"Amix":{"AudioEnhance":false}}` |JSON 字符串格式的额外配置，包括音量平衡、降噪和原声音量。更多信息，请参见 [CreateSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/CreateSpeechTask) 的 `Extra` 参数。<br><br>> **说明**<br><br><br>> 我们建议仅在启用配音音频时传入该参数。有关配音音频配置的详情，请参见 [使用场景](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createsubtitletranscodepreset-2023?lang=en#usage-scenario)。<br> |

### SIOutput

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Sei |Array of String |否 |`["subtitle"]` |如需将字幕写入直播流中的 SEI 消息，请将该参数设置为 `["subtitle"]`。<br><br>> **说明**<br><br><br><br>* > 仅当 `Pipe` 设置为 `si` 或 `mix` 时，该参数才生效。<br><br><br>* > MediaLive 在将字幕写入 SEI 消息时使用 `100` 作为 SEI `type` 值。如果您的推流工具或 App 也会向流中写入自定义 SEI 消息，请避免使用相同的 SEI `type` 值。否则，播放器可能会将自定义数据识别为字幕。<br> |
|Callback |Object of [Callback](https://docs.byteplus.com/en/docs/24/106963#callback) |否 |`-` |回调配置。 |

### SourceLanguage

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Display |Boolean |是 |`true` |是否显示源字幕。取值：<br><br><br>* `true`：显示。源字幕和翻译字幕都会显示。<br><br>* `false`：不显示。仅显示翻译字幕。 |
|Language |String |否 |`zh` |源字幕语言。<br><br><br>* 当 `SIConfig` 下的 `Enable` 值设置为 `true` 并使用 AI 配音模式时，调用 [GetSubtitleTranscodePresetConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSubtitleTranscodePresetConfig)，并使用 `OriginalLang` 获取当前账号可用于字幕翻译和配音音频的语言列表，或使用 `AsrLang` 获取当前账号可用于原始（ASR）字幕的语言列表，然后传入 `Key` 值。<br><br>* 当 `SIConfig` 下的 `Enable` 值设置为 `false` 并使用仅字幕模式时，有效值如下：<br><br>   * `zh`：中英文混合。<br><br>   * `en`：英语。<br><br>   * `ko`：韩语。<br><br>   * `ja`：日语。 |
|ShowPriority |Integer |否 |`2` |源字幕的显示优先级。默认情况下，源字幕显示在翻译字幕上方。值越大，优先级越高。例如，如果源字幕的 `ShowPriority` 为 `1`，翻译字幕的 `ShowPriority` 为 `2`，则翻译字幕显示在源字幕上方。 |
|MaxCharNumber |Integer |否 |`60` |源字幕每行的最大字符数。默认值： `60`。推荐值： `60`。<br><br>> **说明**<br><br><br><br>* > 系统会根据该参数、 `MarginLr`、 `Font`、 `FontSize`、屏幕分辨率和其他因素，计算最终每行可显示的最大字符数。<br><br><br>* > 每个中文字符、字母、符号或数字均计为一个字符。<br><br><br>* > 当 `MaxRowNumber` 设置为 `1` 或 `2` 时，如果源字幕字符总数超出显示范围，内容会被截断。例如，如果每行最大字符数为 10，且 `MaxRowNumber` 为 `2`，则第 20 个字符之后的内容会被截断。<br><br><br>* > 如果未传入 `DisplayPreset`，该参数必填。如果传入 `DisplayPreset`，该参数不生效。<br> |
|Font |String |是 |`siyuanheiti` |源字幕字体。<br><br><br>* 当 `SIConfig` 下的 `Enable` 值设置为 `true` 并使用 AI 配音模式时，调用 [GetSubtitleTranscodePresetConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSubtitleTranscodePresetConfig)，并使用 `Font` 获取当前账号可用字体列表，然后传入 `Key` 值。<br><br>* 当 `SIConfig` 下的 `Enable` 值设置为 `false` 并使用仅字幕模式时，有效值取决于源字幕语言 (`Language`)。<br><br>   * 如果源字幕语言为 `zh`，支持以下字体：<br><br>      * `siyuanheiti`：思源黑体。<br><br>      * `songtixi`：宋体细。<br><br>      * `songticu`：宋体粗。<br><br>      * `heitifan`：繁体黑体。<br><br>      * `kaiti`：楷体。<br><br>   * 如果源字幕语言为 `en`，支持以下字体：<br><br>      * `inter`：Inter。<br><br>      * `roboto`：Roboto。<br><br>      * `opposans`：OPPOSans。<br><br>      * `siyuansongti`：思源宋体。<br><br>      * `montserrat`：Montserrat。<br><br>   * 如果源字幕语言为 `ko` 或 `ja`，支持 `notosans` (Noto Sans)。 |
|FontSize |Integer |否 |`18` |源字幕字号，单位为 px。<br><br>> **说明**<br><br><br>> 如果未传入 `DisplayPreset`，该参数必填。如果传入 `DisplayPreset`，该参数不生效。<br> |
|FontColor |String |否 |`0xFF0000@0.5` |源字幕字体颜色。您可以通过以下任一方式指定颜色：<br><br><br>* 以 `0x` 或 `#` 开头，后跟十六进制 RGB 颜色值，并使用 `@` 附加不透明度。不透明度支持 `0x80` 等十六进制值和 `0.5` 等十进制值。例如，如需指定 50% 不透明度的红色 (`FF0000`)，可传入 `0xFF0000@0x80`、 `0xFF0000@0.5`、 `#FF0000@0x80` 或 `#FF0000@0.5`。<br><br>* 使用 FFmpeg 颜色关键字，并使用 `@` 附加不透明度。不透明度支持 `0.5` 等十进制值。例如，如需指定 50% 不透明度的 `0xF0F8FF`，可传入 `AliceBlue@0.5`。<br><br><br>> **说明**<br><br><br><br>* > 有关颜色定义和更多颜色关键字，请参见 [FFmpeg 颜色语法](https://ffmpeg.org/ffmpeg-utils.html#color-syntax)。<br><br><br>* > 不透明度值越大，透明度越低。<br><br><br>* > 当不透明度指定为小数时，有效范围为 `[0,1]`，最多支持两位小数。<br> |
|Box |Object of [Box](https://docs.byteplus.com/en/docs/24/106963#box) |否 |`-` |源字幕的字体背景。 |
|Border |Object of [Border](https://docs.byteplus.com/en/docs/24/106963#border) |否 |`-` |源字幕的字体阴影。 |

### TargetLanguage

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Language |String |否 |`en` |翻译字幕语言。<br><br><br>* 当 `SIConfig` 下的 `Enable` 值设置为 `true` 并使用 AI 配音模式时，调用 [GetSubtitleTranscodePresetConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSubtitleTranscodePresetConfig)，并使用 `Lang` 获取当前账号可用语言列表，然后传入 `Key` 值。<br><br>* 当 `SIConfig` 下的 `Enable` 值设置为 `false` 并使用仅字幕模式时，有效值如下：<br><br>   * `zh`：中英文混合。<br><br>   * `en`：英语。<br><br>   * `ko`：韩语。<br><br>   * `ja`：日语。 |
|ShowPriority |Integer |否 |`1` |翻译字幕的显示优先级。默认情况下，源字幕显示在翻译字幕上方。值越大，优先级越高。例如，如果源字幕的 `ShowPriority` 为 `1`，翻译字幕的 `ShowPriority` 为 `2`，则翻译字幕显示在源字幕上方。 |
|MaxCharNumber |Integer |否 |`60` |翻译字幕每行的最大字符数。默认值： `60`。推荐值： `60`。<br><br>> **说明**<br><br><br><br>* > 系统会根据该参数、 `MarginLr`、 `Font`、 `FontSize`、屏幕分辨率和其他因素，计算最终每行可显示的最大字符数。<br><br><br>* > 每个中文字符、字母、符号或数字均计为一个字符。<br><br><br>* > 当 `MaxRowNumber` 设置为 `1` 或 `2` 时，如果翻译字幕字符总数超出显示范围，内容会被截断。例如，如果每行最大字符数为 10，且 `MaxRowNumber` 为 `2`，则第 20 个字符之后的内容会被截断。<br><br><br>* > 如果未传入 `DisplayPreset`，该参数必填。如果传入 `DisplayPreset`，该参数不生效。<br> |
|Hidden |Boolean |否 |`false` |是否隐藏翻译字幕。默认值： `false`。取值：<br><br><br>* `true`：隐藏翻译字幕。<br><br>* `false`：显示翻译字幕。 |
|Font |String |是 |`inter` |翻译字幕字体。<br><br><br>* 当 `SIConfig` 下的 `Enable` 值设置为 `true` 并使用 AI 配音模式时，调用 [GetSubtitleTranscodePresetConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSubtitleTranscodePresetConfig)，并使用 `Font` 获取当前账号可用字体列表，然后传入 `Key` 值。<br><br>* 当 `SIConfig` 下的 `Enable` 值设置为 `false` 并使用仅字幕模式时，有效值取决于翻译字幕语言 (`Language`)。<br><br>   * 如果翻译字幕语言为 `zh`，支持以下字体：<br><br>      * `siyuanheiti`：思源黑体。<br><br>      * `songtixi`：宋体细。<br><br>      * `songticu`：宋体粗。<br><br>      * `heitifan`：繁体黑体。<br><br>      * `kaiti`：楷体。<br><br>   * 如果翻译字幕语言为 `en`，支持以下字体：<br><br>      * `inter`：Inter。<br><br>      * `roboto`：Roboto。<br><br>      * `opposans`：OPPOSans。<br><br>      * `siyuansongti`：思源宋体。<br><br>      * `montserrat`：Montserrat。<br><br>   * 如果翻译字幕语言为 `ko` 或 `ja`，支持 `notosans` (Noto Sans)。 |
|FontSize |Integer |否 |`18` |翻译字幕字号，单位为 px。<br><br>> **说明**<br><br><br>> 如果未传入 `DisplayPreset`，该参数必填。如果传入 `DisplayPreset`，该参数不生效。<br> |
|FontColor |String |是 |`0xFF0000@0.5` |翻译字幕字体颜色。您可以通过以下任一方式指定颜色：<br><br><br>* 以 `0x` 或 `#` 开头，后跟十六进制 RGB 颜色值，并使用 `@` 附加不透明度。不透明度支持 `0x80` 等十六进制值和 `0.5` 等十进制值。例如，如需指定 50% 不透明度的红色 (`FF0000`)，可传入 `0xFF0000@0x80`、 `0xFF0000@0.5`、 `#FF0000@0x80` 或 `#FF0000@0.5`。<br><br>* 使用 FFmpeg 颜色关键字，并使用 `@` 附加不透明度。不透明度支持 `0.5` 等十进制值。例如，如需指定 50% 不透明度的 `0xF0F8FF`，可传入 `AliceBlue@0.5`。<br><br><br>> **说明**<br><br><br><br>* > 有关颜色定义和更多颜色关键字，请参见 [FFmpeg 颜色语法](https://ffmpeg.org/ffmpeg-utils.html#color-syntax)。<br><br><br>* > 不透明度值越大，透明度越低。<br><br><br>* > 当不透明度指定为小数时，有效范围为 `[0,1]`，最多支持两位小数。<br> |
|Border |Object of [Border](https://docs.byteplus.com/en/docs/24/106963#border) |否 |`-` |翻译字幕的字体阴影。 |
|Box |Object of [Box](https://docs.byteplus.com/en/docs/24/106963#box) |否 |`-` |翻译字幕的字体背景。 |

### Callback

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Url |String |是 |`https://xxx` |用于接收回调消息的 URL。该 URL 必须以 `http://` 或 `https://` 开头，可公网访问，且包含 1\-100 个字符。有关 AI 配音回调消息的更多信息，请参见 [AI 配音](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-callback-description?lang=en#ai-dubbing)。 |

### Box

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|W |Float |是 |`2` |宽度，单位为 px。推荐范围： `[1,10]`。 |
|Color |String |是 |`0xFF0000@0.5` |颜色。您可以通过以下任一方式指定颜色：<br><br><br>* 以 `0x` 或 `#` 开头，后跟十六进制 RGB 颜色值，并使用 `@` 附加不透明度。不透明度支持 `0x80` 等十六进制值和 `0.5` 等十进制值。例如，如需指定 50% 不透明度的红色 (`FF0000`)，可传入 `0xFF0000@0x80`、 `0xFF0000@0.5`、 `#FF0000@0x80` 或 `#FF0000@0.5`。<br><br>* 使用 FFmpeg 颜色关键字，并使用 `@` 附加不透明度。不透明度支持 `0.5` 等十进制值。例如，如需指定 50% 不透明度的 `0xF0F8FF`，可传入 `AliceBlue@0.5`。<br><br><br>> **说明**<br><br><br><br>* > 有关颜色定义和更多颜色关键字，请参见 [FFmpeg 颜色语法](https://ffmpeg.org/ffmpeg-utils.html#color-syntax)。<br><br><br>* > 不透明度值越大，透明度越低。<br><br><br>* > 当不透明度指定为小数时，有效范围为 `[0,1]`，最多支持两位小数。<br> |

### Border

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Width |Float |是 |`2` |宽度，单位为 px。推荐范围： `[1,10]`。 |
|Color |String |是 |`0xFF0000@0.5` |颜色。您可以通过以下任一方式指定颜色：<br><br><br>* 以 `0x` 或 `#` 开头，后跟十六进制 RGB 颜色值，并使用 `@` 附加不透明度。不透明度支持 `0x80` 等十六进制值和 `0.5` 等十进制值。例如，如需指定 50% 不透明度的红色 (`FF0000`)，可传入 `0xFF0000@0x80`、 `0xFF0000@0.5`、 `#FF0000@0x80` 或 `#FF0000@0.5`。<br><br>* 使用 FFmpeg 颜色关键字，并使用 `@` 附加不透明度。不透明度支持 `0.5` 等十进制值。例如，如需指定 50% 不透明度的 `0xF0F8FF`，可传入 `AliceBlue@0.5`。<br><br><br>> **说明**<br><br><br><br>* > 有关颜色定义和更多颜色关键字，请参见 [FFmpeg 颜色语法](https://ffmpeg.org/ffmpeg-utils.html#color-syntax)。<br><br><br>* > 不透明度值越大，透明度越低。<br><br><br>* > 当不透明度指定为小数时，有效范围为 `[0,1]`，最多支持两位小数。<br> |

## 响应参数

该 API 仅在响应中返回[公共参数](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

## 示例

### 请求示例

**原始（ASR）字幕（整句显示）**

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

**原始（ASR）字幕（直播显示）**

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

**字幕翻译**

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

**配音音频 + 翻译字幕**

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

**配音音频 + 唇形同步 + 翻译字幕**

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

### 响应示例

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

## 错误码

以下是与当前操作相关的错误码。有关其他错误码，请参见 [BytePlus OpenAPI 公共错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。

|状态码 |错误码 |错误消息 |描述 |
|---|---|---|---|
|200 |CommonErr |\- |未分类错误。建议重试。如果仍返回该错误码，请 [联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |\- |输入参数无效或不符合要求。请参照 [请求参数](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createsubtitletranscodepreset-2023#request-parameters) 说明进行检查。 |
|400 |InvalidParam.BindError |Request parameter error, please check input data |参数校验失败。请检查数据类型是否正确。 |
|403 |RequestForbidden |\- |请求被拒绝，因为当前账号下没有请求的资源（资源包括域名空间、域名、App 名称、配置和证书）。 |
|403 |RequestForbidden.AccountIDNotAllow |this AccountID does not have permission to access the corresponding resource, please check the request parameters |请求被拒绝，因为当前账号下没有请求的资源（资源包括域名空间、域名、App 名称、配置和证书）。 |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |视频直播服务未开通或账号欠费，导致账单不可用。请检查服务开通状态和账号欠费状态。 |
|404 |ResourceNotFound |\- |未找到资源（包括域名空间、域名、App 名称、配置和证书）。建议重试。如果仍返回该错误码，请 [联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |an internal error occurred, please contact the administrator. |发生内部错误。请 [联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.Preset |an internal error related to preset occurred, please contact the administrator. |发生与预设相关的内部错误。请 [联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |发生内部错误。请 [联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |发生内部错误。请 [联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
