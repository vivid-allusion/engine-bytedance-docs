---
title: "DescribeSubtitleTranscodePresetDetail"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/DescribeSubtitleTranscodePresetDetail-zh-TW"
---

呼叫 `DescribeSubtitleTranscodePresetDetail` API，查詢特定字幕設定的詳細資料。

## 要求

**速率限制**：每個帳號每秒 10 個請求。

## HTTP 請求

* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=DescribeSubtitleTranscodePresetDetail&Version=2023\-01\-01

## 請求參數

### 公共參數

除 API 專屬參數外，所有 API 都必須使用[公共參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)呼叫。

### 查詢

|參數 |資料類型 |必填 |範例值 |描述 |
|---|---|---|---|---|
|Action |String |是 |`DescribeSubtitleTranscodePresetDetail` |API 操作。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |

### 主體參數

|參數 |資料類型 |必填 |範例值 |描述 |
|---|---|---|---|---|
|PresetList |Array of String |是 |`["igx**dqjks","iga**dqjks"]` |字幕設定的名稱。您可以呼叫 [ListVhostSubtitleTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostsubtitletranscodepreset-2023)，並使用傳回的 `PresetName` 值取得名稱。 |

## 回應參數

如需 API 專屬的唯一回應參數，請參閱下表。如需更多詳細資料，請參閱[請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)章節。

|參數 |資料類型 |範例值 |描述 |
|---|---|---|---|
|PresetDetailList |Array of [PresetDetailList](https://docs.byteplus.com/en/docs/24/118404#presetdetaillist) |`-` |字幕設定的詳細資料。 |

### PresetDetailList

|參數 |資料類型 |範例值 |描述 |
|---|---|---|---|
|PresetName |String |`OriginPreset` |字幕設定的名稱。 |
|Status |Integer |`1` |已棄用。 |
|Description |String |`subtitleconfig0001` |字幕設定的描述。 |
|SuffixName |String |`_subtitle` |字幕尾碼。例如，如果字幕串流位址為 `rtmp://pull.example.com/live/test_subtitle`，字幕尾碼為 `_subtitle`。 |
|Delay |Integer |`12` |播放延遲，單位為秒，用於為配音音訊和字幕翻譯預留足夠時間。<br><br>> **说明**<br><br><br><br>* > 如果字幕早於原始聲音或影片出現，請減少播放延遲，使字幕與原始聲音或影片對齊，反之亦然。<br><br><br>* > 僅當 `SIConfig` 下的 `Enable` 設為 `true` 時，此參數才會生效。<br> |
|DisplayPreset |String |`small` |不建議使用。用於快速設定的預設效果。<br><br>傳入此參數後，系統會自動調整 `Font`、`MaxRowNumber`、`MaxCharNumber` 和 `Position`。`MaxRowNumber`、`MaxCharNumber` 和 `Position` 參數將不再生效。有效值：<br><br><br>* `small`：小尺寸字幕。<br><br>* `medium`：中尺寸字幕。<br><br>* `large`：大尺寸字幕。 |
|MaxRowNumber |Integer |`0` |每種語言的字幕行數上限。有效值：<br><br><br>* `0`：根據字幕字元總數和每行字元數上限自動換行，以確保完整顯示。<br><br>* `1`：每種語言最多顯示一行。內容可能會被截斷。<br><br>* `2`：每種語言最多顯示兩行。內容可能會被截斷。<br><br><br>> **说明**<br><br><br><br>* > 如果傳入 `DisplayPreset`，此參數固定為 `0`。<br><br><br>* > 此參數會分別套用於來源字幕和翻譯字幕。來源字幕與翻譯字幕的行數限制會分別計算。<br> |
|Position |Object of [Position](https://docs.byteplus.com/en/docs/24/118404#position) |`-` |字幕位置。<br><br>> **说明**<br><br><br>> 如果傳入 `DisplayPreset`，此參數不會生效。<br> |
|SIConfig |Object of [SIConfig](https://docs.byteplus.com/en/docs/24/118404#siconfig) |`-` |AI 配音模式設定。 |
|SourceLanguage |Object of [SourceLanguage](https://docs.byteplus.com/en/docs/24/118404#sourcelanguage) |`-` |來源字幕設定。 |
|TargetLanguage |Array of [TargetLanguage](https://docs.byteplus.com/en/docs/24/118404#targetlanguage) |`-` |翻譯字幕設定。 |
|HotWordList |Array of String |`["MediaLive","LiveCore"]` |熱詞清單。<br><br>熱詞必須與來源語言相符，並作為語音辨識模型的參考，以協助提升原文 (ASR) 字幕的辨識準確率，**但熱詞不一定每次都能準確辨識**。<br><br>> **警告**<br><br><br>> 此參數僅對**原文 (ASR) 字幕**生效。<br> |
|ReplaceMap |JSON Map |`{"live core":"LiveCore","media life":"MediaLive"}` |修正清單。<br><br>字幕文字的強制取代規則。格式為 `"incorrect text":"correct text"`。當系統比對到錯誤文字時，會強制將錯誤文字取代為正確文字。<br><br><br>* **原文 (ASR) 字幕**：修正辨識錯誤。<br><br>* **翻譯字幕**：修正誤譯。**修正只會修改翻譯字幕，不會修改來源字幕或配音音訊**。 |
|GlossaryWordList |Array of String |`["赛事直播:sports live streaming","实时字幕:real-time subtitles"]` |詞彙表。<br><br>每個陣列元素都必須採用 `"original text:translation"` 格式，並記錄專有詞彙及預期翻譯，例如品牌名稱、人物名稱、產品名稱或功能名稱。詞彙表項目會作為翻譯模型的參考，以協助提升專有詞彙的翻譯準確率，**但預期翻譯不一定每次都會使用**。<br><br>> **警告**<br><br><br>> 僅當已設定 `TargetLanguage` 時，此參數才會生效，且**僅套用於翻譯字幕**。<br> |
|CreatedAt |Integer |`1779335505` |字幕設定的建立時間。值為秒級 Unix 時間戳記。 |
|UpdatedAt |Integer |`1779435505` |字幕設定的更新時間。值為秒級 Unix 時間戳記。 |
|SIOutput |Object of [SIOutput](https://docs.byteplus.com/en/docs/24/118404#sioutput) |`-` |輸出相關設定。 |

### Position

|參數 |資料類型 |範例值 |描述 |
|---|---|---|---|
|Relative |String |`bottom` |字幕在影片中的位置。有效值：<br><br><br>* `top`：在影片頂部顯示字幕。<br><br>* `bottom`：在影片底部顯示字幕。 |
|MarginVertical |Float |`0.5` |字幕的頂部或底部邊距，即字幕到影片頂部或底部邊緣的距離。值為影片高度的百分比。有效範圍： `(0, 0.5]`。<br><br><br>* 當 `Relative` 設為 `top` 時，此參數指定頂部邊距。<br><br>* 當 `Relative` 設為 `bottom` 時，此參數指定底部邊距。 |
|MarginHorizontal |Float |`0.2` |字幕的左右邊距，即字幕到影片左右邊緣的距離。值為影片寬度的百分比。有效範圍： `(0, 0.3]`。 |

### SIConfig

|參數 |資料類型 |範例值 |描述 |
|---|---|---|---|
|Enable |Boolean |`true` |是否啟用 AI 配音模式。有效值：<br><br><br>* `true`：啟用 AI 配音模式。此模式支援字幕、取代原始聲音的配音音訊，以及唇形同步，提供沉浸式體驗。<br><br>* `false`：停用 AI 配音模式，並啟用僅字幕模式。停用 AI 配音模式後，`SIConfig` 中的其他參數不會生效。 |
|Pipe |String |`si` |AI 配音類型。有效值：<br><br><br>* `si`：字幕、配音音訊和影片完全同步。支援唇形同步。此模式適用於會議直播，以及其他需要高度同步和沉浸感的場景。<br><br>* `mix`：僅字幕。<br><br>* `realtime`：直播顯示中的原文 (ASR) 字幕。 |
|SpeakerRecognition |Integer |`1` |是否啟用配音音訊。有效值：<br><br><br>* 大於 `0` 的值：啟用配音音訊。啟用此功能後，會提供具備聲音克隆的翻譯語音，以取代原始聲音。<br><br>* `0`：停用配音音訊。<br><br><br>> **说明**<br><br><br>> 僅當 `Pipe` 為空或設為 `si` 時，此參數才會生效。<br> |
|DigitalHumanMouthShape |Boolean |`false` |是否啟用唇形同步。有效值：<br><br><br>* `true`：啟用唇形同步。啟用此功能後，說話者的唇部動作會與配音音訊同步，使直播更具沉浸感。<br><br>* `false`：停用唇形同步。<br><br><br>> **说明**<br><br><br><br>* > 僅當 `Pipe` 為空或設為 `si` 時，此參數才會生效。<br><br><br>* > 當此參數設為 `true` 時，預設會啟用配音音訊。<br> |
|PipeExtra |String |`{"Separator":{"HandleType":1},"Amix":{"AudioEnhance":false}}` |JSON 字串格式的額外設定，包括音量平衡、降噪和原始聲音音量。如需更多資訊，請參閱 [CreateSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/CreateSpeechTask) 的 `Extra` 參數。<br><br>> **说明**<br><br><br>> 僅當 `SpeakerRecognition` 大於 `0`，也就是啟用配音音訊時，此參數才會生效。<br> |

### SourceLanguage

|參數 |資料類型 |範例值 |描述 |
|---|---|---|---|
|Display |Boolean |`true` |是否顯示來源字幕。有效值：<br><br><br>* `true`：顯示。將同時顯示來源字幕和翻譯字幕。<br><br>* `false`：不顯示。只會顯示翻譯字幕。 |
|Language |String |`zh` |來源字幕語言。<br><br><br>* 當 `SIConfig` 下的 `Enable` 值設為 `true` 並使用 AI 配音模式時，您可以呼叫 [GetSubtitleTranscodePresetConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSubtitleTranscodePresetConfig)，並使用 `OriginalLang` 取得來源字幕語言的顯示名稱，或使用 `AsrLang` 取得原文 (ASR) 字幕語言的顯示名稱。<br><br>* 當 `SIConfig` 下的 `Enable` 值設為 `false` 並使用僅字幕模式時，有效值如下：<br><br>   * `zh`：中英文混合。<br><br>   * `en`：英文。<br><br>   * `ko`：韓文。<br><br>   * `ja`：日文。 |
|ShowPriority |Integer |`2` |來源字幕的顯示優先順序。值越大表示優先順序越高。例如，如果來源字幕的 `ShowPriority` 為 `1`，且翻譯字幕的 `ShowPriority` 為 `2`，則翻譯字幕會顯示在來源字幕上方。 |
|MaxCharNumber |Integer |`60` |來源字幕每行的字元數上限。<br><br>> **说明**<br><br><br><br>* > 系統會根據此參數、 `MarginLr`、 `Font`、 `FontSize`、螢幕解析度和其他因素，計算最終每行可顯示的字元數上限。<br><br><br>* > 每個中文字元、字母、符號或數字都計為一個字元。<br><br><br>* > 當 `MaxRowNumber` 設為 `1` 或 `2` 時，如果來源字幕字元總數超過顯示範圍，內容會被截斷。例如，如果每行字元數上限為 10，且 `MaxRowNumber` 為 `2`，則第 20 個字元之後的內容會被截斷。<br><br><br>* > 如果傳入 `DisplayPreset`，此參數不會生效。<br> |
|FontColor |String |`0xFF0000@0.5` |來源字幕字型顏色。您可以使用下列其中一種方式指定顏色：<br><br><br>* 以 `0x` 或 `#` 開頭，後接十六進位 RGB 顏色值，並使用 `@` 附加不透明度。不透明度支援十六進位值，例如 `0x80`，以及十進位值，例如 `0.5`。例如，若要指定 50% 不透明度的紅色 (`FF0000`)，請傳入 `0xFF0000@0x80`、 `0xFF0000@0.5`、 `#FF0000@0x80` 或 `#FF0000@0.5`。<br><br>* 使用 FFmpeg 顏色關鍵字，並使用 `@` 附加不透明度。不透明度支援十進位值，例如 `0.5`。例如，若要指定 50% 不透明度的 `0xF0F8FF`，請傳入 `AliceBlue@0.5`。<br><br><br>> **说明**<br><br><br><br>* > 如需顏色定義和更多顏色關鍵字，請參閱 [FFmpeg 顏色語法](https://ffmpeg.org/ffmpeg-utils.html#color-syntax)。<br><br><br>* > 不透明度值越大，表示透明度越低。<br> |
|Font |String |`siyuanheiti` |來源字幕字型。<br><br><br>* 當 `SIConfig` 下的 `Enable` 值設為 `true` 並使用 AI 配音模式時，您可以呼叫 [GetSubtitleTranscodePresetConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSubtitleTranscodePresetConfig)，並使用 `Alias` 取得字型的顯示名稱。<br><br>* 當 `SIConfig` 下的 `Enable` 值設為 `false` 並使用僅字幕模式時，有效值取決於來源字幕語言 (`Language`)。<br><br>   * 如果來源字幕語言為 `zh`，支援下列字型：<br><br>      * `siyuanheiti`：Source Han Sans。<br><br>      * `songtixi`：Songti Light。<br><br>      * `songticu`：Songti Bold。<br><br>      * `heitifan`：Heiti Traditional。<br><br>      * `kaiti`：Kaiti。<br><br>   * 如果來源字幕語言為 `en`，支援下列字型：<br><br>      * `inter`：Inter。<br><br>      * `roboto`：Roboto。<br><br>      * `opposans`：OPPOSans。<br><br>      * `siyuansongti`：Source Han Serif。<br><br>      * `montserrat`：Montserrat。<br><br>   * 如果來源字幕語言為 `ko` 或 `ja`，支援 `notosans` (Noto Sans)。 |
|FontSize |Integer |`18` |來源字幕字型大小，單位為 px。<br><br>> **说明**<br><br><br>> 如果傳入 `DisplayPreset`，此參數不會生效。<br> |
|Border |Object of [Border](https://docs.byteplus.com/en/docs/24/118404#border) |`-` |來源字幕的字型陰影。 |
|Box |Object of [Box](https://docs.byteplus.com/en/docs/24/118404#box) |`-` |來源字幕的字型背景。 |

### TargetLanguage

|參數 |資料類型 |範例值 |描述 |
|---|---|---|---|
|Language |String |`en` |翻譯字幕語言。<br><br><br>* 當 `SIConfig` 下的 `Enable` 值設為 `true` 並使用 AI 配音模式時，您可以呼叫 [GetSubtitleTranscodePresetConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSubtitleTranscodePresetConfig)，並使用 `Lang` 取得翻譯字幕語言的顯示名稱。<br><br>* 當 `SIConfig` 下的 `Enable` 值設為 `false` 並使用僅字幕模式時，有效值如下：<br><br>   * `zh`：中英文混合。<br><br>   * `en`：英文。<br><br>   * `ko`：韓文。<br><br>   * `ja`：日文。 |
|ShowPriority |Integer |`1` |翻譯字幕的顯示優先順序。值越大表示優先順序越高。例如，如果來源字幕的 `ShowPriority` 為 `1`，且翻譯字幕的 `ShowPriority` 為 `2`，則翻譯字幕會顯示在來源字幕上方。 |
|MaxCharNumber |Integer |`60` |翻譯字幕每行的字元數上限。<br><br>> **说明**<br><br><br><br>* > 系統會根據此參數、 `MarginLr`、 `Font`、 `FontSize`、螢幕解析度和其他因素，計算最終每行可顯示的字元數上限。<br><br><br>* > 每個中文字元、字母、符號或數字都計為一個字元。<br><br><br>* > 當 `MaxRowNumber` 設為 `1` 或 `2` 時，如果翻譯字幕字元總數超過顯示範圍，內容會被截斷。例如，如果每行字元數上限為 10，且 `MaxRowNumber` 為 `2`，則第 20 個字元之後的內容會被截斷。<br><br><br>* > 如果傳入 `DisplayPreset`，此參數不會生效。<br> |
|Hidden |Boolean |`false` |是否隱藏翻譯字幕。有效值：<br><br><br>* `true`：隱藏翻譯字幕。<br><br>* `false`：顯示翻譯字幕。 |
|Font |String |`inter` |翻譯字幕字型。<br><br><br>* 當 `SIConfig` 下的 `Enable` 值設為 `true` 並使用 AI 配音模式時，您可以呼叫 [GetSubtitleTranscodePresetConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSubtitleTranscodePresetConfig)，並使用 `Alias` 取得字型的顯示名稱。<br><br>* 當 `SIConfig` 下的 `Enable` 值設為 `false` 並使用僅字幕模式時，有效值取決於翻譯字幕語言 (`Language`)。<br><br>   * 如果翻譯字幕語言為 `zh`，支援下列字型：<br><br>      * `siyuanheiti`：Source Han Sans。<br><br>      * `songtixi`：Songti Light。<br><br>      * `songticu`：Songti Bold。<br><br>      * `heitifan`：Heiti Traditional。<br><br>      * `kaiti`：Kaiti。<br><br>   * 如果翻譯字幕語言為 `en`，支援下列字型：<br><br>      * `inter`：Inter。<br><br>      * `roboto`：Roboto。<br><br>      * `opposans`：OPPOSans。<br><br>      * `siyuansongti`：Source Han Serif。<br><br>      * `montserrat`：Montserrat。<br><br>   * 如果翻譯字幕語言為 `ko` 或 `ja`，支援 `notosans` (Noto Sans)。 |
|FontSize |Integer |`18` |翻譯字幕字型大小，單位為 px。<br><br>> **说明**<br><br><br>> 如果傳入 `DisplayPreset`，此參數不會生效。<br> |
|FontColor |String |`0xFF0000@0.5` |翻譯字幕字型顏色。您可以使用下列其中一種方式指定顏色：<br><br><br>* 以 `0x` 或 `#` 開頭，後接十六進位 RGB 顏色值，並使用 `@` 附加不透明度。不透明度支援十六進位值，例如 `0x80`，以及十進位值，例如 `0.5`。例如，若要指定 50% 不透明度的紅色 (`FF0000`)，請傳入 `0xFF0000@0x80`、 `0xFF0000@0.5`、 `#FF0000@0x80` 或 `#FF0000@0.5`。<br><br>* 使用 FFmpeg 顏色關鍵字，並使用 `@` 附加不透明度。不透明度支援十進位值，例如 `0.5`。例如，若要指定 50% 不透明度的 `0xF0F8FF`，請傳入 `AliceBlue@0.5`。<br><br><br>> **说明**<br><br><br><br>* > 如需顏色定義和更多顏色關鍵字，請參閱 [FFmpeg 顏色語法](https://ffmpeg.org/ffmpeg-utils.html#color-syntax)。<br><br><br>* > 不透明度值越大，表示透明度越低。<br> |
|Border |Object of [Border](https://docs.byteplus.com/en/docs/24/118404#border) |`-` |翻譯字幕的字型陰影。 |
|Box |Object of [Box](https://docs.byteplus.com/en/docs/24/118404#box) |`-` |翻譯字幕的字型背景。 |

### SIOutput

|參數 |資料類型 |範例值 |描述 |
|---|---|---|---|
|Sei |Array of String |`["subtitle"]` |參數值 `["subtitle"]` 表示將字幕寫入直播串流中的 SEI 訊息。<br><br>> **说明**<br><br><br>> 僅當 `Pipe` 設為 `si` 或 `mix` 時，此參數才會生效。<br> |
|Callback |Object of [Callback](https://docs.byteplus.com/en/docs/24/118404#callback) |`-` |回呼設定。 |

### Border

|參數 |資料類型 |範例值 |描述 |
|---|---|---|---|
|Width |Float |`1.0` |寬度，單位為 px。 |
|Color |String |`0xFF0000@0.5` |顏色。您可以使用下列其中一種方式指定顏色：<br><br><br>* 以 `0x` 或 `#` 開頭，後接十六進位 RGB 顏色值，並使用 `@` 附加不透明度。不透明度支援十六進位值，例如 `0x80`，以及十進位值，例如 `0.5`。例如，若要指定 50% 不透明度的紅色 (`FF0000`)，請傳入 `0xFF0000@0x80`、 `0xFF0000@0.5`、 `#FF0000@0x80` 或 `#FF0000@0.5`。<br><br>* 使用 FFmpeg 顏色關鍵字，並使用 `@` 附加不透明度。不透明度支援十進位值，例如 `0.5`。例如，若要指定 50% 不透明度的 `0xF0F8FF`，請傳入 `AliceBlue@0.5`。<br><br><br>> **说明**<br><br><br><br>* > 如需顏色定義和更多顏色關鍵字，請參閱 [FFmpeg 顏色語法](https://ffmpeg.org/ffmpeg-utils.html#color-syntax)。<br><br><br>* > 不透明度值越大，表示透明度越低。<br> |

### Box

|參數 |資料類型 |範例值 |描述 |
|---|---|---|---|
|W |Float |`2` |寬度，單位為 px。 |
|Color |String |`0xFF0000@0.5` |顏色。您可以使用下列其中一種方式指定顏色：<br><br><br>* 以 `0x` 或 `#` 開頭，後接十六進位 RGB 顏色值，並使用 `@` 附加不透明度。不透明度支援十六進位值，例如 `0x80`，以及十進位值，例如 `0.5`。例如，若要指定 50% 不透明度的紅色 (`FF0000`)，請傳入 `0xFF0000@0x80`、 `0xFF0000@0.5`、 `#FF0000@0x80` 或 `#FF0000@0.5`。<br><br>* 使用 FFmpeg 顏色關鍵字，並使用 `@` 附加不透明度。不透明度支援十進位值，例如 `0.5`。例如，若要指定 50% 不透明度的 `0xF0F8FF`，請傳入 `AliceBlue@0.5`。<br><br><br>> **说明**<br><br><br><br>* > 如需顏色定義和更多顏色關鍵字，請參閱 [FFmpeg 顏色語法](https://ffmpeg.org/ffmpeg-utils.html#color-syntax)。<br><br><br>* > 不透明度值越大，表示透明度越低。<br> |

### Callback

|參數 |資料類型 |範例值 |描述 |
|---|---|---|---|
|Url |String |`https://xxx` |用於接收回呼訊息的 URL。如需 AI 配音回呼訊息的更多資訊，請參閱 [AI 配音](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-callback-description?lang=en#ai-dubbing)。 |

## 範例

### 範例請求

```json
POST https://open.byteplusapi.com/?Action=DescribeSubtitleTranscodePresetDetail&Version=2023-01-01
{
    "PresetList": [
        "igx**dqjks",
        "iga**dqjks"
    ]
}
```

### 範例回應

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

## 錯誤碼

以下是與目前操作相關的錯誤碼。如需其他錯誤碼，請參閱 [BytePlus OpenAPI 公共錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。

|狀態碼 |錯誤碼 |錯誤訊息 |描述 |
|---|---|---|---|
|200 |CommonErr |\- |未分類錯誤。建議重試。如果仍傳回此錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |\- |輸入參數無效或不符合要求。請參閱[請求參數](https://docs.byteplus.com/en/docs/24/118404#request-parameters)描述進行檢查。 |
|400 |InvalidParam.BindError |Request parameter error, please check input data |參數驗證失敗。請檢查資料類型是否正確。 |
|403 |RequestForbidden |\- |請求遭拒，因為目前帳號下沒有請求的資源。資源包括域名空間、域名、應用程式名稱、設定和憑證。 |
|403 |RequestForbidden.AccountIDNotAllowed |this AccountID does not have permission to access the corresponding resource, please check the request parameters |請求遭拒，因為目前帳號下沒有請求的資源。資源包括域名空間、域名、應用程式名稱、設定和憑證。 |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |影片直播服務尚未啟用，或帳號欠費，導致帳單不可用。請檢查服務啟用狀態和帳號欠費狀態。 |
|404 |ResourceNotFound |\- |找不到資源。資源包括域名空間、域名、應用程式名稱、設定和憑證。建議重試。如果仍傳回此錯誤碼，請 [聯絡支援](https://console.byteplus.com/workorder/create)。 |
|404 |ResourceNotFound.VhostNotExist |vhost not found |找不到域名空間 (Vhost)。請檢查指定的域名空間是否與實際使用的域名空間相同。 |
|500 |InternalError |an internal error occurred, please contact the administrator. |發生內部錯誤。請 [聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |an internal error related to database occurred, please contact the administrator. |發生與資料庫相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.VhostOrDomain |an internal error related to vhost or domain occurred, please contact the administrator. |發生與域名空間 (Vhost) 或域名 (Domain) 相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |發生內部錯誤。請 [聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |發生內部錯誤。請 [聯絡支援](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |內部服務逾時。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
