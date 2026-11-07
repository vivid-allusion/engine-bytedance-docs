---
title: "UpdateSubtitleTranscodePreset"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatesubtitletranscodepreset-2023-zh-CN"
---

调用 `UpdateSubtitleTranscodePreset` API 更新已添加的字幕配置。

## 使用场景

根据您的场景选择合适的功能。

|场景 |推荐功能 |参数配置 |描述 |
|---|---|---|---|
|为直播流提供基础字幕，帮助观众在静音或嘈杂环境中观看。 |原文（ASR）字幕 |* 整句显示：字幕逐句显示。将 `SIConfig` 下的 `Enable` 设置为 `true`，将 `Pipe` 设置为 `mix`（仅字幕），并且仅配置 `SourceLanguage`（源字幕），不配置 `TargetLanguage`（翻译字幕）。<br><br>* 直播显示：字幕会逐字或逐词显示，无需等待整句结束。将 `SIConfig` 下的 `Enable` 设置为 `true`，将 `Pipe` 设置为 `realtime`，并且仅配置 `SourceLanguage`（源字幕），不配置 `TargetLanguage`（翻译字幕）。 |通过语音识别在视频上叠加源字幕。<br><br>> **说明**<br><br><br>> 目前，直播显示仅支持中文和英文字幕。整句显示支持更多语言。<br> |
|启用跨语言文本沟通，触达全球观众。 |字幕翻译 |* AI Dubbing 模式：将 `SIConfig` 下的 `Enable` 设置为 `true`，将 `Pipe` 设置为 `mix`（仅字幕），并配置 `SourceLanguage`（源字幕）和 `TargetLanguage`（翻译字幕）。<br><br>* Subtitle Only 模式：将 `SIConfig` 下的 `Enable` 设置为 `false`，并配置 `SourceLanguage`（源字幕）和 `TargetLanguage`（翻译字幕）。<br><br><br>> **说明**<br><br><br>> 建议使用 AI Dubbing 模式以获得更好的翻译质量。<br> |通过语音识别在视频上叠加翻译字幕，同时保留原声。 |
|提供类似观看译制片的配音式翻译体验。 |配音音频 |将 `SIConfig` 下的 `Enable` 设置为 `true`，将 `Pipe` 设置为 `si`（AI Dubbing），将 `SpeakerRecognition` 设置为大于 `0` 的值，并配置 `SourceLanguage`（源字幕）和 `TargetLanguage`（翻译字幕）的 `Language` 字段。 |提供配音音频并替换原声。 |
|提供沉浸式人工传译体验，提升专业度。 |配音音频 + 唇形同步 |将 `SIConfig` 下的 `Enable` 设置为 `true`，将 `Pipe` 设置为 `si`（AI Dubbing），将 `SpeakerRecognition` 设置为大于 `0` 的值，将 `DigitalHumanMouthShape` 设置为 `true`，并配置 `SourceLanguage`（源字幕）和 `TargetLanguage`（翻译字幕）的 `Language` 字段。 |基于配音音频，AI 技术会将说话人的唇部动作与配音音频同步，营造高度真实的效果。 |

## 要求

* **频率限制**：每个账号每秒 10 次请求。

* **计费**：

   * **字幕费用**：根据字幕任务的**实际运行时长**计费。更多信息，请参见[字幕计费](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-billing-subtitle)。

   * **转码费用**：如果拉取转码流，将产生转码费用。转码根据**实际转码时长**计费。更多信息，请参见[转码计费](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-transcoding)。

* **直播延迟**：为确保字幕稳定且完整，关联的转码流或追加字幕后缀的源流会引入额外 **15 到 30 秒**的直播延迟。

* **生效时间**：添加、编辑或删除字幕配置后，您必须等待 3 到 5 分钟，并重新推流，变更才会生效。

## HTTP 请求

* 方法：POST

* 接入点：https://open.byteplusapi.com/?Action=UpdateSubtitleTranscodePreset&Version=2023\-01\-01

## 请求参数

### 公共参数

调用所有 API 时，除 API 特定参数外，还必须携带[公共参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

### Query

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Action |String |是 |`UpdateSubtitleTranscodePreset` |API 操作。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。当前版本：2023\-01\-01。 |

### Body 参数

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |域名空间。您可以调用 [ListVhostSubtitleTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostsubtitletranscodepreset-2023) API，获取要更新的字幕配置的 `Vhost` 值。 |
|App |String |是 |`live` |`AppName`。您可以调用 [ListVhostSubtitleTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostsubtitletranscodepreset-2023) API，获取要更新的字幕配置的 `App` 值。 |
|PresetName |String |是 |`OriginPreset` |字幕配置名称。您可以调用 [ListVhostSubtitleTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostsubtitletranscodepreset-2023) API，获取要更新的字幕配置的 `PresetName` 值。 |
|Description |String |否 |`subtitleconfig0001` |字幕配置描述。 |
|Suffixes |String 数组 |否 |`["_hd","_bd"]` |当前 `AppName` 下的一个或多个转码后缀。这些后缀会为转码流添加字幕、配音音频和其他效果，因此观众切换清晰度时可以体验这些效果。<br><br>您可以调用 [ListVhostTransCodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/ListVhostTransCodePreset) 获取 `Suffixes`，然后将其值传入此参数。<br><br>> **警告**<br><br><br>> 一个 `AppName` 下的每个转码后缀只能绑定一个字幕配置。<br><br><br>示例：<br><br><br>* 源流地址：`rtmp://pull.example.com/live/test`<br><br>* 转码流（带字幕、配音音频和其他效果）地址：`rtmp://pull.example.com/live/test_hd` |
|Delay |Integer |否 |`12` |播放延迟，单位为秒，用于为配音音频和字幕翻译预留足够时间。取值范围： `[0,60]`。推荐值因功能而异：<br><br><br>* `si`：<br><br>   * 启用唇形同步、配音音频和字幕： `20`。<br><br>   * 启用配音音频和字幕：`12`。<br><br>* `mix`：<br><br>   * 整句显示的原文（ASR）字幕：`15`。<br><br>   * 字幕翻译：`8`。<br><br>* `realtime`（直播显示的原文（ASR）字幕）：`2` 或 `3`。<br><br>   详细功能配置，请参见 [使用场景](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatesubtitletranscodepreset-2023?lang=en#usage-scenario)。<br><br><br>> **说明**<br><br><br><br>* > 如果字幕早于原声或视频出现，请减小播放延迟，使字幕与原声或视频对齐；反之亦然。<br><br><br>* > 仅当 `SIConfig` 下的 `Enable` 设置为 `true` 时，此参数才会生效。<br> |
|DisplayPreset |String |否 |`small` |不推荐使用。用于快速配置的预设效果。<br><br>传入此参数后，系统会自动适配 `Font`、`MaxRowNumber`、`MaxCharNumber` 和 `Position`。`MaxRowNumber`、`MaxCharNumber` 和 `Position` 参数不再生效。取值如下：<br><br><br>* `small`：小号字幕。<br><br>* `medium`：中号字幕。<br><br>* `large`：大号字幕。 |
|MaxRowNumber |Integer |否 |`0` |每种语言的最大字幕行数。取值如下：<br><br><br>* `0`：根据字幕总字符数和每行最大字符数自动换行，确保完整显示。<br><br>* `1`：每种语言最多显示一行。内容可能被截断。<br><br>* `2`：每种语言最多显示两行。内容可能被截断。<br><br><br>> **说明**<br><br><br><br>* > 如果传入 `DisplayPreset`，此参数固定为 `0`。<br><br><br>* > 此参数分别应用于源字幕和翻译字幕。源字幕和翻译字幕的行数限制分别计算。<br> |
|Position |[Position](https://docs.byteplus.com/en/docs/24/106966#position) 对象 |否 |`-` |字幕位置。<br><br>> **说明**<br><br><br>> 如果未传入 `DisplayPreset`，此参数必填。如果传入 `DisplayPreset`，此参数不生效。<br> |
|SourceLanguage |[SourceLanguage](https://docs.byteplus.com/en/docs/24/106966#sourcelanguage) 对象 |是 |`-` |源字幕配置。<br><br>> **说明**<br><br><br>> 当 `SIConfig` 下的 `Enable` 设置为 `true` 时，源语言和目标语言必须不同。<br> |
|TargetLanguage |[TargetLanguage](https://docs.byteplus.com/en/docs/24/106966#targetlanguage) 数组 |否 |`-` |翻译字幕配置。<br><br>> **说明**<br><br><br><br>* > 目前，每个请求只能传入一种翻译字幕语言。<br><br><br>* > 当 `SIConfig` 下的 `Enable` 设置为 `true` 时，源语言和目标语言必须不同。<br> |
|HotWordList |String 数组 |否 |`["MediaLive","LiveCore"]` |热词列表。此参数默认为空。<br><br>热词必须与源语言匹配。总字符数不能超过 30,000。<br><br>传入产品名称和热门短语等热词，作为语音识别模型的参考。这有助于提升识别准确率，**但热词不一定每次都能被准确识别**。如果使用热词后识别错误仍然存在，您可以使用 `ReplaceMap` 逐一配置可能的识别错误及其正确文本，以强制纠正原文（ASR）字幕。<br><br>> **警告**<br><br><br>> 此参数仅对**原文（ASR）字幕**生效。详情请参见 [使用场景](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatesubtitletranscodepreset-2023?lang=en#usage-scenario)。<br> |
|GlossaryWordList |String 数组 |否 |`["赛事直播:sports live streaming","实时字幕:real-time subtitles"]` |术语表。此参数默认为空。<br><br>每个数组元素的格式必须为 `"original text:translation"`。示例： `["赛事直播:sports live streaming","实时字幕:real-time subtitles"]`。总字符数不能超过 30,000。<br><br>传入专有词汇及期望译文，例如品牌名称、人名、产品名称或功能名称，作为翻译模型的参考。这有助于提升专有词汇的翻译准确率，**但期望译文不一定每次都会被使用**。如果使用术语表后误译仍然存在，您可以使用 `ReplaceMap` 逐一配置可能的误译及其正确译文，以强制纠正翻译字幕。<br><br>> **警告**<br><br><br><br>* > 原文或译文值不能包含英文逗号（,）。<br><br><br>* > 仅当配置 `TargetLanguage` 时，此参数才会生效，并且**仅适用于翻译字幕**。<br> |
|SIConfig |[SIConfig](https://docs.byteplus.com/en/docs/24/106966#siconfig) 对象 |否 |`-` |AI Dubbing 模式配置。 |
|ReplaceMap |JSON Map |否 |`{"live core":"LiveCore","media life":"MediaLive"}` |纠正列表。此参数默认为空。<br><br>配置需要强制纠正的字幕文本。逐一添加可能的误译或识别错误及其正确文本。<br><br>格式为 `"incorrect text":"correct text"`。多个纠正项用英文逗号（,）分隔。每个错误文本或正确文本值的长度必须为 1 到 50 个字符。最多可传入 60 个纠正项。<br><br>当系统匹配到错误文本时，会强制将错误文本替换为正确文本。<br><br><br>* **原文（ASR）字幕**：纠正识别错误。例如，如果 **MediaLive** 被错误识别为 **media life**，您可以传入 `{"media life":"MediaLive"}`。<br><br>* **翻译字幕**：纠正误译。**纠正仅修改翻译字幕，不修改源字幕或配音音频**。例如，如果 **LiveCore** 被误译为 **live core**，您可以传入 `{"live core":"LiveCore"}`。<br><br><br>> **警告**<br><br><br><br>* > 错误文本和正确文本值不能包含英文逗号（,）。<br><br><br>* > `ReplaceMap` 仅匹配文本，不判断上下文。仅当错误文本可以被明确识别为错误时，才使用此参数。不要将错误文本替换为包含该错误文本的文本。例如，如果您传入 `{"stream":"live stream"}`，并且字幕已正确显示 **live stream**，系统仍会将 **stream** 替换为 **live stream**，导致出现 **live live stream**。<br> |
|SIOutput |[SIOutput](https://docs.byteplus.com/en/docs/24/106966#sioutput) 对象 |否 |`-` |输出相关配置。 |

### Position

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Relative |String |否 |`bottom` |字幕在视频中的位置。取值如下：<br><br><br>* `top`：在视频顶部显示字幕。<br><br>* `bottom`：在视频底部显示字幕。 |
|MarginVertical |Float |否 |`0.5` |字幕的顶部或底部边距，即字幕到视频顶部或底部边缘的距离。该值为视频高度的百分比。取值范围： `(0, 0.5]`。<br><br><br>* 当 `Relative` 设置为 `top` 时，此参数表示顶部边距。<br><br>* 当 `Relative` 设置为 `bottom` 时，此参数表示底部边距。 |
|MarginHorizontal |Float |否 |`0.2` |字幕的左右边距，即字幕到视频左右边缘的距离。该值为视频宽度的百分比。取值范围： `(0, 0.3]`。 |

### SourceLanguage

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Display |Boolean |是 |`true` |是否显示源字幕。取值如下：<br><br><br>* `true`：显示。源字幕和翻译字幕都会显示。<br><br>* `false`：不显示。仅显示翻译字幕。 |
|Language |String |否 |`zh` |源字幕语言。<br><br><br>* 当 `SIConfig` 下的 `Enable` 值设置为 `true` 并使用 AI Dubbing 模式时，调用 [GetSubtitleTranscodePresetConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSubtitleTranscodePresetConfig)，使用 `OriginalLang` 获取当前账号可用于字幕翻译和配音音频的语言列表，或使用 `AsrLang` 获取当前账号可用于原文（ASR）字幕的语言列表，然后传入 `Key` 值。<br><br>* 当 `SIConfig` 下的 `Enable` 值设置为 `false` 并使用 Subtitle Only 模式时，有效值如下：<br><br>   * `zh`：中英文混合。<br><br>   * `en`：英语。<br><br>   * `ko`：韩语。<br><br>   * `ja`：日语。 |
|Font |String |是 |`siyuanheiti` |源字幕字体。<br><br><br>* 当 `SIConfig` 下的 `Enable` 值设置为 `true` 并使用 AI Dubbing 模式时，调用 [GetSubtitleTranscodePresetConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSubtitleTranscodePresetConfig)，使用 `Font` 获取当前账号可用的字体列表，然后传入 `Key` 值。<br><br>* 当 `SIConfig` 下的 `Enable` 值设置为 `false` 并使用 Subtitle Only 模式时，有效值取决于源字幕语言（`Language`）。<br><br>   * 如果源字幕语言为 `zh`，支持以下字体：<br><br>      * `siyuanheiti`：思源黑体。<br><br>      * `songtixi`：宋体细。<br><br>      * `songticu`：宋体粗。<br><br>      * `heitifan`：黑体繁。<br><br>      * `kaiti`：楷体。<br><br>   * 如果源字幕语言为 `en`，支持以下字体：<br><br>      * `inter`：Inter。<br><br>      * `roboto`：Roboto。<br><br>      * `opposans`：OPPOSans。<br><br>      * `siyuansongti`：思源宋体。<br><br>      * `montserrat`：Montserrat。<br><br>   * 如果源字幕语言为 `ko` 或 `ja`，支持 `notosans`（Noto Sans）。 |
|FontSize |Integer |否 |`18` |源字幕字体大小，单位为 px。<br><br>> **说明**<br><br><br>> 如果未传入 `DisplayPreset`，此参数必填。如果传入 `DisplayPreset`，此参数不生效。<br> |
|FontColor |String |否 |`0xFF0000@0.5` |源字幕字体颜色。您可以通过以下任一方式指定颜色：<br><br><br>* 以 `0x` 或 `#` 开头，后跟十六进制 RGB 颜色值，并使用 `@` 追加不透明度。不透明度支持 `0x80` 等十六进制值和 `0.5` 等十进制值。例如，要指定 50% 不透明度的红色（`FF0000`），请传入 `0xFF0000@0x80`、 `0xFF0000@0.5`、 `#FF0000@0x80` 或 `#FF0000@0.5`。<br><br>* 使用 FFmpeg 颜色关键字，并使用 `@` 追加不透明度。不透明度支持 `0.5` 等十进制值。例如，要指定 50% 不透明度的 `0xF0F8FF`，请传入 `AliceBlue@0.5`。<br><br><br>> **说明**<br><br><br><br>* > 有关颜色定义和更多颜色关键字，请参见 [FFmpeg 颜色语法](https://ffmpeg.org/ffmpeg-utils.html#color-syntax)。<br><br><br>* > 不透明度值越大，透明度越低。<br><br><br>* > 当不透明度指定为十进制时，取值范围为 `[0,1]`，最多支持两位小数。<br> |
|Border |[Border](https://docs.byteplus.com/en/docs/24/106966#border) 对象 |否 |`-` |源字幕的字体阴影。 |
|Box |[Box](https://docs.byteplus.com/en/docs/24/106966#box) 对象 |否 |`-` |源字幕的字体背景。 |
|MaxCharNumber |Integer |否 |`60` |源字幕每行最大字符数。推荐值： `60`。<br><br>> **说明**<br><br><br><br>* > 系统会根据此参数、 `MarginLr`、 `Font`、 `FontSize`、屏幕分辨率等因素，计算每行最终可显示的最大字符数。<br><br><br>* > 每个中文字符、字母、符号或数字均计为一个字符。<br><br><br>* > 当 `MaxRowNumber` 设置为 `1` 或 `2` 时，如果源字幕总字符数超出显示范围，内容会被截断。例如，如果每行最大字符数为 10，且 `MaxRowNumber` 为 `2`，则第 20 个字符之后的内容会被截断。<br><br><br>* > 如果未传入 `DisplayPreset`，此参数必填。如果传入 `DisplayPreset`，此参数不生效。<br> |
|ShowPriority |Integer |否 |`2` |源字幕的显示优先级。值越大，优先级越高。例如，如果源字幕的 `ShowPriority` 为 `1`，翻译字幕的 `ShowPriority` 为 `2`，则翻译字幕显示在源字幕上方。 |

### TargetLanguage

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Language |String |否 |`en` |翻译字幕语言。<br><br><br>* 当 `SIConfig` 下的 `Enable` 值设置为 `true` 并使用 AI Dubbing 模式时，调用 [GetSubtitleTranscodePresetConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSubtitleTranscodePresetConfig)，使用 `Lang` 获取当前账号可用的语言列表，然后传入 `Key` 值。<br><br>* 当 `SIConfig` 下的 `Enable` 值设置为 `false` 并使用 Subtitle Only 模式时，有效值如下：<br><br>   * `zh`：中英文混合。<br><br>   * `en`：英语。<br><br>   * `ko`：韩语。<br><br>   * `ja`：日语。 |
|Font |String |是 |`inter` |翻译字幕字体。<br><br><br>* 当 `SIConfig` 下的 `Enable` 值设置为 `true` 并使用 AI Dubbing 模式时，调用 [GetSubtitleTranscodePresetConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSubtitleTranscodePresetConfig)，使用 `Font` 获取当前账号可用的字体列表，然后传入 `Key` 值。<br><br>* 当 `SIConfig` 下的 `Enable` 值设置为 `false` 并使用 Subtitle Only 模式时，有效值取决于翻译字幕语言（`Language`）。<br><br>   * 如果翻译字幕语言为 `zh`，支持以下字体：<br><br>      * `siyuanheiti`：思源黑体。<br><br>      * `songtixi`：宋体细。<br><br>      * `songticu`：宋体粗。<br><br>      * `heitifan`：黑体繁。<br><br>      * `kaiti`：楷体。<br><br>   * 如果翻译字幕语言为 `en`，支持以下字体：<br><br>      * `inter`：Inter。<br><br>      * `roboto`：Roboto。<br><br>      * `opposans`：OPPOSans。<br><br>      * `siyuansongti`：思源宋体。<br><br>      * `montserrat`：Montserrat。<br><br>   * 如果翻译字幕语言为 `ko` 或 `ja`，支持 `notosans`（Noto Sans）。 |
|FontSize |Integer |否 |`18` |翻译字幕字体大小，单位为 px。<br><br>> **说明**<br><br><br>> 如果未传入 `DisplayPreset`，此参数必填。如果传入 `DisplayPreset`，此参数不生效。<br> |
|FontColor |String |否 |`0xFF0000@0.5` |翻译字幕字体颜色。您可以通过以下任一方式指定颜色：<br><br><br>* 以 `0x` 或 `#` 开头，后跟十六进制 RGB 颜色值，并使用 `@` 追加不透明度。不透明度支持 `0x80` 等十六进制值和 `0.5` 等十进制值。例如，要指定 50% 不透明度的红色（`FF0000`），请传入 `0xFF0000@0x80`、 `0xFF0000@0.5`、 `#FF0000@0x80` 或 `#FF0000@0.5`。<br><br>* 使用 FFmpeg 颜色关键字，并使用 `@` 追加不透明度。不透明度支持 `0.5` 等十进制值。例如，要指定 50% 不透明度的 `0xF0F8FF`，请传入 `AliceBlue@0.5`。<br><br><br>> **说明**<br><br><br><br>* > 有关颜色定义和更多颜色关键字，请参见 [FFmpeg 颜色语法](https://ffmpeg.org/ffmpeg-utils.html#color-syntax)。<br><br><br>* > 不透明度值越大，透明度越低。<br><br><br>* > 当不透明度指定为十进制时，取值范围为 `[0,1]`，最多支持两位小数。<br> |
|Border |[Border](https://docs.byteplus.com/en/docs/24/106966#border) 对象 |否 |`-` |翻译字幕的字体阴影。 |
|Hidden |Boolean |否 |`false` |是否隐藏翻译字幕。取值如下：<br><br><br>* `true`：隐藏翻译字幕。<br><br>* `false`：显示翻译字幕。 |
|Box |[Box](https://docs.byteplus.com/en/docs/24/106966#box) 对象 |否 |`-` |翻译字幕的字体背景。 |
|MaxCharNumber |Integer |否 |`60` |翻译字幕每行最大字符数。推荐值： `60`。<br><br>> **说明**<br><br><br><br>* > 系统会根据此参数、 `MarginLr`、 `Font`、 `FontSize`、屏幕分辨率等因素，计算每行最终可显示的最大字符数。<br><br><br>* > 每个中文字符、字母、符号或数字均计为一个字符。<br><br><br>* > 当 `MaxRowNumber` 设置为 `1` 或 `2` 时，如果翻译字幕总字符数超出显示范围，内容会被截断。例如，如果每行最大字符数为 10，且 `MaxRowNumber` 为 `2`，则第 20 个字符之后的内容会被截断。<br><br><br>* > 如果未传入 `DisplayPreset`，此参数必填。如果传入 `DisplayPreset`，此参数不生效。<br> |
|ShowPriority |Integer |否 |`1` |翻译字幕的显示优先级。值越大，优先级越高。例如，如果源字幕的 `ShowPriority` 为 `1`，翻译字幕的 `ShowPriority` 为 `2`，则翻译字幕显示在源字幕上方。 |

### SIConfig

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Enable |Boolean |否 |`true` |是否启用 AI Dubbing 模式。取值如下：<br><br><br>* `true`：启用 AI Dubbing 模式。此模式支持字幕、替换原声的配音音频，以及用于沉浸式体验的唇形同步。<br><br>* `false`：禁用 AI Dubbing 模式并启用 Subtitle Only 模式。禁用 AI Dubbing 模式后，`SIConfig` 中的其他参数不生效。 |
|Pipe |String |否 |`si` |AI Dubbing 类型。取值如下：<br><br><br>* `si`：字幕、配音音频和视频完全同步。支持唇形同步。此模式适用于会议直播等需要强同步和沉浸感的场景。<br><br>* `mix`：仅字幕，包括整句显示的原文（ASR）字幕。<br><br>* `realtime`：直播显示的原文（ASR）字幕。 |
|SpeakerRecognition |Integer |否 |`1` |是否启用配音音频。取值如下：<br><br><br>* 大于 `0` 的值：启用配音音频。启用此功能后，将提供带有音色克隆的翻译语音，用于替换原声。<br><br>* `0`：禁用配音音频。<br><br><br>> **说明**<br><br><br>> 仅当 `Pipe` 为空或设置为 `si` 时，此参数才会生效。<br> |
|DigitalHumanMouthShape |Boolean |否 |`false` |是否启用唇形同步。取值如下：<br><br><br>* `true`：启用唇形同步。启用此功能后，说话人的唇部动作会与配音音频同步，使直播更具沉浸感。<br><br>* `false`：禁用唇形同步。<br><br><br>> **说明**<br><br><br><br>* > 仅当 `Pipe` 为空或设置为 `si` 时，此参数才会生效。<br><br><br>* > 当此参数设置为 `true` 时，默认启用配音音频。<br> |
|PipeExtra |String |否 |`{"Separator":{"HandleType":1},"Amix":{"AudioEnhance":false}}` |JSON 字符串格式的额外配置，包括音量平衡、降噪和原声音量。更多信息，请参见 [CreateSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/CreateSpeechTask) 的 `Extra` 参数。<br><br>> **说明**<br><br><br>> 建议仅在启用配音音频时传入此参数。有关配音音频配置的详情，请参见 [使用场景](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatesubtitletranscodepreset-2023?lang=en#usage-scenario)。<br> |

### SIOutput

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Sei |String 数组 |否 |`["subtitle"]` |如需将字幕写入直播流中的 SEI 消息，请将此参数设置为 `["subtitle"]`。<br><br>> **说明**<br><br><br><br>* > 仅当 `Pipe` 设置为 `si` 或 `mix` 时，此参数才会生效。<br><br><br>* > MediaLive 将字幕写入 SEI 消息时使用 `100` 作为 SEI `type` 值。如果您的推流工具或应用也会向流中写入自定义 SEI 消息，请避免使用相同的 SEI `type` 值。否则，播放器可能会将自定义数据识别为字幕。<br> |
|Callback |[Callback](https://docs.byteplus.com/en/docs/24/106966#callback) 对象 |否 |`-` |回调配置。 |

### Border

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Width |Float |是 |`1.0` |宽度，单位为 px。推荐范围： `[1,10]`。 |
|Color |String |是 |`0xFF0000@0.5` |颜色。您可以通过以下任一方式指定颜色：<br><br><br>* 以 `0x` 或 `#` 开头，后跟十六进制 RGB 颜色值，并使用 `@` 追加不透明度。不透明度支持 `0x80` 等十六进制值和 `0.5` 等十进制值。例如，要指定 50% 不透明度的红色（`FF0000`），请传入 `0xFF0000@0x80`、 `0xFF0000@0.5`、 `#FF0000@0x80` 或 `#FF0000@0.5`。<br><br>* 使用 FFmpeg 颜色关键字，并使用 `@` 追加不透明度。不透明度支持 `0.5` 等十进制值。例如，要指定 50% 不透明度的 `0xF0F8FF`，请传入 `AliceBlue@0.5`。<br><br><br>> **说明**<br><br><br><br>* > 有关颜色定义和更多颜色关键字，请参见 [FFmpeg 颜色语法](https://ffmpeg.org/ffmpeg-utils.html#color-syntax)。<br><br><br>* > 不透明度值越大，透明度越低。<br><br><br>* > 当不透明度指定为十进制时，取值范围为 `[0,1]`，最多支持两位小数。<br> |

### Box

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|W |Float |是 |`2` |宽度，单位为 px。推荐范围： `[1,10]`。 |
|Color |String |是 |`0xFF0000@0.5` |颜色。您可以通过以下任一方式指定颜色：<br><br><br>* 以 `0x` 或 `#` 开头，后跟十六进制 RGB 颜色值，并使用 `@` 追加不透明度。不透明度支持 `0x80` 等十六进制值和 `0.5` 等十进制值。例如，要指定 50% 不透明度的红色（`FF0000`），请传入 `0xFF0000@0x80`、 `0xFF0000@0.5`、 `#FF0000@0x80` 或 `#FF0000@0.5`。<br><br>* 使用 FFmpeg 颜色关键字，并使用 `@` 追加不透明度。不透明度支持 `0.5` 等十进制值。例如，要指定 50% 不透明度的 `0xF0F8FF`，请传入 `AliceBlue@0.5`。<br><br><br>> **说明**<br><br><br><br>* > 有关颜色定义和更多颜色关键字，请参见 [FFmpeg 颜色语法](https://ffmpeg.org/ffmpeg-utils.html#color-syntax)。<br><br><br>* > 不透明度值越大，透明度越低。<br><br><br>* > 当不透明度指定为十进制时，取值范围为 `[0,1]`，最多支持两位小数。<br> |

### Callback

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Url |String |是 |`https://xxx` |用于接收回调消息的 URL。URL 必须以 `http://` 或 `https://` 开头，可公网访问，且包含 1\-100 个字符。有关 AI Dubbing 回调消息的更多信息，请参见 [AI Dubbing](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-callback-description?lang=en#ai-dubbing)。 |

## 响应参数

此 API 仅在响应中返回[公共参数](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

## 示例

### 请求示例

**原文（ASR）字幕（整句显示）**

```json
POST https://open.byteplusapi.com/?Action=UpdateSubtitleTranscodePreset&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "App": "live",
    "PresetName": "SubtitlePreset",
    "Description": "Original ASR subtitles - whole-sentence display",
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

**原文（ASR）字幕（直播显示）**

```json
POST https://open.byteplusapi.com/?Action=UpdateSubtitleTranscodePreset&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "App": "live",
    "PresetName": "SubtitlePreset",
    "Description": "Original ASR subtitles - live streaming display",
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
POST https://open.byteplusapi.com/?Action=UpdateSubtitleTranscodePreset&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "App": "live",
    "PresetName": "SubtitlePreset",
    "Description": "Subtitle translation",
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
POST https://open.byteplusapi.com/?Action=UpdateSubtitleTranscodePreset&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "App": "live",
    "PresetName": "SubtitlePreset",
    "Description": "Dubbed audio + translated subtitles",
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
POST https://open.byteplusapi.com/?Action=UpdateSubtitleTranscodePreset&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "App": "live",
    "PresetName": "SubtitlePreset",
    "Description": "Dubbed audio + lip sync + translated subtitles",
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
        "Action": "UpdateSubtitleTranscodePreset",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```

## 错误码

以下是与当前操作相关的错误码。对于其他错误码，请参见 [BytePlus OpenAPI 公共错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。

|状态码 |错误码 |错误消息 |描述 |
|---|---|---|---|
|200 |CommonErr |\- |未分类错误。建议重试。如果仍返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |\- |输入参数无效或不符合要求。请参照[请求参数](https://docs.byteplus.com/en/docs/24/106966#request-parameters)说明进行检查。 |
|400 |InvalidParam.BindError |Request parameter error, please check input data |参数校验失败。请检查数据类型是否正确。 |
|403 |RequestForbidden |\- |请求被拒绝，因为当前账号下没有请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.AccountIDNotAllow |this AccountID does not have permission to access the corresponding resource, please check the request parameters |请求被拒绝，因为当前账号下没有请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |视频直播服务未开通或账号欠费，导致账单不可用。请检查服务开通状态和账号欠费状态。 |
|404 |ResourceNotFound |\- |未找到资源（包括域名空间、域名、应用名称、配置和证书）。建议重试。如果仍返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |an internal error occurred, please contact the administrator. |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.Preset |an internal error related to preset occurred, please contact the administrator. |发生与预设相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
