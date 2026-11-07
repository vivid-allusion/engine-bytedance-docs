---
title: "CreateSubtitleTranscodePreset"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createsubtitletranscodepreset-2023-zh-TW"
---

呼叫 `CreateSubtitleTranscodePreset` API 以新增字幕配置。新增配置後，觀眾可透過拉取關聯字幕配置的轉碼串流，或拉取附加字幕尾碼的原始串流，觀看字幕效果。如需詳細資訊，請參閱[字幕配置](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-manage-subtitle-configuration)。

## 使用情境

根據您的情境選擇適當功能。

|情境 |建議功能 |參數配置 |說明 |
|---|---|---|---|
|為直播串流提供基本字幕，協助觀眾在靜音或嘈雜環境觀看。 |原文 (ASR) 字幕 |* 整句顯示：字幕逐句顯示。將 `SIConfig` 下的 `Enable` 設為 `true`，將 `Pipe` 設為 `mix`（僅字幕），並且只配置 `SourceLanguage`（原始字幕），不配置 `TargetLanguage`（翻譯字幕）。<br><br>* 直播顯示：字幕不等待句子結束，逐字元或逐詞顯示。將 `SIConfig` 下的 `Enable` 設為 `true`，將 `Pipe` 設為 `realtime`，並且只配置 `SourceLanguage`（原始字幕），不配置 `TargetLanguage`（翻譯字幕）。 |使用語音辨識在影片上疊加原始字幕。<br><br>> **说明**<br><br><br>> 目前，直播顯示僅支援中文和英文字幕。整句顯示支援更多語言。<br> |
|啟用跨語言文字溝通，觸及全球觀眾。 |字幕翻譯 |* AI 配音模式：將 `SIConfig` 下的 `Enable` 設為 `true`，將 `Pipe` 設為 `mix`（僅字幕），並配置 `SourceLanguage`（原始字幕）和 `TargetLanguage`（翻譯字幕）。<br><br>* 僅字幕模式：將 `SIConfig` 下的 `Enable` 設為 `false`，並配置 `SourceLanguage`（原始字幕）和 `TargetLanguage`（翻譯字幕）。<br><br><br>> **说明**<br><br><br>> 建議使用 AI 配音模式，以獲得更好的翻譯品質。<br> |使用語音辨識在影片上疊加翻譯字幕，同時保留原聲。 |
|提供配音式翻譯體驗，類似觀看配音電影。 |配音音訊 |將 `SIConfig` 下的 `Enable` 設為 `true`，將 `Pipe` 設為 `si`（AI 配音），將 `SpeakerRecognition` 設為大於 `0` 的值，並配置 `SourceLanguage`（原始字幕）和 `TargetLanguage`（翻譯字幕）的 `Language` 欄位。 |提供配音音訊並取代原聲。 |
|提供沉浸式真人口譯員體驗，提升專業感。 |配音音訊 + 唇形同步 |將 `SIConfig` 下的 `Enable` 設為 `true`，將 `Pipe` 設為 `si`（AI 配音），將 `SpeakerRecognition` 設為大於 `0` 的值，將 `DigitalHumanMouthShape` 設為 `true`，並配置 `SourceLanguage`（原始字幕）和 `TargetLanguage`（翻譯字幕）的 `Language` 欄位。 |基於配音音訊，AI 技術會將說話者的唇部動作與配音音訊同步，產生高度真實的效果。 |

## 要求

* **速率限制**：每個帳號每秒 10 個請求。

* **計費**：

   * **字幕費用**：根據字幕任務的**實際執行時長**計費。如需詳細資訊，請參閱[字幕計費](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-billing-subtitle)。

   * **轉碼費用**：如果您拉取轉碼串流，會產生轉碼費用。轉碼根據**實際轉碼時長**計費。如需詳細資訊，請參閱[轉碼計費](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-transcoding)。

* **先決條件**：

   * 確保用於推流和拉流的網域名稱已新增至同一網域名稱空間下。如需詳細資訊，請參閱 [CreateDomain](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-dj3h3u96xn)。

   * 已在網域名稱空間下新增轉碼配置，以便後續關聯。確保要新增的轉碼配置和字幕配置使用相同的網域名稱空間和 `AppName`。如需詳細資訊，請參閱 [CreateTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/createtranscodepresetv2023)。

* **直播延遲**：為確保字幕穩定且完整，關聯的轉碼串流或附加字幕尾碼的原始串流會引入額外 **15 到 30 秒**的直播延遲。

* **生效時間**：新增、編輯或刪除字幕配置後，您必須等待 3 到 5 分鐘，並重新啟動推流，變更才會生效。

## HTTP 請求

* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=CreateSubtitleTranscodePreset&Version=2023\-01\-01

## 請求參數

### 通用參數

除 API 專屬參數外，所有 API 都必須搭配[通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)呼叫。

### Query

|參數 |資料類型 |必填 |範例值 |說明 |
|---|---|---|---|---|
|Action |String |是 |`CreateSubtitleTranscodePreset` |API 操作。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |

### Body 參數

|參數 |資料類型 |必填 |範例值 |說明 |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |推流和拉流網域所屬的網域名稱空間。<br><br>您可以透過下列任一方式取得網域名稱空間：<br><br><br>* 呼叫 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023)，並使用回應參數 `Vhost` 取得網域名稱空間。<br><br>* 在 MediaLive 控制台的[網域](https://console.byteplus.com/live/main/domain)頁面，按一下特定網域右側的**設定**，並從**網域名稱空間**欄位取得網域名稱空間。 |
|App |String |是 |`live` |推流位址中的 `AppName`。例如，如果推流位址為 `rtmp://push.example.com/live/test?authinfo`，則 `AppName` 為 `live`。<br><br>> **警告**<br><br><br>> 確保此值與轉碼配置的 `AppName` 相同。<br> |
|Description |String |否 |`subtitleconfig0001` |字幕配置的說明。 |
|SuffixName |String |是 |`_subtitle` |字幕尾碼。您可以將此尾碼附加到原始串流位址，直接為原始直播串流新增字幕、配音音訊和其他效果，而不變更解析度或位元率。<br><br>若要自訂尾碼，尾碼必須以連字號 (\-) 或底線 ( *) 開頭，長度為 1 到 100 個字元，且可包含大寫字母 (A\-Z)、小寫字母 (a\-z)、連字號 (\-) 和底線 (* )。<br><br>範例：<br><br><br>* 原始串流位址：`rtmp://pull.example.com/live/test`<br><br>* 字幕串流（含字幕、配音音訊和其他效果）位址：`rtmp://pull.example.com/live/test_subtitle`。 |
|Suffixes |String 陣列 |是 |`["_hd","_bd"]` |目前 `AppName` 下的一個或多個轉碼尾碼。這些尾碼會為轉碼串流新增字幕、配音音訊和其他效果，讓觀眾切換畫質等級時可體驗這些效果。<br><br>您可以呼叫 [ListVhostTransCodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/ListVhostTransCodePreset)，並使用 `SuffixName` 取得轉碼尾碼。<br><br>> **警告**<br><br><br>> `AppName` 下的每個轉碼尾碼只能繫結到一個字幕配置。<br><br><br>範例：<br><br><br>* 原始串流位址：`rtmp://pull.example.com/live/test`<br><br>* 轉碼串流（含字幕、配音音訊和其他效果）位址：`rtmp://pull.example.com/live/test_hd` |
|Delay |Integer |否 |`8` |播放延遲，單位為秒，用於為配音音訊和字幕翻譯預留足夠時間。有效範圍： `[0,60]`。建議值因功能而異：<br><br><br>* `si`：<br><br>   * 已啟用唇形同步、配音音訊和字幕： `20`。<br><br>   * 已啟用配音音訊和字幕：`12`。<br><br>* `mix`：<br><br>   * 整句顯示的原文 (ASR) 字幕：`15`。<br><br>   * 字幕翻譯：`8`。<br><br>* `realtime`（直播顯示的原文 (ASR) 字幕）：`2` 或 `3`。<br><br>   如需詳細功能配置，請參閱 [使用情境](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createsubtitletranscodepreset-2023?lang=en#usage-scenario)。<br><br><br>> **说明**<br><br><br><br>* > 如果字幕早於原聲或影片出現，請降低播放延遲，使字幕與原聲或影片對齊，反之亦然。<br><br><br>* > 只有當 `SIConfig` 下的 `Enable` 設為 `true` 時，此參數才會生效。<br> |
|DisplayPreset |String |否 |`small` |不建議使用。用於快速配置的預設效果。<br><br>傳入此參數後，系統會自動適配 `Font`、`MaxRowNumber`、`MaxCharNumber` 和 `Position`。`MaxRowNumber`、`MaxCharNumber` 和 `Position` 參數不再生效。預設情況下，此參數為空，表示不使用預設效果。有效值：<br><br><br>* `small`：小尺寸字幕。<br><br>* `medium`：中尺寸字幕。<br><br>* `large`：大尺寸字幕。 |
|MaxRowNumber |Integer |否 |`0` |每種語言的字幕列數上限。預設值：`0`。有效值：<br><br><br>* `0`：根據字幕字元總數和每列字元數上限自動換列，以確保完整顯示。<br><br>* `1`：每種語言最多顯示一列。內容可能被截斷。<br><br>* `2`：每種語言最多顯示兩列。內容可能被截斷。<br><br><br>> **说明**<br><br><br><br>* > 如果傳入 `DisplayPreset`，此參數固定為 `0`。<br><br><br>* > 此參數分別套用於原始字幕和翻譯字幕。原始字幕和翻譯字幕的列數限制會分別計算。<br> |
|Position |[Position](https://docs.byteplus.com/en/docs/24/107349#position) 物件 |否 |`-` |字幕位置。<br><br>> **说明**<br><br><br>> 如果未傳入 `DisplayPreset`，此參數為必填。如果傳入 `DisplayPreset`，此參數不生效。<br> |
|SIConfig |[SIConfig](https://docs.byteplus.com/en/docs/24/107349#siconfig) 物件 |否 |`-` |AI 配音模式配置。 |
|SIOutput |[SIOutput](https://docs.byteplus.com/en/docs/24/107349#sioutput) 物件 |否 |`-` |輸出相關配置。 |
|SourceLanguage |[SourceLanguage](https://docs.byteplus.com/en/docs/24/107349#sourcelanguage) 物件 |是 |`-` |原始字幕配置。<br><br>> **说明**<br><br><br>> 當 `SIConfig` 下的 `Enable` 設為 `true` 時，來源語言與目標語言必須不同。<br> |
|TargetLanguage |[TargetLanguage](https://docs.byteplus.com/en/docs/24/107349#targetlanguage) 陣列 |否 |`-` |翻譯字幕配置。<br><br>> **说明**<br><br><br><br>* > 目前，每個請求只能傳入一種翻譯字幕語言。<br><br><br>* > 當 `SIConfig` 下的 `Enable` 設為 `true` 時，來源語言與目標語言必須不同。<br> |
|HotWordList |String 陣列 |否 |`["MediaLive","LiveCore"]` |熱詞清單。此參數預設為空。<br><br>熱詞必須符合來源語言。字元總數不得超過 30,000。<br><br>傳入產品名稱和熱門片語等熱詞，作為語音辨識模型的參考。這有助於提升辨識準確度，**但熱詞不一定每次都能準確辨識**。如果使用熱詞後仍持續發生辨識錯誤，您可以使用 `ReplaceMap` 逐一配置可能的辨識錯誤及其正確文字，以強制更正原文 (ASR) 字幕。<br><br>> **警告**<br><br><br>> 此參數僅對**原文 (ASR) 字幕**生效。如需詳細資訊，請參閱 [使用情境](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createsubtitletranscodepreset-2023?lang=en#usage-scenario)。<br> |
|GlossaryWordList |String 陣列 |否 |`["赛事直播:sports live streaming","实时字幕:real-time subtitles"]` |術語表。此參數預設為空。<br><br>每個陣列元素必須採用 `"original text:translation"` 格式。範例： `["赛事直播:sports live streaming","实时字幕:real-time subtitles"]`。字元總數不得超過 30,000。<br><br>傳入品牌名稱、人名、產品名稱或功能名稱等專有詞彙和預期翻譯，作為翻譯模型的參考。這有助於提升專有詞彙的翻譯準確度，**但預期翻譯不一定每次都會使用**。如果使用術語表後仍持續發生誤譯，您可以使用 `ReplaceMap` 逐一配置可能的誤譯及其正確翻譯，以強制更正翻譯字幕。<br><br>> **警告**<br><br><br><br>* > 原文或翻譯值不得包含英文逗號 (,)。<br><br><br>* > 此參數僅在配置 `TargetLanguage` 時生效，且**僅套用於翻譯字幕**。<br> |
|ReplaceMap |JSON Map |否 |`{"live core":"LiveCore","media life":"MediaLive"}` |更正清單。此參數預設為空。<br><br>配置需要強制更正的字幕文字。逐一新增可能的誤譯或辨識錯誤及其正確文字。<br><br>格式為 `"incorrect text":"correct text"`。使用英文逗號 (,) 分隔多個更正項目。每個錯誤文字或正確文字值的長度必須為 1 到 50 個字元。最多可傳入 60 個更正項目。<br><br>當系統比對到錯誤文字時，會強制以正確文字取代錯誤文字。<br><br><br>* **原文 (ASR) 字幕**：更正辨識錯誤。例如，如果 **MediaLive** 被錯誤辨識為 **media life**，您可以傳入 `{"media life":"MediaLive"}`。<br><br>* **翻譯字幕**：更正誤譯。**更正只會修改翻譯字幕，不會修改原始字幕或配音音訊**。例如，如果 **LiveCore** 被誤譯為 **live core**，您可以傳入 `{"live core":"LiveCore"}`。<br><br><br>> **警告**<br><br><br><br>* > 錯誤文字和正確文字值不得包含英文逗號 (,)。<br><br><br>* > `ReplaceMap` 只比對文字，不判斷上下文。只有在可明確判定錯誤文字為錯誤時，才使用此參數。請勿將錯誤文字取代為包含該錯誤文字的文字。例如，如果您傳入 `{"stream":"live stream"}`，而字幕已正確顯示 **live stream**，系統仍會將 **stream** 取代為 **live stream**，導致顯示 **live live stream**。<br> |

### Position

|參數 |資料類型 |必填 |範例值 |說明 |
|---|---|---|---|---|
|Relative |String |否 |`top` |字幕在影片中的位置。預設值： `bottom`。有效值：<br><br><br>* `top`：在影片頂部顯示字幕。<br><br>* `bottom`：在影片底部顯示字幕。 |
|MarginVertical |Float |否 |`0.5` |字幕的上邊距或下邊距，即字幕到影片頂部或底部邊緣的距離。此值為影片高度的百分比。有效範圍： `(0, 0.5]`。<br><br><br>* 當 `Relative` 設為 `top` 時，此參數指定上邊距。<br><br>* 當 `Relative` 設為 `bottom` 時，此參數指定下邊距。 |
|MarginHorizontal |Float |否 |`0.2` |字幕的左右邊距，即字幕到影片左右邊緣的距離。此值為影片寬度的百分比。有效範圍： `(0, 0.3]`。 |

### SIConfig

|參數 |資料類型 |必填 |範例值 |說明 |
|---|---|---|---|---|
|Enable |Boolean |否 |`false` |是否啟用 AI 配音模式。預設值：`false`。有效值：<br><br><br>* `true`：啟用 AI 配音模式。此模式支援字幕、取代原聲的配音音訊，以及提供沉浸式體驗的唇形同步。<br><br>* `false`：停用 AI 配音模式並啟用僅字幕模式。停用 AI 配音模式後，`SIConfig` 中的其他參數不生效。 |
|Pipe |String |否 |`mix` |AI 配音類型。有效值：<br><br><br>* `si`：字幕、配音音訊和影片完全同步。支援唇形同步。此模式適用於會議直播等需要強同步和沉浸感的情境。<br><br>* `mix`：僅字幕，包括整句顯示的原文 (ASR) 字幕。<br><br>* `realtime`：直播顯示的原文 (ASR) 字幕。 |
|DigitalHumanMouthShape |Boolean |否 |`false` |是否啟用唇形同步。預設值：`false`。有效值：<br><br><br>* `true`：啟用唇形同步。啟用此功能後，說話者的唇部動作會與配音音訊同步，使直播更具沉浸感。<br><br>* `false`：停用唇形同步。<br><br><br>> **说明**<br><br><br><br>* > 此參數僅在 `Pipe` 為空或設為 `si` 時生效。<br><br><br>* > 當此參數設為 `true` 時，預設啟用配音音訊。<br> |
|SpeakerRecognition |Integer |否 |`1` |是否啟用配音音訊。此參數預設為空。有效值：<br><br><br>* 大於 `0` 的值：啟用配音音訊。啟用此功能後，會提供使用聲音複製的翻譯語音，以取代原聲。<br><br>* `0`：停用配音音訊。<br><br><br>> **说明**<br><br><br>> 此參數僅在 `Pipe` 為空或設為 `si` 時生效。<br> |
|PipeExtra |String |否 |`{"Separator":{"HandleType":1},"Amix":{"AudioEnhance":false}}` |JSON 字串格式的額外配置，包括音量平衡、降噪和原聲音量。如需詳細資訊，請參閱 [CreateSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/CreateSpeechTask) 的 `Extra` 參數。<br><br>> **说明**<br><br><br>> 建議僅在啟用配音音訊時傳入此參數。如需配音音訊配置的詳細資訊，請參閱 [使用情境](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createsubtitletranscodepreset-2023?lang=en#usage-scenario)。<br> |

### SIOutput

|參數 |資料類型 |必填 |範例值 |說明 |
|---|---|---|---|---|
|Sei |String 陣列 |否 |`["subtitle"]` |若要將字幕寫入直播串流中的 SEI 訊息，請將此參數設為 `["subtitle"]`。<br><br>> **说明**<br><br><br><br>* > 此參數僅在 `Pipe` 設為 `si` 或 `mix` 時生效。<br><br><br>* > MediaLive 將字幕寫入 SEI 訊息時，使用 `100` 作為 SEI `type` 值。如果您的推流工具或應用程式也將自訂 SEI 訊息寫入串流，請避免使用相同的 SEI `type` 值。否則，播放器可能會將自訂資料識別為字幕。<br> |
|Callback |[Callback](https://docs.byteplus.com/en/docs/24/107349#callback) 物件 |否 |`-` |回呼配置。 |

### SourceLanguage

|參數 |資料類型 |必填 |範例值 |說明 |
|---|---|---|---|---|
|Display |Boolean |是 |`true` |是否顯示原始字幕。有效值：<br><br><br>* `true`：顯示。原始字幕和翻譯字幕都會顯示。<br><br>* `false`：不顯示。只會顯示翻譯字幕。 |
|Language |String |否 |`zh` |原始字幕語言。<br><br><br>* 當 `SIConfig` 下的 `Enable` 值設為 `true` 且使用 AI 配音模式時，呼叫 [GetSubtitleTranscodePresetConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSubtitleTranscodePresetConfig)，並使用 `OriginalLang` 取得目前帳號可用於字幕翻譯和配音音訊的語言清單，或使用 `AsrLang` 取得目前帳號可用於原文 (ASR) 字幕的語言清單，然後傳入 `Key` 值。<br><br>* 當 `SIConfig` 下的 `Enable` 值設為 `false` 且使用僅字幕模式時，有效值如下：<br><br>   * `zh`：中英文混合。<br><br>   * `en`：英文。<br><br>   * `ko`：韓文。<br><br>   * `ja`：日文。 |
|ShowPriority |Integer |否 |`2` |原始字幕的顯示優先順序。預設情況下，原始字幕會顯示在翻譯字幕上方。值越大表示優先順序越高。例如，如果原始字幕的 `ShowPriority` 為 `1`，翻譯字幕的 `ShowPriority` 為 `2`，則翻譯字幕會顯示在原始字幕上方。 |
|MaxCharNumber |Integer |否 |`60` |原始字幕每列的字元數上限。預設值： `60`。建議值： `60`。<br><br>> **说明**<br><br><br><br>* > 系統會根據此參數、 `MarginLr`、 `Font`、 `FontSize`、螢幕解析度和其他因素，計算最終每列可顯示字元數上限。<br><br><br>* > 每個中文字元、字母、符號或數字都計為一個字元。<br><br><br>* > 當 `MaxRowNumber` 設為 `1` 或 `2` 時，如果原始字幕字元總數超過顯示範圍，內容會被截斷。例如，如果每列字元數上限為 10，且 `MaxRowNumber` 為 `2`，則第 20 個字元之後的內容會被截斷。<br><br><br>* > 如果未傳入 `DisplayPreset`，此參數為必填。如果傳入 `DisplayPreset`，此參數不生效。<br> |
|Font |String |是 |`siyuanheiti` |原始字幕字型。<br><br><br>* 當 `SIConfig` 下的 `Enable` 值設為 `true` 且使用 AI 配音模式時，呼叫 [GetSubtitleTranscodePresetConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSubtitleTranscodePresetConfig)，並使用 `Font` 取得目前帳號可用的字型清單，然後傳入 `Key` 值。<br><br>* 當 `SIConfig` 下的 `Enable` 值設為 `false` 且使用僅字幕模式時，有效值取決於原始字幕語言 (`Language`)。<br><br>   * 如果原始字幕語言為 `zh`，支援下列字型：<br><br>      * `siyuanheiti`：Source Han Sans。<br><br>      * `songtixi`：Songti Light。<br><br>      * `songticu`：Songti Bold。<br><br>      * `heitifan`：Heiti Traditional。<br><br>      * `kaiti`：Kaiti。<br><br>   * 如果原始字幕語言為 `en`，支援下列字型：<br><br>      * `inter`：Inter。<br><br>      * `roboto`：Roboto。<br><br>      * `opposans`：OPPOSans。<br><br>      * `siyuansongti`：Source Han Serif。<br><br>      * `montserrat`：Montserrat。<br><br>   * 如果原始字幕語言為 `ko` 或 `ja`，支援 `notosans` (Noto Sans)。 |
|FontSize |Integer |否 |`18` |原始字幕字型大小，單位為 px。<br><br>> **说明**<br><br><br>> 如果未傳入 `DisplayPreset`，此參數為必填。如果傳入 `DisplayPreset`，此參數不生效。<br> |
|FontColor |String |否 |`0xFF0000@0.5` |原始字幕字型顏色。您可以透過下列任一方式指定顏色：<br><br><br>* 以 `0x` 或 `#` 開頭，後接十六進位 RGB 色彩值，並使用 `@` 附加不透明度。不透明度支援十六進位值，例如 `0x80`，以及十進位值，例如 `0.5`。例如，若要指定紅色 (`FF0000`) 且不透明度為 50%，請傳入 `0xFF0000@0x80`、 `0xFF0000@0.5`、 `#FF0000@0x80` 或 `#FF0000@0.5`。<br><br>* 使用 FFmpeg 色彩關鍵字，並使用 `@` 附加不透明度。不透明度支援十進位值，例如 `0.5`。例如，若要指定 `0xF0F8FF` 且不透明度為 50%，請傳入 `AliceBlue@0.5`。<br><br><br>> **说明**<br><br><br><br>* > 如需色彩定義和更多色彩關鍵字，請參閱 [FFmpeg 色彩語法](https://ffmpeg.org/ffmpeg-utils.html#color-syntax)。<br><br><br>* > 不透明度值越大，表示透明度越低。<br><br><br>* > 當不透明度指定為十進位時，有效範圍為 `[0,1]`，最多支援兩位小數。<br> |
|Box |[Box](https://docs.byteplus.com/en/docs/24/107349#box) 物件 |否 |`-` |原始字幕的字型背景。 |
|Border |[Border](https://docs.byteplus.com/en/docs/24/107349#border) 物件 |否 |`-` |原始字幕的字型陰影。 |

### TargetLanguage

|參數 |資料類型 |必填 |範例值 |說明 |
|---|---|---|---|---|
|Language |String |否 |`en` |翻譯字幕語言。<br><br><br>* 當 `SIConfig` 下的 `Enable` 值設為 `true` 且使用 AI 配音模式時，呼叫 [GetSubtitleTranscodePresetConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSubtitleTranscodePresetConfig)，並使用 `Lang` 取得目前帳號可用的語言清單，然後傳入 `Key` 值。<br><br>* 當 `SIConfig` 下的 `Enable` 值設為 `false` 且使用僅字幕模式時，有效值如下：<br><br>   * `zh`：中英文混合。<br><br>   * `en`：英文。<br><br>   * `ko`：韓文。<br><br>   * `ja`：日文。 |
|ShowPriority |Integer |否 |`1` |翻譯字幕的顯示優先順序。預設情況下，原始字幕會顯示在翻譯字幕上方。值越大表示優先順序越高。例如，如果原始字幕的 `ShowPriority` 為 `1`，翻譯字幕的 `ShowPriority` 為 `2`，則翻譯字幕會顯示在原始字幕上方。 |
|MaxCharNumber |Integer |否 |`60` |翻譯字幕每列的字元數上限。預設值： `60`。建議值： `60`。<br><br>> **说明**<br><br><br><br>* > 系統會根據此參數、 `MarginLr`、 `Font`、 `FontSize`、螢幕解析度和其他因素，計算最終每列可顯示字元數上限。<br><br><br>* > 每個中文字元、字母、符號或數字都計為一個字元。<br><br><br>* > 當 `MaxRowNumber` 設為 `1` 或 `2` 時，如果翻譯字幕字元總數超過顯示範圍，內容會被截斷。例如，如果每列字元數上限為 10，且 `MaxRowNumber` 為 `2`，則第 20 個字元之後的內容會被截斷。<br><br><br>* > 如果未傳入 `DisplayPreset`，此參數為必填。如果傳入 `DisplayPreset`，此參數不生效。<br> |
|Hidden |Boolean |否 |`false` |是否隱藏翻譯字幕。預設值： `false`。有效值：<br><br><br>* `true`：隱藏翻譯字幕。<br><br>* `false`：顯示翻譯字幕。 |
|Font |String |是 |`inter` |翻譯字幕字型。<br><br><br>* 當 `SIConfig` 下的 `Enable` 值設為 `true` 且使用 AI 配音模式時，呼叫 [GetSubtitleTranscodePresetConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSubtitleTranscodePresetConfig)，並使用 `Font` 取得目前帳號可用的字型清單，然後傳入 `Key` 值。<br><br>* 當 `SIConfig` 下的 `Enable` 值設為 `false` 且使用僅字幕模式時，有效值取決於翻譯字幕語言 (`Language`)。<br><br>   * 如果翻譯字幕語言為 `zh`，支援下列字型：<br><br>      * `siyuanheiti`：Source Han Sans。<br><br>      * `songtixi`：Songti Light。<br><br>      * `songticu`：Songti Bold。<br><br>      * `heitifan`：Heiti Traditional。<br><br>      * `kaiti`：Kaiti。<br><br>   * 如果翻譯字幕語言為 `en`，支援下列字型：<br><br>      * `inter`：Inter。<br><br>      * `roboto`：Roboto。<br><br>      * `opposans`：OPPOSans。<br><br>      * `siyuansongti`：Source Han Serif。<br><br>      * `montserrat`：Montserrat。<br><br>   * 如果翻譯字幕語言為 `ko` 或 `ja`，支援 `notosans` (Noto Sans)。 |
|FontSize |Integer |否 |`18` |翻譯字幕字型大小，單位為 px。<br><br>> **说明**<br><br><br>> 如果未傳入 `DisplayPreset`，此參數為必填。如果傳入 `DisplayPreset`，此參數不生效。<br> |
|FontColor |String |是 |`0xFF0000@0.5` |翻譯字幕字型顏色。您可以透過下列任一方式指定顏色：<br><br><br>* 以 `0x` 或 `#` 開頭，後接十六進位 RGB 色彩值，並使用 `@` 附加不透明度。不透明度支援十六進位值，例如 `0x80`，以及十進位值，例如 `0.5`。例如，若要指定紅色 (`FF0000`) 且不透明度為 50%，請傳入 `0xFF0000@0x80`、 `0xFF0000@0.5`、 `#FF0000@0x80` 或 `#FF0000@0.5`。<br><br>* 使用 FFmpeg 色彩關鍵字，並使用 `@` 附加不透明度。不透明度支援十進位值，例如 `0.5`。例如，若要指定 `0xF0F8FF` 且不透明度為 50%，請傳入 `AliceBlue@0.5`。<br><br><br>> **说明**<br><br><br><br>* > 如需色彩定義和更多色彩關鍵字，請參閱 [FFmpeg 色彩語法](https://ffmpeg.org/ffmpeg-utils.html#color-syntax)。<br><br><br>* > 不透明度值越大，表示透明度越低。<br><br><br>* > 當不透明度指定為十進位時，有效範圍為 `[0,1]`，最多支援兩位小數。<br> |
|Border |[Border](https://docs.byteplus.com/en/docs/24/107349#border) 物件 |否 |`-` |翻譯字幕的字型陰影。 |
|Box |[Box](https://docs.byteplus.com/en/docs/24/107349#box) 物件 |否 |`-` |翻譯字幕的字型背景。 |

### Callback

|參數 |資料類型 |必填 |範例值 |說明 |
|---|---|---|---|---|
|Url |String |是 |`https://xxx` |用於接收回呼訊息的 URL。URL 必須以 `http://` 或 `https://` 開頭，可公開存取，且包含 1\-100 個字元。如需 AI 配音回呼訊息的詳細資訊，請參閱 [AI 配音](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-callback-description?lang=en#ai-dubbing)。 |

### Box

|參數 |資料類型 |必填 |範例值 |說明 |
|---|---|---|---|---|
|W |Float |是 |`2` |寬度，單位為 px。建議範圍： `[1,10]`。 |
|Color |String |是 |`0xFF0000@0.5` |顏色。您可以透過下列任一方式指定顏色：<br><br><br>* 以 `0x` 或 `#` 開頭，後接十六進位 RGB 色彩值，並使用 `@` 附加不透明度。不透明度支援十六進位值，例如 `0x80`，以及十進位值，例如 `0.5`。例如，若要指定紅色 (`FF0000`) 且不透明度為 50%，請傳入 `0xFF0000@0x80`、 `0xFF0000@0.5`、 `#FF0000@0x80` 或 `#FF0000@0.5`。<br><br>* 使用 FFmpeg 色彩關鍵字，並使用 `@` 附加不透明度。不透明度支援十進位值，例如 `0.5`。例如，若要指定 `0xF0F8FF` 且不透明度為 50%，請傳入 `AliceBlue@0.5`。<br><br><br>> **说明**<br><br><br><br>* > 如需色彩定義和更多色彩關鍵字，請參閱 [FFmpeg 色彩語法](https://ffmpeg.org/ffmpeg-utils.html#color-syntax)。<br><br><br>* > 不透明度值越大，表示透明度越低。<br><br><br>* > 當不透明度指定為十進位時，有效範圍為 `[0,1]`，最多支援兩位小數。<br> |

### Border

|參數 |資料類型 |必填 |範例值 |說明 |
|---|---|---|---|---|
|Width |Float |是 |`2` |寬度，單位為 px。建議範圍： `[1,10]`。 |
|Color |String |是 |`0xFF0000@0.5` |顏色。您可以透過下列任一方式指定顏色：<br><br><br>* 以 `0x` 或 `#` 開頭，後接十六進位 RGB 色彩值，並使用 `@` 附加不透明度。不透明度支援十六進位值，例如 `0x80`，以及十進位值，例如 `0.5`。例如，若要指定紅色 (`FF0000`) 且不透明度為 50%，請傳入 `0xFF0000@0x80`、 `0xFF0000@0.5`、 `#FF0000@0x80` 或 `#FF0000@0.5`。<br><br>* 使用 FFmpeg 色彩關鍵字，並使用 `@` 附加不透明度。不透明度支援十進位值，例如 `0.5`。例如，若要指定 `0xF0F8FF` 且不透明度為 50%，請傳入 `AliceBlue@0.5`。<br><br><br>> **说明**<br><br><br><br>* > 如需色彩定義和更多色彩關鍵字，請參閱 [FFmpeg 色彩語法](https://ffmpeg.org/ffmpeg-utils.html#color-syntax)。<br><br><br>* > 不透明度值越大，表示透明度越低。<br><br><br>* > 當不透明度指定為十進位時，有效範圍為 `[0,1]`，最多支援兩位小數。<br> |

## 回應參數

此 API 只會在回應中傳回[通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

## 範例

### 範例請求

**原文 (ASR) 字幕（整句顯示）**

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

**原文 (ASR) 字幕（直播顯示）**

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

**字幕翻譯**

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

**配音音訊 + 翻譯字幕**

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

**配音音訊 + 唇形同步 + 翻譯字幕**

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

### 範例回應

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

## 錯誤碼

以下是與目前操作相關的錯誤碼。如需其他錯誤碼，請參閱 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。

|狀態碼 |錯誤碼 |錯誤訊息 |說明 |
|---|---|---|---|
|200 |CommonErr |\- |未分類錯誤。建議重試。如果仍傳回此錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |\- |輸入參數無效或不符合要求。請參閱[請求參數](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createsubtitletranscodepreset-2023#request-parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |Request parameter error, please check input data |參數驗證失敗。請檢查資料類型是否正確。 |
|403 |RequestForbidden |\- |請求遭拒，因為目前帳號下沒有請求的資源（資源包括網域名稱空間、網域名稱、應用程式名稱、配置和憑證）。 |
|403 |RequestForbidden.AccountIDNotAllow |this AccountID does not have permission to access the corresponding resource, please check the request parameters |請求遭拒，因為目前帳號下沒有請求的資源（資源包括網域名稱空間、網域名稱、應用程式名稱、配置和憑證）。 |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |影片直播服務尚未啟用或帳號欠費，導致帳單不可用。請檢查服務啟用狀態和帳號欠費狀態。 |
|404 |ResourceNotFound |\- |找不到資源（包括網域名稱空間、網域名稱、應用程式名稱、配置和憑證）。建議重試。如果仍傳回此錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |an internal error occurred, please contact the administrator. |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.Preset |an internal error related to preset occurred, please contact the administrator. |發生與預設配置相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |內部服務逾時。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
