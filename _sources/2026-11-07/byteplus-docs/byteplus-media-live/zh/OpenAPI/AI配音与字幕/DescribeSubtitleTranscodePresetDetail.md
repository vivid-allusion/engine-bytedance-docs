---
title: "DescribeSubtitleTranscodePresetDetail"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/DescribeSubtitleTranscodePresetDetail-zh-CN"
---

调用 `DescribeSubtitleTranscodePresetDetail` API 查询指定字幕配置的详细信息。

## 要求

**速率限制**：每个账号每秒 10 次请求。

## HTTP 请求

* 方法：POST

* 接入点：https://open.byteplusapi.com/?Action=DescribeSubtitleTranscodePresetDetail&Version=2023\-01\-01

## 请求参数

### 公共参数

调用所有 API 时，除 API 特定参数外，还必须包含[公共参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

### Query

|参数 |数据类型 |是否必选 |示例值 |描述 |
|---|---|---|---|---|
|Action |String |是 |`DescribeSubtitleTranscodePresetDetail` |API 操作。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。当前版本：2023\-01\-01。 |

### Body 参数

|参数 |数据类型 |是否必选 |示例值 |描述 |
|---|---|---|---|---|
|PresetList |String 数组 |是 |`["igx**dqjks","iga**dqjks"]` |字幕配置的名称。您可以调用 [ListVhostSubtitleTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostsubtitletranscodepreset-2023)，并使用返回的 `PresetName` 值获取名称。 |

## 响应参数

有关 API 特定的唯一响应参数，请参见下表。更多详情，请参见[请求响应](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)章节。

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|PresetDetailList |[PresetDetailList](https://docs.byteplus.com/en/docs/24/118395#presetdetaillist) 数组 |`-` |字幕配置的详细信息。 |

### PresetDetailList

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|PresetName |String |`OriginPreset` |字幕配置的名称。 |
|Status |Integer |`1` |已废弃。 |
|Description |String |`subtitleconfig0001` |字幕配置的描述。 |
|SuffixName |String |`_subtitle` |字幕后缀。例如，如果字幕流地址为 `rtmp://pull.example.com/live/test_subtitle`，则字幕后缀为 `_subtitle`。 |
|Delay |Integer |`12` |播放延迟，单位为秒。用于为配音音频和字幕翻译预留足够时间。<br><br>> **说明**<br><br><br><br>* > 如果字幕早于原声或视频出现，请减小播放延迟，使字幕与原声或视频对齐；反之亦然。<br><br><br>* > 仅当 `SIConfig` 下的 `Enable` 设置为 `true` 时，此参数才生效。<br> |
|DisplayPreset |String |`small` |不推荐。用于快速配置的预设效果。<br><br>传入此参数后，系统会自动适配 `Font`、`MaxRowNumber`、`MaxCharNumber` 和 `Position`。`MaxRowNumber`、`MaxCharNumber` 和 `Position` 参数不再生效。有效值：<br><br><br>* `small`：小号字幕。<br><br>* `medium`：中号字幕。<br><br>* `large`：大号字幕。 |
|MaxRowNumber |Integer |`0` |每种语言的最大字幕行数。有效值：<br><br><br>* `0`：根据字幕字符总数和每行最大字符数自动换行，确保完整显示。<br><br>* `1`：每种语言最多显示一行。内容可能被截断。<br><br>* `2`：每种语言最多显示两行。内容可能被截断。<br><br><br>> **说明**<br><br><br><br>* > 如果传入 `DisplayPreset`，此参数固定为 `0`。<br><br><br>* > 此参数分别应用于源字幕和翻译字幕。源字幕和翻译字幕的行数限制分别计算。<br> |
|Position |[Position](https://docs.byteplus.com/en/docs/24/118395#position) 对象 |`-` |字幕位置。<br><br>> **说明**<br><br><br>> 如果传入 `DisplayPreset`，此参数不生效。<br> |
|SIConfig |[SIConfig](https://docs.byteplus.com/en/docs/24/118395#siconfig) 对象 |`-` |AI 配音模式配置。 |
|SourceLanguage |[SourceLanguage](https://docs.byteplus.com/en/docs/24/118395#sourcelanguage) 对象 |`-` |源字幕配置。 |
|TargetLanguage |[TargetLanguage](https://docs.byteplus.com/en/docs/24/118395#targetlanguage) 数组 |`-` |翻译字幕配置。 |
|HotWordList |String 数组 |`["MediaLive","LiveCore"]` |热词列表。<br><br>热词必须与源语言匹配。它们会作为语音识别模型的参考，帮助提高原文（ASR）字幕的识别准确率，**但热词不一定每次都能被准确识别**。<br><br>> **警告**<br><br><br>> 此参数仅对**原文（ASR）字幕**生效。<br> |
|ReplaceMap |JSON Map |`{"live core":"LiveCore","media life":"MediaLive"}` |纠错列表。<br><br>字幕文本的强制替换规则。格式为 `"错误文本":"正确文本"`。当系统匹配到错误文本时，会强制将错误文本替换为正确文本。<br><br><br>* **原文（ASR）字幕**：纠正识别错误。<br><br>* **翻译字幕**：纠正误译。**纠错仅修改翻译字幕，不修改源字幕或配音音频**。 |
|GlossaryWordList |String 数组 |`["赛事直播:sports live streaming","实时字幕:real-time subtitles"]` |术语表。<br><br>每个数组元素必须采用 `"原文:译文"` 格式，用于记录专有词汇和期望译文，例如品牌名称、人名、产品名称或功能名称。术语表条目会作为翻译模型的参考，帮助提高专有词汇的翻译准确率，**但期望译文不一定每次都会被使用**。<br><br>> **警告**<br><br><br>> 此参数仅在配置 `TargetLanguage` 时生效，并且**仅应用于翻译字幕**。<br> |
|CreatedAt |Integer |`1779335505` |字幕配置的创建时间。取值为 Unix 时间戳，单位为秒。 |
|UpdatedAt |Integer |`1779435505` |字幕配置的更新时间。取值为 Unix 时间戳，单位为秒。 |
|SIOutput |[SIOutput](https://docs.byteplus.com/en/docs/24/118395#sioutput) 对象 |`-` |输出相关配置。 |

### Position

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|Relative |String |`bottom` |字幕在视频中的位置。有效值：<br><br><br>* `top`：在视频顶部显示字幕。<br><br>* `bottom`：在视频底部显示字幕。 |
|MarginVertical |Float |`0.5` |字幕的顶部或底部边距，即字幕到视频顶部或底部边缘的距离。取值为视频高度的百分比。有效范围： `(0, 0.5]`。<br><br><br>* 当 `Relative` 设置为 `top` 时，此参数指定顶部边距。<br><br>* 当 `Relative` 设置为 `bottom` 时，此参数指定底部边距。 |
|MarginHorizontal |Float |`0.2` |字幕的左右边距，即字幕到视频左右边缘的距离。取值为视频宽度的百分比。有效范围： `(0, 0.3]`。 |

### SIConfig

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|Enable |Boolean |`true` |是否启用 AI 配音模式。有效值：<br><br><br>* `true`：启用 AI 配音模式。此模式支持字幕、替换原声的配音音频，以及口型同步，提供沉浸式体验。<br><br>* `false`：禁用 AI 配音模式，并启用仅字幕模式。禁用 AI 配音模式后，`SIConfig` 中的其他参数不生效。 |
|Pipe |String |`si` |AI 配音类型。有效值：<br><br><br>* `si`：字幕、配音音频和视频完全同步。支持口型同步。此模式适用于会议直播等需要强同步和沉浸感的场景。<br><br>* `mix`：仅字幕。<br><br>* `realtime`：直播显示中的原文（ASR）字幕。 |
|SpeakerRecognition |Integer |`1` |是否启用配音音频。有效值：<br><br><br>* 大于 `0` 的值：启用配音音频。启用此功能后，会提供带声音克隆的翻译语音，用于替换原声。<br><br>* `0`：禁用配音音频。<br><br><br>> **说明**<br><br><br>> 仅当 `Pipe` 为空或设置为 `si` 时，此参数才生效。<br> |
|DigitalHumanMouthShape |Boolean |`false` |是否启用口型同步。有效值：<br><br><br>* `true`：启用口型同步。启用此功能后，说话人的唇部动作会与配音音频同步，使直播更具沉浸感。<br><br>* `false`：禁用口型同步。<br><br><br>> **说明**<br><br><br><br>* > 仅当 `Pipe` 为空或设置为 `si` 时，此参数才生效。<br><br><br>* > 当此参数设置为 `true` 时，默认启用配音音频。<br> |
|PipeExtra |String |`{"Separator":{"HandleType":1},"Amix":{"AudioEnhance":false}}` |JSON 字符串格式的额外配置，包括音量均衡、降噪和原声音量。更多信息，请参见 [CreateSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/CreateSpeechTask) 的 `Extra` 参数。<br><br>> **说明**<br><br><br>> 仅当 `SpeakerRecognition` 大于 `0`，即启用配音音频时，此参数才生效。<br> |

### SourceLanguage

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|Display |Boolean |`true` |是否显示源字幕。有效值：<br><br><br>* `true`：显示。源字幕和翻译字幕都会显示。<br><br>* `false`：不显示。仅显示翻译字幕。 |
|Language |String |`zh` |源字幕语言。<br><br><br>* 当 `SIConfig` 下的 `Enable` 值设置为 `true` 并使用 AI 配音模式时，您可以调用 [GetSubtitleTranscodePresetConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSubtitleTranscodePresetConfig)，并使用 `OriginalLang` 获取源字幕语言的显示名称，或使用 `AsrLang` 获取原文（ASR）字幕语言的显示名称。<br><br>* 当 `SIConfig` 下的 `Enable` 值设置为 `false` 并使用仅字幕模式时，有效值如下：<br><br>   * `zh`：中英文混合。<br><br>   * `en`：英语。<br><br>   * `ko`：韩语。<br><br>   * `ja`：日语。 |
|ShowPriority |Integer |`2` |源字幕的显示优先级。值越大，优先级越高。例如，如果源字幕的 `ShowPriority` 为 `1`，翻译字幕的 `ShowPriority` 为 `2`，则翻译字幕显示在源字幕上方。 |
|MaxCharNumber |Integer |`60` |源字幕每行的最大字符数。<br><br>> **说明**<br><br><br><br>* > 系统会根据此参数、 `MarginLr`、 `Font`、 `FontSize`、屏幕分辨率和其他因素，计算最终每行可显示的最大字符数。<br><br><br>* > 每个中文字符、字母、符号或数字均计为一个字符。<br><br><br>* > 当 `MaxRowNumber` 设置为 `1` 或 `2` 时，如果源字幕字符总数超过显示范围，内容会被截断。例如，如果每行最大字符数为 10，且 `MaxRowNumber` 为 `2`，则第 20 个字符之后的内容会被截断。<br><br><br>* > 如果传入 `DisplayPreset`，此参数不生效。<br> |
|FontColor |String |`0xFF0000@0.5` |源字幕字体颜色。您可以通过以下任一方式指定颜色：<br><br><br>* 以 `0x` 或 `#` 开头，后跟十六进制 RGB 颜色值，并使用 `@` 追加不透明度。不透明度支持十六进制值（例如 `0x80`）和十进制值（例如 `0.5`）。例如，若要指定 50% 不透明度的红色（`FF0000`），请传入 `0xFF0000@0x80`、 `0xFF0000@0.5`、 `#FF0000@0x80` 或 `#FF0000@0.5`。<br><br>* 使用 FFmpeg 颜色关键字，并使用 `@` 追加不透明度。不透明度支持十进制值，例如 `0.5`。例如，若要指定 50% 不透明度的 `0xF0F8FF`，请传入 `AliceBlue@0.5`。<br><br><br>> **说明**<br><br><br><br>* > 有关颜色定义和更多颜色关键字，请参见 [FFmpeg 颜色语法](https://ffmpeg.org/ffmpeg-utils.html#color-syntax)。<br><br><br>* > 不透明度值越大，透明度越低。<br> |
|Font |String |`siyuanheiti` |源字幕字体。<br><br><br>* 当 `SIConfig` 下的 `Enable` 值设置为 `true` 并使用 AI 配音模式时，您可以调用 [GetSubtitleTranscodePresetConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSubtitleTranscodePresetConfig)，并使用 `Alias` 获取字体的显示名称。<br><br>* 当 `SIConfig` 下的 `Enable` 值设置为 `false` 并使用仅字幕模式时，有效值取决于源字幕语言（`Language`）。<br><br>   * 如果源字幕语言为 `zh`，支持以下字体：<br><br>      * `siyuanheiti`：思源黑体。<br><br>      * `songtixi`：宋体细。<br><br>      * `songticu`：宋体粗。<br><br>      * `heitifan`：黑体繁。<br><br>      * `kaiti`：楷体。<br><br>   * 如果源字幕语言为 `en`，支持以下字体：<br><br>      * `inter`：Inter。<br><br>      * `roboto`：Roboto。<br><br>      * `opposans`：OPPOSans。<br><br>      * `siyuansongti`：思源宋体。<br><br>      * `montserrat`：Montserrat。<br><br>   * 如果源字幕语言为 `ko` 或 `ja`，支持 `notosans` （Noto Sans）。 |
|FontSize |Integer |`18` |源字幕字体大小，单位为 px。<br><br>> **说明**<br><br><br>> 如果传入 `DisplayPreset`，此参数不生效。<br> |
|Border |[Border](https://docs.byteplus.com/en/docs/24/118395#border) 对象 |`-` |源字幕的字体阴影。 |
|Box |[Box](https://docs.byteplus.com/en/docs/24/118395#box) 对象 |`-` |源字幕的字体背景。 |

### TargetLanguage

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|Language |String |`en` |翻译字幕语言。<br><br><br>* 当 `SIConfig` 下的 `Enable` 值设置为 `true` 并使用 AI 配音模式时，您可以调用 [GetSubtitleTranscodePresetConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSubtitleTranscodePresetConfig)，并使用 `Lang` 获取翻译字幕语言的显示名称。<br><br>* 当 `SIConfig` 下的 `Enable` 值设置为 `false` 并使用仅字幕模式时，有效值如下：<br><br>   * `zh`：中英文混合。<br><br>   * `en`：英语。<br><br>   * `ko`：韩语。<br><br>   * `ja`：日语。 |
|ShowPriority |Integer |`1` |翻译字幕的显示优先级。值越大，优先级越高。例如，如果源字幕的 `ShowPriority` 为 `1`，翻译字幕的 `ShowPriority` 为 `2`，则翻译字幕显示在源字幕上方。 |
|MaxCharNumber |Integer |`60` |翻译字幕每行的最大字符数。<br><br>> **说明**<br><br><br><br>* > 系统会根据此参数、 `MarginLr`、 `Font`、 `FontSize`、屏幕分辨率和其他因素，计算最终每行可显示的最大字符数。<br><br><br>* > 每个中文字符、字母、符号或数字均计为一个字符。<br><br><br>* > 当 `MaxRowNumber` 设置为 `1` 或 `2` 时，如果翻译字幕字符总数超过显示范围，内容会被截断。例如，如果每行最大字符数为 10，且 `MaxRowNumber` 为 `2`，则第 20 个字符之后的内容会被截断。<br><br><br>* > 如果传入 `DisplayPreset`，此参数不生效。<br> |
|Hidden |Boolean |`false` |是否隐藏翻译字幕。有效值：<br><br><br>* `true`：隐藏翻译字幕。<br><br>* `false`：显示翻译字幕。 |
|Font |String |`inter` |翻译字幕字体。<br><br><br>* 当 `SIConfig` 下的 `Enable` 值设置为 `true` 并使用 AI 配音模式时，您可以调用 [GetSubtitleTranscodePresetConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSubtitleTranscodePresetConfig)，并使用 `Alias` 获取字体的显示名称。<br><br>* 当 `SIConfig` 下的 `Enable` 值设置为 `false` 并使用仅字幕模式时，有效值取决于翻译字幕语言（`Language`）。<br><br>   * 如果翻译字幕语言为 `zh`，支持以下字体：<br><br>      * `siyuanheiti`：思源黑体。<br><br>      * `songtixi`：宋体细。<br><br>      * `songticu`：宋体粗。<br><br>      * `heitifan`：黑体繁。<br><br>      * `kaiti`：楷体。<br><br>   * 如果翻译字幕语言为 `en`，支持以下字体：<br><br>      * `inter`：Inter。<br><br>      * `roboto`：Roboto。<br><br>      * `opposans`：OPPOSans。<br><br>      * `siyuansongti`：思源宋体。<br><br>      * `montserrat`：Montserrat。<br><br>   * 如果翻译字幕语言为 `ko` 或 `ja`，支持 `notosans` （Noto Sans）。 |
|FontSize |Integer |`18` |翻译字幕字体大小，单位为 px。<br><br>> **说明**<br><br><br>> 如果传入 `DisplayPreset`，此参数不生效。<br> |
|FontColor |String |`0xFF0000@0.5` |翻译字幕字体颜色。您可以通过以下任一方式指定颜色：<br><br><br>* 以 `0x` 或 `#` 开头，后跟十六进制 RGB 颜色值，并使用 `@` 追加不透明度。不透明度支持十六进制值（例如 `0x80`）和十进制值（例如 `0.5`）。例如，若要指定 50% 不透明度的红色（`FF0000`），请传入 `0xFF0000@0x80`、 `0xFF0000@0.5`、 `#FF0000@0x80` 或 `#FF0000@0.5`。<br><br>* 使用 FFmpeg 颜色关键字，并使用 `@` 追加不透明度。不透明度支持十进制值，例如 `0.5`。例如，若要指定 50% 不透明度的 `0xF0F8FF`，请传入 `AliceBlue@0.5`。<br><br><br>> **说明**<br><br><br><br>* > 有关颜色定义和更多颜色关键字，请参见 [FFmpeg 颜色语法](https://ffmpeg.org/ffmpeg-utils.html#color-syntax)。<br><br><br>* > 不透明度值越大，透明度越低。<br> |
|Border |[Border](https://docs.byteplus.com/en/docs/24/118395#border) 对象 |`-` |翻译字幕的字体阴影。 |
|Box |[Box](https://docs.byteplus.com/en/docs/24/118395#box) 对象 |`-` |翻译字幕的字体背景。 |

### SIOutput

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|Sei |String 数组 |`["subtitle"]` |参数值 `["subtitle"]` 表示将字幕写入直播流中的 SEI 消息。<br><br>> **说明**<br><br><br>> 仅当 `Pipe` 设置为 `si` 或 `mix` 时，此参数才生效。<br> |
|Callback |[Callback](https://docs.byteplus.com/en/docs/24/118395#callback) 对象 |`-` |回调配置。 |

### Border

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|Width |Float |`1.0` |宽度，单位为 px。 |
|Color |String |`0xFF0000@0.5` |颜色。您可以通过以下任一方式指定颜色：<br><br><br>* 以 `0x` 或 `#` 开头，后跟十六进制 RGB 颜色值，并使用 `@` 追加不透明度。不透明度支持十六进制值（例如 `0x80`）和十进制值（例如 `0.5`）。例如，若要指定 50% 不透明度的红色（`FF0000`），请传入 `0xFF0000@0x80`、 `0xFF0000@0.5`、 `#FF0000@0x80` 或 `#FF0000@0.5`。<br><br>* 使用 FFmpeg 颜色关键字，并使用 `@` 追加不透明度。不透明度支持十进制值，例如 `0.5`。例如，若要指定 50% 不透明度的 `0xF0F8FF`，请传入 `AliceBlue@0.5`。<br><br><br>> **说明**<br><br><br><br>* > 有关颜色定义和更多颜色关键字，请参见 [FFmpeg 颜色语法](https://ffmpeg.org/ffmpeg-utils.html#color-syntax)。<br><br><br>* > 不透明度值越大，透明度越低。<br> |

### Box

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|W |Float |`2` |宽度，单位为 px。 |
|Color |String |`0xFF0000@0.5` |颜色。您可以通过以下任一方式指定颜色：<br><br><br>* 以 `0x` 或 `#` 开头，后跟十六进制 RGB 颜色值，并使用 `@` 追加不透明度。不透明度支持十六进制值（例如 `0x80`）和十进制值（例如 `0.5`）。例如，若要指定 50% 不透明度的红色（`FF0000`），请传入 `0xFF0000@0x80`、 `0xFF0000@0.5`、 `#FF0000@0x80` 或 `#FF0000@0.5`。<br><br>* 使用 FFmpeg 颜色关键字，并使用 `@` 追加不透明度。不透明度支持十进制值，例如 `0.5`。例如，若要指定 50% 不透明度的 `0xF0F8FF`，请传入 `AliceBlue@0.5`。<br><br><br>> **说明**<br><br><br><br>* > 有关颜色定义和更多颜色关键字，请参见 [FFmpeg 颜色语法](https://ffmpeg.org/ffmpeg-utils.html#color-syntax)。<br><br><br>* > 不透明度值越大，透明度越低。<br> |

### Callback

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|Url |String |`https://xxx` |用于接收回调消息的 URL。有关 AI 配音回调消息的更多信息，请参见 [AI 配音](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-callback-description?lang=en#ai-dubbing)。 |

## 示例

### 示例请求

```json
POST https://open.byteplusapi.com/?Action=DescribeSubtitleTranscodePresetDetail&Version=2023-01-01
{
    "PresetList": [
        "igx**dqjks",
        "iga**dqjks"
    ]
}
```

### 示例响应

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeSubtitleTranscodePresetDetail",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "PresetDetailList": [
            {
                "PresetName": "OriginPreset",
                "Status": 1,
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
                "CreatedAt": 1779335505,
                "UpdatedAt": 1779435505,
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
        ]
    }
}
```

## 错误码

以下为与当前操作相关的错误码。有关其他错误码，请参见 [BytePlus OpenAPI 公共错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。

|状态码 |错误码 |错误消息 |描述 |
|---|---|---|---|
|200 |CommonErr |\- |未分类错误。建议重试。如果仍返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |\- |输入参数无效或不符合要求。请参照[请求参数](https://docs.byteplus.com/en/docs/24/118395#request-parameters)说明进行检查。 |
|400 |InvalidParam.BindError |Request parameter error, please check input data |参数验证失败。请检查数据类型是否正确。 |
|403 |RequestForbidden |\- |请求被拒绝，因为当前账号下没有请求的资源（资源包括域名空间、域名、App 名称、配置和证书）。 |
|403 |RequestForbidden.AccountIDNotAllowed |this AccountID does not have permission to access the corresponding resource, please check the request parameters |请求被拒绝，因为当前账号下没有请求的资源（资源包括域名空间、域名、App 名称、配置和证书）。 |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |视频直播服务尚未启用，或账号欠费，导致账单不可用。请检查服务开通状态和账号欠费状态。 |
|404 |ResourceNotFound |\- |未找到资源（包括域名空间、域名、App 名称、配置和证书）。建议重试。如果仍返回该错误码，请 [联系支持](https://console.byteplus.com/workorder/create)。 |
|404 |ResourceNotFound.VhostNotExist |vhost not found |未找到域名空间（Vhost）。请检查指定的域名空间是否与实际使用的域名空间一致。 |
|500 |InternalError |an internal error occurred, please contact the administrator. |发生内部错误。请 [联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |an internal error related to database occurred, please contact the administrator. |发生与数据库相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.VhostOrDomain |an internal error related to vhost or domain occurred, please contact the administrator. |发生与域名空间（Vhost）或域名（Domain）相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |发生内部错误。请 [联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |发生内部错误。请 [联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
