---
title: "CreateSpeechTask"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/CreateSpeechTask-zh-TW"
---

呼叫 `CreateSpeechTask` API 以建立 AI Dubbing 任務。任務建立後，當您在 `StartTime` 到 `EndTime` 的轉推時間期間開始推送串流時，任務會自動拉取直播串流進行 AI Dubbing 處理，並將處理後的直播串流推送至指定的推流位址。例如，您可以使用 OBS 開始直播，透過 AI Dubbing 任務處理直播串流，然後在 TikTok 上串流處理後的內容。如需詳細資訊，請參閱 [AI Dubbing](https://docs.byteplus.com/en/docs/byteplus-media-live/ai-liveinterpret-simultaneous-audio-and-video-interpretation)。

## 使用情境

根據您的情境選取適合的功能。

|情境 |建議功能 |參數配置 |描述 |
|---|---|---|---|
|為直播串流提供基本字幕，協助觀眾在靜音或嘈雜環境中觀看。 |原始 (ASR) 字幕 |* 整句顯示：字幕逐句顯示。將 `Pipe` 設為 `mix`（僅字幕），且僅設定 `Original`（來源字幕），不設定 `Translation`（翻譯字幕）。<br><br>* 直播顯示：字幕不等待句子結束，逐字元或逐字顯示。將 `Pipe` 設為 `realtime`（即時口譯模式），且僅設定 `Original`（來源字幕），不設定 `Translation`（翻譯字幕）。 |使用語音辨識在影片上疊加來源字幕。<br><br>> **说明**<br><br><br>> 目前，直播顯示僅支援中文和英文字幕。整句顯示支援更多語言。<br> |
|啟用跨語言文字溝通，觸及全球受眾。 |字幕翻譯 |將 `Pipe` 設為 `mix`（僅字幕）或 `realtime`（即時口譯模式），並同時設定 `Original`（來源字幕）和 `Translation`（翻譯字幕）。 |使用語音辨識在影片上疊加翻譯字幕，同時保留原聲。 |
|提供類似觀看配音電影的配音式翻譯體驗。 |配音音訊 |將 `Pipe` 設為 `realtime`（即時口譯模式）且將 `VoiceShow` 設為 `true`，或將 `Pipe` 設為 `si`（AI Dubbing 模式），並設定 `Original`（來源字幕）和 `Translation`（翻譯字幕）的 `Language` 欄位。 |提供配音音訊並取代原聲。在即時口譯模式中，您可以選擇將配音音訊疊加到原聲上，或直接取代原聲。 |
|提供沉浸式真人口譯體驗，以提升專業度。 |配音音訊 + 唇形同步 |將 `Pipe` 設為 `si`（AI Dubbing 模式），將 `LipSync` 設為 `true`，並設定 `Original`（來源字幕）和 `Translation`（翻譯字幕）的 `Language` 欄位。 |在配音音訊的基礎上，AI 技術會將講者的唇部動作與配音音訊同步，創造高度逼真的效果。 |

## 要求

* **速率限制**：每個帳號每秒 10 個請求。

* **計費**：僅收取 AI Dubbing 費用。AI Dubbing 依任務的**實際串流推送時長**計費。如需詳細資訊，請參閱 [AI Dubbing 計費](https://docs.byteplus.com/en/docs/byteplus-media-live/ai_dubbing)。

* **並行限制**：每個帳號最多可同時執行 2 個任務。若要同時執行更多任務，請[提交工單](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)聯絡技術支援。

* **先決條件**

   * 確保推流和拉流的網域名稱已新增至同一個網域名稱空間下。如需詳細資訊，請參閱 [CreateDomain](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-dj3h3u96xn)。

      > **注意**

      > 只有在您使用 MediaLive 推流和拉流位址時，才需要此先決條件。

   * 準備 **Pull Stream URL** 和 **Push Stream URL**。

      * **Pull Stream URL**：取得用於拉取原始直播串流的有效拉流位址。支援 RTMP 和 FLV 格式。

         如果您使用 MediaLive 拉流位址作為 **Pull Stream URL**，請使用相同的 `AppName` 和 `StreamName`，並使用 [GeneratePushURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generatepushurl-2023) 和 [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) 產生一組位址。此組位址包含作為 **Pull Stream URL** 使用的拉流位址，以及用於推送原始直播串流的推流位址。

      * **Push Stream URL**：用於推送處理後的直播串流。支援 RTMP 格式。

         * 如果您使用 MediaLive 推流位址作為 **Push Stream URL**，請使用相同的 `AppName` 和 `StreamName`，並使用 [GeneratePushURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generatepushurl-2023) 和 [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) 產生一組位址。此組位址包含作為 **Push Stream URL** 使用的推流位址，以及用於拉取處理後直播串流的拉流位址。

         * 如果您使用其他雲端供應商或 TikTok 等直播平台的推流位址作為 **Push Stream URL**，請參閱對應平台的官方文件，或聯絡平台客服以取得有效的推流位址。

   > **说明**

   > 用於推送原始直播串流的推流位址，以及用於拉取處理後直播串流的拉流位址，不受特定通訊協定限制。請根據您的實際需求選擇通訊協定。

## HTTP 請求

* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=CreateSpeechTask&Version=2023\-01\-01

## 請求參數

### 通用參數

所有 API 除了 API 特定參數外，還必須搭配[通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)呼叫。

### Query

|參數 |資料類型 |必填 |範例值 |描述 |
|---|---|---|---|---|
|Action |String |是 |`CreateSpeechTask` |API 操作。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |

### Body 參數

|參數 |資料類型 |必填 |範例值 |描述 |
|---|---|---|---|---|
|Name |String |是 |`TaskA` |任務名稱。名稱在所有執行中的任務之間必須唯一。名稱長度必須為 1 到 20 個字元，且可包含數字 (0\-9)、大寫字母 (A\-Z)、小寫字母 (a\-z)、中文字元、底線 (_) 和連字號 (\-)。 |
|Rule |[Rule](https://docs.byteplus.com/en/docs/24/118403#rule) 的物件 |是 |`-` |任務規則。 |

### Rule

|參數 |資料類型 |必填 |範例值 |描述 |
|---|---|---|---|---|
|Pipe |String |是 |`si` |任務類型。有效值：<br><br><br>* `si`：AI Dubbing 模式。字幕、配音音訊和影片完全同步。支援唇形同步。此模式適用於會議直播和其他需要高度同步與沉浸感的情境。此模式會引入一些延遲。<br><br>* `mix`：僅字幕，包含整句顯示的原始 (ASR) 字幕。<br><br>* `realtime`：即時口譯模式，包含直播顯示的原始 (ASR) 字幕。此模式延遲低，但影片可能無法與字幕或配音音訊同步。此模式適用於體育直播等對延遲敏感的情境。<br><br><br>> **说明**<br><br><br>> 當此參數設為 `si` 時，預設啟用配音音訊且無法停用。<br> |
|Delay |Integer |否 |`20` |播放延遲，單位為秒，用於留出足夠時間進行配音音訊和字幕翻譯。有效範圍：`[0,60]`。建議值會依任務類型 (`Pipe`) 和功能而異：<br><br><br>* `si`：<br><br>   * 啟用唇形同步、配音音訊和字幕：`20`。<br><br>   * 啟用配音音訊和字幕：`12`。<br><br>* `mix`：<br><br>   * 整句顯示的原始 (ASR) 字幕：`15`。<br><br>   * 字幕翻譯：`8`。<br><br>* `realtime`：`2` 或 `3`。<br><br><br>如需詳細功能設定，請參閱[使用情境](https://docs.byteplus.com/en/docs/byteplus-media-live/CreateSpeechTask?lang=en#usage-scenario)。<br><br>> **说明**<br><br><br>> 如果字幕早於原聲或影片出現，請降低播放延遲，使字幕與原聲或影片對齊；反之亦然。<br> |
|Source |[Source](https://docs.byteplus.com/en/docs/24/118403#source) 的物件 |是 |`-` |來源串流設定。 |
|StartTime |String |否 |`2025-11-17T11:30:06+08:00` |任務開始時間。時間採用 RFC3339 格式，使用 UTC+8，且精確到秒。如果未傳入此參數，任務會立即開始。 |
|EndTime |String |否 |`2025-11-17T12:11:06+08:00` |任務結束時間。結束時間必須晚於 `StartTime`，且 `StartTime` 與 `EndTime` 之間的時間跨度不得超過 7 天。時間採用 RFC3339 格式，使用 UTC+8，且精確到秒。如果未傳入此參數，任務會在開始時間後 7 天結束。<br><br>> **说明**<br><br><br>> 當任務結束、來源串流中斷連線或拉流失敗時，轉推會自動停止。<br> |
|Output |[Output](https://docs.byteplus.com/en/docs/24/118403#output) 的物件 |是 |`-` |推流設定。 |
|SI |[SI](https://docs.byteplus.com/en/docs/24/118403#si) 的物件 |否 |`-` |AI Dubbing 模式設定。<br><br>> **说明**<br><br><br>> 此參數僅在 `Pipe` 設為 `si` 時生效。<br> |
|RealTime |[RealTime](https://docs.byteplus.com/en/docs/24/118403#realtime) 的物件 |否 |`-` |即時口譯模式設定。<br><br>> **说明**<br><br><br>> 此參數僅在 `Pipe` 設為 `realtime` 時生效。<br> |
|Extra |[Extra](https://docs.byteplus.com/en/docs/24/118403#extra) 的物件 |否 |`-` |額外設定。<br><br>> **说明**<br><br><br>> 建議僅在啟用配音音訊時傳入此參數。如需配音音訊設定的詳細資訊，請參閱[使用情境](https://docs.byteplus.com/en/docs/byteplus-media-live/CreateSpeechTask?lang=en#usage-scenario)。<br> |
|Subtitle |[Subtitle](https://docs.byteplus.com/en/docs/24/118403#subtitle) 的物件 |否 |`-` |字幕設定。 |

### Source

|參數 |資料類型 |必填 |範例值 |描述 |
|---|---|---|---|---|
|Url |String |是 |`https://xxx/live/xxx.flv` |**Pull Stream URL**。支援 RTMP 和 FLV 格式。任務會從此 URL 拉取原始直播串流並處理串流。<br><br>> **说明**<br><br><br>> URL 不能直接包含多位元組字元，例如中文字元。如需使用此類字元，請對其進行 URL 編碼。<br> |

### Output

|參數 |資料類型 |必填 |範例值 |描述 |
|---|---|---|---|---|
|Url |String 陣列 |是 |`["rtmp://push.example.com/live/test01","rtmp://push.example.com/live/test02"]` |**Push Stream URL**。支援 RTMP 格式。任務會將處理後的直播串流推送至此 URL。<br><br>您最多可以傳入 8 個推流 URL。<br><br>> **说明**<br><br><br><br>* > URL 不能直接包含多位元組字元，例如中文字元。如需使用此類字元，請對其進行 URL 編碼。<br><br><br>* > 若要在 TikTok 或其他第三方平台播放處理後的直播串流，請確保您使用第三方平台的推流 URL。如需取得推流 URL 的資訊，請參閱第三方平台的官方文件，或聯絡平台客服。<br> |
|Callback |[Callback](https://docs.byteplus.com/en/docs/24/118403#callback) 的物件 |否 |`-` |回呼設定。 |
|Sei |String 陣列 |否 |`["subtitle"]` |若要將字幕寫入直播串流中的 SEI 訊息，請將此參數設為 `["subtitle"]`。<br><br>> **说明**<br><br><br><br>* > 此參數僅在 `Pipe` 設為 `si` 或 `mix` 時生效。<br><br><br>* > MediaLive 將字幕寫入 SEI 訊息時，會使用 `100` 作為 SEI `type` 值。如果您的推流工具或應用程式也會將自訂 SEI 訊息寫入串流，請避免使用相同的 SEI `type` 值。否則，播放器可能會將自訂資料識別為字幕。<br> |

### SI

|參數 |資料類型 |必填 |範例值 |描述 |
|---|---|---|---|---|
|LipSync |Boolean |否 |`true` |是否啟用唇形同步。預設值：`false`。有效值：<br><br><br>* `true`：啟用唇形同步。啟用此功能後，講者的唇部動作會與配音音訊同步，使直播串流更具沉浸感。<br><br>* `false`：停用唇形同步。 |

### RealTime

|參數 |資料類型 |必填 |範例值 |描述 |
|---|---|---|---|---|
|VoiceShow |Boolean |否 |`true` |是否啟用配音音訊。預設值：`false`。有效值：<br><br><br>* `true`：啟用配音音訊。啟用此功能後，會提供具有聲音複製效果的翻譯語音。<br><br>* `false`：停用配音音訊。 |

### Extra

|參數 |資料類型 |必填 |範例值 |描述 |
|---|---|---|---|---|
|AMix |[AMix](https://docs.byteplus.com/en/docs/24/118403#amix) 的物件 |否 |`-` |混音設定。 |
|Separator |[Separator](https://docs.byteplus.com/en/docs/24/118403#separator) 的物件 |否 |`-` |人聲與背景音分離設定。 |

### Subtitle

|參數 |資料類型 |必填 |範例值 |描述 |
|---|---|---|---|---|
|Position |[Position](https://docs.byteplus.com/en/docs/24/118403#position) 的物件 |否 |`-` |字幕位置。 |
|Original |[Original](https://docs.byteplus.com/en/docs/24/118403#original) 的物件 |是 |`-` |來源字幕設定。<br><br>> **说明**<br><br><br>> 來源語言和目標語言必須不同。<br> |
|Translation |[Translation](https://docs.byteplus.com/en/docs/24/118403#translation) 的陣列 |否 |`-` |翻譯字幕設定。<br><br>> **说明**<br><br><br><br>* > 來源語言和目標語言必須不同。<br><br><br>* > 目前，每個請求只能傳入一種翻譯字幕語言。<br> |
|GlossaryMap |JSON Map |否 |`{"赛事直播":"sports live streaming","实时字幕":"real-time subtitles"}` |術語表。此參數預設為空。<br><br>使用格式 `"original text":"translation"`，並以英文逗號 (,) 分隔多個項目。範例：`{"赛事直播":"sports live streaming","实时字幕":"real-time subtitles"}`。總字元數不得超過 30,000。<br><br>傳入專有詞彙和預期翻譯，例如品牌名稱、人名、產品名稱或功能名稱，作為翻譯模型的參考。這有助於提升專有詞彙的翻譯準確性，**但預期翻譯不一定每次都會使用**。如果使用術語表後仍持續出現誤譯，您可以使用 `ReplaceMap` 逐一設定可能的誤譯及其正確翻譯，以強制修正翻譯字幕。<br><br>> **警告**<br><br><br><br>* > 原文或翻譯值不能包含英文逗號 (,)。<br><br><br>* > 此參數僅在已設定 `Translation` 時生效，且**僅套用於翻譯字幕**。<br> |
|ReplaceMap |JSON Map |否 |`{"live core":"LiveCore","media life":"MediaLive"}` |修正清單。此參數預設為空。<br><br>設定需要強制修正的字幕文字。逐一新增可能的誤譯或辨識錯誤及其正確文字。<br><br>格式為 `"incorrect text":"correct text"`。以英文逗號 (,) 分隔多個修正項目。每個錯誤文字或正確文字值的長度必須為 1 到 50 個字元。您最多可以傳入 60 個修正項目。<br><br>當系統比對到錯誤文字時，會強制將錯誤文字取代為正確文字。<br><br><br>* **原始 (ASR) 字幕**：修正辨識錯誤。例如，如果 **MediaLive** 被錯誤辨識為 **media life**，您可以傳入 `{"media life":"MediaLive"}`。<br><br>* **翻譯字幕**：修正誤譯。**修正僅修改翻譯字幕，不會修改來源字幕或配音音訊**。例如，如果 **LiveCore** 被誤譯為 **live core**，您可以傳入 `{"live core":"LiveCore"}`。<br><br><br>> **警告**<br><br><br><br>* > 錯誤文字和正確文字值不能包含英文逗號 (,)。<br><br><br>* > `ReplaceMap` 僅比對文字，不會判斷上下文。僅在可明確識別錯誤文字為錯誤時使用此參數。請勿將錯誤文字取代為包含該錯誤文字的文字。例如，如果您傳入 `{"stream":"live stream"}`，而字幕已正確顯示 **live stream**，系統仍會將 **stream** 取代為 **live stream**，導致 **live live stream**。<br> |
|HotWords |String 陣列 |否 |`["MediaLive","LiveCore"]` |熱詞清單。此參數預設為空。<br><br>熱詞必須符合來源語言，且總字元數不得超過 30,000。<br><br>傳入熱詞，例如產品名稱和熱門短語，作為語音辨識模型的參考。這有助於提升辨識準確性，**但熱詞不一定每次都能準確辨識**。如果使用熱詞後仍持續出現辨識錯誤，您可以使用 `ReplaceMap` 逐一設定可能的辨識錯誤及其正確文字，以強制修正原始 (ASR) 字幕。<br><br>> **警告**<br><br><br>> 此參數僅對**原始 (ASR) 字幕**生效。如需詳細資訊，請參閱[使用情境](https://docs.byteplus.com/en/docs/byteplus-media-live/CreateSpeechTask?lang=en#usage-scenario)。<br> |

### Callback

|參數 |資料類型 |必填 |範例值 |描述 |
|---|---|---|---|---|
|Url |String |是 |`https://xxx` |用於接收回呼訊息的 URL。URL 必須以 `http://` 或 `https://` 開頭，可公開存取，且包含 1–100 個字元。如需 AI Dubbing 回呼訊息的詳細資訊，請參閱 [AI Dubbing](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-callback-description?lang=en#ai-dubbing)。 |

### AMix

|參數 |資料類型 |必填 |範例值 |描述 |
|---|---|---|---|---|
|BGVolume |Float |否 |`1.0` |原聲或排除人聲後的背景音音量。預設值：`0.2`。有效範圍：`[0, 1.0]`。<br><br><br>* 當 `Separator` 設為 `true` 時，此參數會調整背景音音量。<br><br>* 當 `Separator` 設為 `false` 時，此參數會調整原聲音量。如果此參數設為 `0`，僅保留配音音訊中的人聲。<br><br><br>> **说明**<br><br><br>> 此參數僅在 `Pipe` 設為 `realtime` 時生效。<br> |
|AudioEnhance |Boolean |否 |`true` |是否啟用音量平衡。預設值：`true`。有效值：<br><br><br>* `true`：啟用音量平衡。系統會自動調整輸出音訊音量，使音量保持穩定且舒適，協助避免突然的音量變化或刺耳爆音，並改善聆聽體驗。<br><br>* `false`：停用音量平衡。 |

### Separator

|參數 |資料類型 |必填 |範例值 |描述 |
|---|---|---|---|---|
|HandleType |Integer |否 |`0` |是否啟用降噪。預設值：`0`。有效值：<br><br><br>* `0`：停用降噪。<br><br>* `1`：啟用降噪。這可以降低配音音訊中的電流聲和環境噪音等背景噪音，並提升最終音訊清晰度。<br><br><br>> **警告**<br><br><br><br>* > 啟用降噪可能會導致背景音消失。<br><br><br>* > 當 `Pipe` 設為 `realtime` 時，此參數僅在 `Separator` 設為 `true` 時生效。<br> |
|Separator |Boolean |否 |`false` |是否以配音音訊取代原聲。預設值：`false`。有效值：<br><br><br>* `true`：完全移除原聲，僅輸出翻譯語音。這適用於不需要原聲的情境。<br><br>* `false`：將配音音訊疊加到原聲上。這常用於體育直播和其他必須保留現場氛圍的情境。<br><br><br>> **说明**<br><br><br>> 此參數僅在 `Pipe` 設為 `realtime` 時生效。<br> |

### Position

|參數 |資料類型 |必填 |範例值 |描述 |
|---|---|---|---|---|
|Relative |String |否 |`bottom` |影片中的字幕位置。預設值：`bottom`。有效值：<br><br><br>* `top`：在影片頂部顯示字幕。<br><br>* `bottom`：在影片底部顯示字幕。 |
|MarginTb |Float |否 |`0.05` |字幕的上邊距或下邊距，也就是字幕到影片頂部或底部邊緣的距離。值為影片高度的百分比。有效範圍：`(0, 0.5]`。<br><br><br>* 當 `Relative` 設為 `top` 時，此參數指定上邊距。<br><br>* 當 `Relative` 設為 `bottom` 時，此參數指定下邊距。 |
|MarginLr |Float |否 |`0.2` |字幕的左右邊距，也就是字幕到影片左右邊緣的距離。值為影片寬度的百分比。有效範圍：`(0, 0.3]`。 |

### Original

|參數 |資料類型 |必填 |範例值 |描述 |
|---|---|---|---|---|
|Language |String |是 |`zh` |來源字幕語言。您可以呼叫 [GetSpeechConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSpeechConfig)，並使用 `OriginalLang` 取得目前帳號可用於字幕翻譯和配音音訊的來源語言，或使用 `AsrLang` 取得目前帳號可用的原始 (ASR) 字幕語言。傳入 `Key` 值。 |
|Font |String |否 |`arial` |來源字幕字型。預設值：`arial`。您可以呼叫 [GetSpeechConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSpeechConfig)，並使用 `Font` 取得目前帳號可用的字型清單。傳入 `Key` 值。 |
|FontSize |Integer |否 |`32` |來源字幕字型大小。預設值：`40`。有效範圍：`[1,100]`。 |
|FontColor |String |否 |`0xFF0000@0.5` |來源字幕字型顏色。您可以使用下列其中一種方式指定顏色：<br><br><br>* 以 `0x` 或 `#` 開頭，後接十六進位 RGB 色值，並使用 `@` 附加不透明度。不透明度支援 `0x80` 等十六進位值，以及 `0.5` 等十進位值。例如，若要指定 50% 不透明度的紅色 (`FF0000`)，請傳入 `0xFF0000@0x80`、`0xFF0000@0.5`、`#FF0000@0x80` 或 `#FF0000@0.5`。<br><br>* 使用 FFmpeg 顏色關鍵字，並使用 `@` 附加不透明度。不透明度支援 `0.5` 等十進位值。例如，若要指定 50% 不透明度的 `0xF0F8FF`，請傳入 `AliceBlue@0.5`。<br><br><br>> **说明**<br><br><br><br>* > 如需顏色定義和更多顏色關鍵字，請參閱 [FFmpeg color syntax](https://ffmpeg.org/ffmpeg-utils.html#color-syntax)。<br><br><br>* > 不透明度值越大，透明度越低。<br><br><br>* > 當不透明度指定為十進位時，有效範圍為 `[0,1]`，最多支援兩位小數。<br> |
|Alignment |Integer |否 |`0` |來源字幕對齊方式。預設值：`0`。有效值：<br><br><br>* `0`：置中對齊。<br><br>* `1`：靠左對齊。<br><br>* `2`：靠右對齊。 |
|MaxRowNumber |Integer |否 |`2` |來源字幕的最大行數。預設值：`0`。有效值：<br><br><br>* `0`：根據字幕字元總數和每行最大字元數自動換行，以確保完整顯示。<br><br>* `1`：每種語言最多顯示一行。內容可能會被截斷。<br><br>* `2`：每種語言最多顯示兩行。內容可能會被截斷。<br><br><br>> **说明**<br><br><br>> 來源字幕和翻譯字幕的行數限制會分別計算。<br> |
|MaxCharNumber |Integer |否 |`60` |來源字幕每行的最大字元數。預設值：`60`。建議值：`60`。<br><br>> **说明**<br><br><br><br>* > 系統會根據此參數、`MarginLr`、`Font`、`FontSize`、螢幕解析度和其他因素，計算最終每行可顯示的最大字元數。<br><br><br>* > 每個中文字元、字母、符號或數字均計為一個字元。<br><br><br>* > 當 `MaxRowNumber` 設為 `1` 或 `2` 時，如果來源字幕字元總數超過顯示範圍，內容會被截斷。例如，如果每行最大字元數為 10，且 `MaxRowNumber` 為 `2`，則第 20 個字元之後的內容會被截斷。<br> |
|Hidden |Boolean |否 |`false` |是否隱藏來源字幕。預設值：`false`。有效值：<br><br><br>* `true`：隱藏來源字幕。<br><br>* `false`：顯示來源字幕。 |
|ShowPriority |Integer |否 |`100` |來源字幕的顯示優先順序。預設情況下，來源字幕顯示在翻譯字幕上方。值越大表示優先順序越高。例如，如果來源字幕的 `ShowPriority` 為 `1`，而翻譯字幕的 `ShowPriority` 為 `2`，則翻譯字幕會顯示在來源字幕上方。 |
|Box |[Box](https://docs.byteplus.com/en/docs/24/118403#box) 的物件 |否 |`-` |來源字幕的字型背景。 |
|Border |[Border](https://docs.byteplus.com/en/docs/24/118403#border) 的物件 |否 |`-` |來源字幕的字型陰影。 |

### Translation

|參數 |資料類型 |必填 |範例值 |描述 |
|---|---|---|---|---|
|Language |String |是 |`en` |翻譯字幕語言。您可以呼叫 [GetSpeechConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSpeechConfig)，並使用 `Lang` 取得目前帳號可用的翻譯字幕語言。傳入 `Key` 值。 |
|Font |String |否 |`arial` |翻譯字幕字型。預設值：`arial`。您可以呼叫 [GetSpeechConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSpeechConfig)，並使用 `Font` 取得目前帳號可用的字型清單。傳入 `Key` 值。 |
|FontSize |Integer |否 |`32` |翻譯字幕字型大小。預設值：`40`。有效範圍：`[1,100]`。 |
|FontColor |String |否 |`0xFF0000@0.5` |翻譯字幕字型顏色。您可以使用下列其中一種方式指定顏色：<br><br><br>* 以 `0x` 或 `#` 開頭，後接十六進位 RGB 色值，並使用 `@` 附加不透明度。不透明度支援 `0x80` 等十六進位值，以及 `0.5` 等十進位值。例如，若要指定 50% 不透明度的紅色 (`FF0000`)，請傳入 `0xFF0000@0x80`、`0xFF0000@0.5`、`#FF0000@0x80` 或 `#FF0000@0.5`。<br><br>* 使用 FFmpeg 顏色關鍵字，並使用 `@` 附加不透明度。不透明度支援 `0.5` 等十進位值。例如，若要指定 50% 不透明度的 `0xF0F8FF`，請傳入 `AliceBlue@0.5`。<br><br><br>> **说明**<br><br><br><br>* > 如需顏色定義和更多顏色關鍵字，請參閱 [FFmpeg color syntax](https://ffmpeg.org/ffmpeg-utils.html#color-syntax)。<br><br><br>* > 不透明度值越大，透明度越低。<br><br><br>* > 當不透明度指定為十進位時，有效範圍為 `[0,1]`，最多支援兩位小數。<br> |
|Alignment |Integer |否 |`0` |翻譯字幕對齊方式。預設值：`0`。有效值：<br><br><br>* `0`：置中對齊。<br><br>* `1`：靠左對齊。<br><br>* `2`：靠右對齊。 |
|MaxRowNumber |Integer |否 |`2` |翻譯字幕的最大行數。預設值：`0`。有效值：<br><br><br>* `0`：根據字幕字元總數和每行最大字元數自動換行，以確保完整顯示。<br><br>* `1`：每種語言最多顯示一行。內容可能會被截斷。<br><br>* `2`：每種語言最多顯示兩行。內容可能會被截斷。<br><br><br>> **说明**<br><br><br>> 來源字幕和翻譯字幕的行數限制會分別計算。<br> |
|MaxCharNumber |Integer |否 |`60` |翻譯字幕每行的最大字元數。預設值：`60`。建議值：`60`。<br><br>> **说明**<br><br><br><br>* > 系統會根據此參數、`MarginLr`、`Font`、`FontSize`、螢幕解析度和其他因素，計算最終每行可顯示的最大字元數。<br><br><br>* > 每個中文字元、字母、符號或數字均計為一個字元。<br><br><br>* > 當 `MaxRowNumber` 設為 `1` 或 `2` 時，如果翻譯字幕字元總數超過顯示範圍，內容會被截斷。例如，如果每行最大字元數為 10，且 `MaxRowNumber` 為 `2`，則第 20 個字元之後的內容會被截斷<br> |
|Hidden |Boolean |否 |`false` |是否隱藏翻譯字幕。預設值：`false`。有效值：<br><br><br>* `true`：隱藏翻譯字幕。<br><br>* `false`：顯示翻譯字幕。 |
|ShowPriority |Integer |否 |`100` |翻譯字幕的顯示優先順序。預設情況下，來源字幕顯示在翻譯字幕上方。值越大表示優先順序越高。例如，如果來源字幕的 `ShowPriority` 為 `1`，而翻譯字幕的 `ShowPriority` 為 `2`，則翻譯字幕會顯示在來源字幕上方。 |
|Box |[Box](https://docs.byteplus.com/en/docs/24/118403#box) 的物件 |否 |`-` |翻譯字幕的字型背景。 |
|Border |[Border](https://docs.byteplus.com/en/docs/24/118403#border) 的物件 |否 |`-` |翻譯字幕的字型陰影。 |

### Box

|參數 |資料類型 |必填 |範例值 |描述 |
|---|---|---|---|---|
|W |Float |是 |`1.0` |寬度，單位為 px。建議範圍：`[1,10]`。 |
|Color |String |是 |`0xFF0000@0.5` |顏色。您可以使用下列其中一種方式指定顏色：<br><br><br>* 以 `0x` 或 `#` 開頭，後接十六進位 RGB 色值，並使用 `@` 附加不透明度。不透明度支援 `0x80` 等十六進位值，以及 `0.5` 等十進位值。例如，若要指定 50% 不透明度的紅色 (`FF0000`)，請傳入 `0xFF0000@0x80`、`0xFF0000@0.5`、`#FF0000@0x80` 或 `#FF0000@0.5`。<br><br>* 使用 FFmpeg 顏色關鍵字，並使用 `@` 附加不透明度。不透明度支援 `0.5` 等十進位值。例如，若要指定 50% 不透明度的 `0xF0F8FF`，請傳入 `AliceBlue@0.5`。<br><br><br>> **说明**<br><br><br><br>* > 如需顏色定義和更多顏色關鍵字，請參閱 [FFmpeg color syntax](https://ffmpeg.org/ffmpeg-utils.html#color-syntax)。<br><br><br>* > 不透明度值越大，透明度越低。<br><br><br>* > 當不透明度指定為十進位時，有效範圍為 `[0,1]`，最多支援兩位小數。<br> |

### Border

|參數 |資料類型 |必填 |範例值 |描述 |
|---|---|---|---|---|
|W |Float |是 |`1.0` |寬度，單位為 px。建議範圍：`[1,10]`。 |
|Color |String |是 |`0xFF0000@0.5` |顏色。您可以使用下列其中一種方式指定顏色：<br><br><br>* 以 `0x` 或 `#` 開頭，後接十六進位 RGB 色值，並使用 `@` 附加不透明度。不透明度支援 `0x80` 等十六進位值，以及 `0.5` 等十進位值。例如，若要指定 50% 不透明度的紅色 (`FF0000`)，請傳入 `0xFF0000@0x80`、`0xFF0000@0.5`、`#FF0000@0x80` 或 `#FF0000@0.5`。<br><br>* 使用 FFmpeg 顏色關鍵字，並使用 `@` 附加不透明度。不透明度支援 `0.5` 等十進位值。例如，若要指定 50% 不透明度的 `0xF0F8FF`，請傳入 `AliceBlue@0.5`。<br><br><br>> **说明**<br><br><br><br>* > 如需顏色定義和更多顏色關鍵字，請參閱 [FFmpeg color syntax](https://ffmpeg.org/ffmpeg-utils.html#color-syntax)。<br><br><br>* > 不透明度值越大，透明度越低。<br><br><br>* > 當不透明度指定為十進位時，有效範圍為 `[0,1]`，最多支援兩位小數。<br> |

## 回應參數

如需唯一的 API 特定回應參數，請參閱下表。如需詳細資訊，請參閱[請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)章節。

|參數 |資料類型 |範例值 |描述 |
|---|---|---|---|
|Code |Integer |`0` |狀態碼。 |
|Message |String |`success` |狀態訊息。 |
|Data |[Data](https://docs.byteplus.com/en/docs/24/118403#data) 的物件 |`-` |任務資訊。 |

### Data

|參數 |資料類型 |範例值 |描述 |
|---|---|---|---|
|TaskID |String |`b71c61****24ae4f` |任務 ID。 |

## 範例

### 範例請求

**原始 (ASR) 字幕（整句顯示）**

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

**原始 (ASR) 字幕（直播顯示）**

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

**字幕翻譯**

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

**配音音訊 + 雙語字幕**

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

**配音音訊 + 唇形同步 + 雙語字幕**

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

### 範例回應

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

## 錯誤碼

如需錯誤碼的詳細資訊，請參閱[通用錯誤碼](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes)。
