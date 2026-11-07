---
title: "OpenAPI 變更日誌"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-changelog-1-zh-TW"
---

## 2026\-10

|API |發布時間 |變更記錄 |相關功能 |
|---|---|---|---|
|更新 [CreateSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/CreateSpeechTask) |2026\-10\-21 |新增請求參數 `Callback` 和 `Sei`。`Callback` 指定用於接收 AI 配音回呼訊息的 URL。`Sei` 指定是否將字幕寫入直播流中的 SEI 訊息。 |AI 配音 |
|更新 [CreateSubtitleTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createsubtitletranscodepreset-2023) ||新增請求參數 `SIOutput`，其中包含 `Callback` 和 `Sei`。`Callback` 指定用於接收 AI 配音回呼訊息的 URL。`Sei` 指定是否將字幕寫入直播流中的 SEI 訊息。 |字幕設定 |
|更新 [UpdateSubtitleTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatesubtitletranscodepreset-2023) ||||
|更新 [ListVhostSubtitleTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostsubtitletranscodepreset-2023) ||新增回應參數 `SIOutput`，其中包含 `Callback` 和 `Sei`。`Callback` 傳回用於接收 AI 配音回呼訊息的 URL。`Sei` 傳回字幕是否寫入直播流中的 SEI 訊息。 ||
|更新 [DescribeSubtitleTranscodePresetDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/DescribeSubtitleTranscodePresetDetail) ||||

## 2026\-09

|API |發布時間 |變更記錄 |相關功能 |
|---|---|---|---|
|更新 [CreateWatermarkPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createwatermarkpreset-2023) |2026\-09\-07 |* 新增請求參數 `TransSuffixs`，用於指定浮水印設定適用的轉碼流或 ABR 子流尾碼。<br><br>* 僅當 `WatermarkMode` 設為 `static` 時，請求參數 `PosX` 和 `PosY` 為必填。<br><br>* 新增請求參數 `WatermarkMode`，用於指定浮水印類型。<br><br>* 新增請求參數 `DynamicMode` 和 `DynamicSpeedLevel`，用於設定動態浮水印。 |浮水印 |
|更新 [UpdateWatermarkPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatewatermarkpreset-2023) ||* 新增請求參數 `TransSuffixs`，用於指定浮水印設定適用的轉碼流或 ABR 子流尾碼。<br><br>* 新增請求參數 `WatermarkMode`，用於指定浮水印類型。<br><br>* 新增請求參數 `DynamicMode` 和 `DynamicSpeedLevel`，用於設定動態浮水印。<br><br>* 更新選填請求參數的處理方式。如需更多資訊，請參閱[使用情境](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatewatermarkpreset-2023?lang=en#usage-scenario)。 ||
|更新 [ListWatermarkPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listwatermarkpreset-2023) ||* 新增回應參數 `WatermarkMode`，用於取得浮水印類型。<br><br>* 新增回應參數 `TransSuffixs`，用於取得浮水印設定適用的轉碼流或 ABR 子流尾碼。<br><br>* 新增回應參數 `DynamicMode` 和 `DynamicSpeedLevel`，用於取得動態浮水印設定。 ||
|更新 [ListVhostWatermarkPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostwatermarkpreset-2023) ||||

## 2026\-08

|API |發布時間 |變更記錄 |相關功能 |
|---|---|---|---|
|更新 [CreatePullToPushTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createpulltopushtask-2023) |2026\-08\-13 |新增請求參數 `PullRequestHeaders`，用於設定轉推任務從直播來源或 VOD 來源拉取內容時，拉流請求中包含的 HTTP 請求標頭。支援的標頭為 `Referer` 和 `UserAgent`。 |轉推 |

## 2026\-07

|API |發布時間 |變更記錄 |相關功能 |
|---|---|---|---|
|更新 [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) |2026\-07\-22 |新增 `udp_websdk` 作為 `Protocol` 回應參數的新值，以支援為 BytePlus MediaLive Player SDK for Web 產生 RTM 拉流位址。 |拉流位址 |

## 2026\-06

|API |發布時間 |變更記錄 |相關功能 |
|---|---|---|---|
|更新 [CreateTranscodePresetBatch](https://docs.byteplus.com/en/docs/byteplus-media-live/CreateTranscodePresetBatch-2023) |2026\-06\-25 |新增請求參數 `IsRtmAbr`，並為 `Type` 參數新增值 `rtm-abr`，以支援建立 ABR 設定時使用 RTM\-ABR 通訊協定類型。 |ABR 設定 |
|更新 [DeleteTranscodePresetBatch](https://docs.byteplus.com/en/docs/byteplus-media-live/DeleteTranscodePresetBatch-2023) ||為 `Type` 參數新增值 `rtm-abr`，以支援刪除 RTM\-ABR 通訊協定類型的 ABR 設定。 ||

## 2026\-04

|API |發布時間 |變更記錄 |相關功能 |
|---|---|---|---|
|新增 [CreateSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/CreateSpeechTask) |2026\-04\-21 |新增 AI 配音任務 API，包括建立、更新、重新啟動、刪除、查詢和搜尋任務。 |AI 配音 |
|新增 [UpdateSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/UpdateSpeechTask) ||||
|新增 [RestartSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/RestartSpeechTask) ||||
|新增 [DeleteSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/DeleteSpeechTask) ||||
|新增 [GetSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSpeechTask) ||||
|新增 [SearchSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/SearchSpeechTask) ||||
|新增 [GetSpeechConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSpeechConfig) ||新增用於取得目前帳號可用 AI 配音設定的 API。 ||
|更新 [CreateSubtitleTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createsubtitletranscodepreset-2023) ||字幕設定 API 新增 AI 配音模式支援，包括建立、更新、列出和查詢字幕設定詳細資料。 ||
|更新 [UpdateSubtitleTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatesubtitletranscodepreset-2023) ||||
|更新 [ListVhostSubtitleTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostsubtitletranscodepreset-2023) ||||
|更新 [DescribeSubtitleTranscodePresetDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/DescribeSubtitleTranscodePresetDetail) ||||
|新增 [GetSubtitleTranscodePresetConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSubtitleTranscodePresetConfig) ||新增用於取得目前帳號在字幕設定的 AI 配音模式中可用字型和語言的 API。 ||

## 2025\-12

|API |發布時間 |變更記錄 |相關功能 |
|---|---|---|---|
|更新 [CreateRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createrecordpresetv2-2023) |2025\-12\-22 |新增請求參數 `VodRegion`，用於設定 VOD 區域。 |錄製 |
|更新 [UpdateRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updaterecordpresetv2-2023) ||||
|更新 [ListVhostRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostrecordpresetv2-2023) ||新增回應參數 `VodRegion`，用於取得 VOD 區域。 ||

## 2025\-10

|API |發布時間 |變更記錄 |相關功能 |
|---|---|---|---|
|更新 [GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) |2025\-10\-14 |新增回應參數 `AuthType`，用於取得產生推流或拉流位址的 URL 鑑權類型。 |URL 鑑權 |
|更新 [GeneratePushURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generatepushurl-2023) ||||
|更新 [DescribeAuth](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeauth-2023) ||新增回應參數 `AuthType`，用於取得 URL 鑑權類型。 ||
|更新 [UpdateAuthKey](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updateauthkey-2023) ||* 新增請求參數 `TimeStampBase`，用於設定時間戳記的時間格式。<br><br>* 新增請求參數 `AuthType`，用於設定 URL 鑑權類型。 ||

## 2025\-09

|API |發布時間 |變更記錄 |相關功能 |
|---|---|---|---|
|新增 [DescribeLiveBatchSourceStreamMetrics](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivebatchsourcestreammetrics) |2025\-09\-15 |支援取得特定時間範圍內，特定拉流網域下全部或指定回源拉流的監控資料，例如音訊和視訊的幀率與位元率。您可以使用監控資料評估回源拉流的健康狀態。 |資料統計 |
|新增 [DescribeLiveStreamCountData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivestreamcountdata) ||支援取得特定時間範圍內，指定推流、回源拉流或轉碼流的峰值數量。 ||
|新增 [CreateSnapshotPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/createsnapshotpresetv2) ||以此 API 取代 `CreateSnapshotPreset`，用於新增截圖設定。 |截圖設定 |
|新增 [UpdateSnapshotPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/updatesnapshotpresetv2) ||以此 API 取代 `UpdateSnapshotPreset`，用於更新截圖設定。 ||
|新增 [ListVhostSnapshotPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/listvhostsnapshotpresetv2) ||以此 API 取代 `ListVhostSnapshotPreset`，用於取得截圖設定資訊。 ||

## 2025 年 5 月

|API |發布日期 |說明 |相關功能 |
|---|---|---|---|
|新增 [UpdateRemoteAuth](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updateremoteauth-2023) |2025\-05\-29 |新增遠端鑑權 API，用於設定、查詢、刪除和列出直播推流的鑑權設定。 |遠端鑑權 |
|新增 [DescribeRemoteAuth](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeremoteauth-2023) ||||
|新增 [DeleteRemoteAuth](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deleteremoteauth-2023) ||||
|新增 [ListVhostRemoteAuth](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostremoteauth-2023) ||||

## 2025 年 4 月

|API |發布日期 |說明 |相關功能 |
|---|---|---|---|
|新增 [CreateCarouselTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createcarouseltask) |2025\-04\-14 |新增直播循環播放 API，支援動態內容更新、播放順序設定、片頭略過和即時切換。 |循環播放清單設定 |
|新增 [DeleteCarouselTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletecarouseltask) ||||
|新增 [UpdateCarouselTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatecarouseltask) ||||
|新增 [GetCarouselDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-getcarouseldetail) ||||
|新增 [ListCarouselTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listcarouseltask) ||||
|新增 [DescribeLiveCallbackData](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelivecallbackdata) ||新增用於查詢直播發布相關回呼記錄的 API。此 API 提供事件類型、狀態、請求和回應資料，用於診斷異常回呼和驗證回呼送達。 |回呼 |

## 2025 年 2 月

|API |發布日期 |說明 |相關功能 |
|---|---|---|---|
|更新 [DescribeLiveStreamSessionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivestreamsessiondata) |2025\-02\-05 |1. 已從 API 請求中移除 `RefererList` 參數及相關值，簡化查詢流程。<br><br>2. 已引入新的 `HitRate` 和 `TotalHitRate` 參數，以提供邊緣請求命中率的更詳細洞察。 |統計與分析 |

## 2025 年 1 月

|API |發布日期 |說明 |相關功能 |
|---|---|---|---|
|更新 [CreateRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createrecordpresetv2-2023) |2025\-01\-22 |將請求參數 `SliceDuration` 的取值範圍從 [5,30] 變更為 [2,100]。 |錄製設定 |

## 2024 年 12 月

|API |發布日期 |說明 |相關功能 |
|---|---|---|---|
|新增 [CreateLivePadPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createlivepadpreset-2023) |2024\-12\-20 |新增管理備用流設定和備用流管理的相關 API。 |備用流 |
|新增 [DescribeLivePadPresetDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelivepadpresetdetail-2023) ||||
|新增 [UpdateLivePadPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatelivepadpreset-2023) ||||
|新增 [DeleteLivePadPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletelivepadpreset-2023) ||||
|新增 [DescribeLivePadStreamList](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelivepadstreamlist-2023) ||||
|新增 [StopLivePadStream](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-stoplivepadstream-2023) ||||
|新增 [DescribeLiveTopPlayData](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelivetopplaydata-2023) |2024\-12\-09 |新增用於查詢 TOPN 直播流或網域流量與頻寬資訊的介面。 |統計與分析 |

## 2024 年 10 月

|API |發布日期 |說明 |相關功能 |
|---|---|---|---|
|更新 [回呼說明](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-callback-description) |2024\-10\-16 |Relay 的回呼訊息已新增 PlayProgress 欄位，用於傳回隨選視訊 (VOD) 檔案的播放時長（秒）。僅當拉流來源為 VOD 檔案 (Type=1) 時，才會傳回此欄位。<br><br>**變更影響**<br><br><br>* **適用情境**：如果您正在拉取 VOD 來源進行推流，此欄位可更精確追蹤播放進度。適用於廣告插入和內容切換等需要進度同步的情境。<br><br>* **不受影響的情境**：如果您正在拉取直播流來源進行推流，此變更不會影響您。 |回呼 |
|更新 [回呼說明](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-callback-description) |2024\-10\-11 |為支援錄製更大的檔案，並避免檔案過大造成的資料溢位問題，Recording 回呼訊息中表示錄製檔案大小的 size 欄位類型已從 Integer 更新為 Long。這提升了處理大型檔案時的穩定性和準確性。 |回呼 |

## 2024 年 9 月

|API |發布日期 |說明 |相關功能 |
|---|---|---|---|
|更新 [CreateRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createrecordpresetv2-2023) |2024\-09\-18 |支援為轉碼流建立錄製設定。並支援將錄製檔案儲存在 BytePlus TOS。 |錄製 |
|更新 [UpdateRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updaterecordpresetv2-2023) ||||
|更新 [ListVhostRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostrecordpresetv2-2023) ||||
|更新 [DescribeRecordTaskFileHistory](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describerecordtaskfilehistory-2023) ||||
|更新 CreateSnapshotPreset ||支援將截圖檔案儲存至 BytePlus TOS。 |截圖擷取 |
|更新 UpdateSnapshotPreset ||||
|更新 ListVhostSnapshotPreset ||||
|更新 [DescribeCDNSnapshotHistory](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describecdnsnapshothistory-2023) ||||
|更新 [CreateTimeShiftPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createtimeshiftpresetv2-2023) ||時移檔案儲存支援 BytePlus TOS。 |時移 |
|更新 [ListTimeShiftPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listtimeshiftpresetv2-2023) ||||
|更新 [CreatePullToPushTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createpulltopushtask-2023) ||支援設定隨選視訊的循環播放次數。並支援為串流輸出的視訊新增浮水印。 |轉推 |
|更新 [UpdatePullToPushTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatepulltopushtask-2023) ||||

## 2024 年 8 月 02 日

|**API** |**類型** |**說明** |
|---|---|---|
|* [CreatePullToPushTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createpulltopushtask-2023)<br><br>* [ListPullToPushTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listpulltopushtask-2023)<br><br>* [RestartPullToPushTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-restartpulltopushtask-2023)<br><br>* [StopPullToPushTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-stoppulltopushtask-2023)<br><br>* [DeletePullToPushTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletepulltopushtask-2023)<br><br>* [UpdatePullToPushTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatepulltopushtask-2023) |更新 |新增、更新、刪除、查詢、啟用和停用 Group 參數，用於在 BytePlus 中建立、更新、刪除、查詢、啟用和停用 Relay 介面。 |
|* [ListPullToPushTaskV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listpulltopushtaskv2-2023)<br><br>* [CreatePullToPushGroup](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createpulltopushgroup-2023)<br><br>* [DeletePullToPushGroup](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletepulltopushgroup-2023) |新增 |為查詢 Relay 任務清單，我們新增了支援 POST 方法的介面。<br><br>支援建立、更新和刪除轉推任務群組。 |
|* [CreateSubtitleTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createsubtitletranscodepreset-2023)<br><br>* [DeleteSubtitleTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletesubtitletranscodepreset-2023)<br><br>* [UpdateSubtitleTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatesubtitletranscodepreset-2023)<br><br>* [ListVhostSubtitleTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostsubtitletranscodepreset-2023) |新增 |支援建立字幕設定、將字幕新增至指定轉碼流，並支援字幕翻譯。 |

## 2024 年 7 月 19 日

|**API** |**類型** |**說明** |
|---|---|---|
|* [UpdateEncryptHLS](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updateencrypthls)<br><br>* [DescribeEncryptHLS](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeencrypthls)<br><br>* [GetHLSEncryptDataKey](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-gethlsencryptdatakey) |新增 |支援設定 HLS 加密所需的金鑰取得位址。 |
|* [BindEncryptDRM](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describecertdrm_1)<br><br>* [ListBindEncryptDRM](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describecertdrm_4) |已更新 |支援新增 HLS 標準加密設定。 |

## 2024 年 6 月 30 日

|**API** |**類型** |**說明** |
|---|---|---|
|[CreateDomainV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-dj3h3u96xn) |已更新 |支援為每個網域設定加速區域。 |
|* [UpdateRegionAccessRule](https://docs.byteplus.com/docs/byteplus-media-live/docs-updateregionaccessrule)<br><br>* [DescribeRegionAccessRule](https://docs.byteplus.com/docs/byteplus-media-live/docs-describeregionaccessrule) |已更新 |支援省級區域限制設定。 |

## 2024 年 4 月 16 日

|**API** |**類型** |**說明** |
|---|---|---|
|* [UpdateHLSConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/updatehlsconfig)<br><br>* [DescribeHLSConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/describehlsconfig)<br><br>* [DeleteHLSConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/deletehlsconfig) |新增 |更新、描述和刪除 HLS 設定。 |
|* [UpdateCMAFConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/updatelatencyconfig)<br><br>* [DescribeCMAFConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/describecmafconfig)<br><br>* [DeleteCMAFConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/deletecmafconfig) |新增 |更新、描述和刪除 DASH 設定。 |
|* [UpdateLatencyConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/updatelatencyconfig)<br><br>* [DescribeLatencyConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/describelatencyconfig)<br><br>* [DeleteLatencyConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/deletelatencyconfig) |新增 |更新、描述和刪除延遲設定。 |

## 2024 年 4 月 8 日

|**API** |**類型** |**說明** |
|---|---|---|
|* [CreateTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/createtranscodepresetv2023)<br><br>* [DescribeLiveStreamInfoByPage](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivestreaminfobypagev2023) |已更新 |身為 IAM 使用者，您現在可以建立轉碼範本，並擷取指定直播流的資訊。 |

## 2024 年 3 月 18 日

|**API** |**類型** |**說明** |
|---|---|---|
|[DescribeLiveLogData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivepushstreaminfodata) |新增 |擷取串流播放、串流推送、來源擷取，以及帶推送的串流播放的日誌檔案資訊。 |
|* [CreateTranscodePresetBatch](https://docs.byteplus.com/en/docs/byteplus-media-live/CreateTranscodePresetBatch-2023)<br><br>* [DeleteTranscodePresetBatch](https://docs.byteplus.com/en/docs/byteplus-media-live/DeleteTranscodePresetBatch-2023?lang=en) |新增 |批次設定自適應位元率串流的轉碼範本。 |
|* [ListVhostTransCodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhosttranscodepreset_1)<br><br>* [UpdateTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatetranscodepreset_1) |已更新 |您現在可以查詢和更新自適應位元率串流的轉碼範本。 |
|[DescribeLivePushStreamInfoData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivepushstreaminfodata) |新增 |查詢已結束推流的資訊。 |

## 2024 年 3 月 14 日

|**API** |**類型** |**說明** |
|---|---|---|
|* [EnableHTTPHeaderConfig](https://docs.byteplus.com/docs/byteplus-media-live/docs-enablehttpheaderconfig)<br><br>* [DeleteHTTPHeaderConfig](https://docs.byteplus.com/docs/byteplus-media-live/docs-deletehttpheaderconfig)<br><br>* [DescribeHTTPHeaderConfig](https://docs.byteplus.com/docs/byteplus-media-live/docs-describehttpheaderconfig)<br><br>* [UpdateHTTPHeaderConfig](https://docs.byteplus.com/docs/byteplus-media-live/docs-updatehttpheaderconfig) |新增 |設定回源拉取任務期間傳送至第三方來源伺服器的請求，以及從邊緣伺服器傳送至用戶端的回應中的其他 HTTP 標頭。 |

## 2024 年 3 月 07 日

|**API** |**類型** |**說明** |
|---|---|---|
|[DescribeLiveStreamSessionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivestreamsessiondata?lang=en) |已更新 |您現在可以查詢邊緣伺服器的快取命中率。 |

## 2024 年 3 月 06 日

|**API** |**類型** |**說明** |
|---|---|---|
|* [DescribeRelaySourceRewrite](https://docs.byteplus.com/docs/byteplus-media-live/docs-dakt2mfojk)<br><br>* [DeleteRelaySourceRewrite](https://docs.byteplus.com/docs/byteplus-media-live/docs-3nf0nln2b2)<br><br>* [UpdateRelaySourceRewrite](https://docs.byteplus.com/docs/byteplus-media-live/docs-updaterelaysourcerewrite) |新增 |設定隨選回源拉取任務的來源位址重寫規則。 |

## 2024 年 2 月 07 日

|**API** |**類型** |**說明** |
|---|---|---|
|[ListCertV2](https://docs.byteplus.com/docs/byteplus-media-live/docs-listcertv2) |新增 |查詢您帳號下的 SSL 憑證。 |

## 2024 年 1 月 25 日

|**API** |**類型** |**說明** |
|---|---|---|
|* [DescribeLicenseDRM](https://docs.byteplus.com/docs/byteplus-media-live/docs-describelicensedrm)<br><br>* [DescribeCertDRM](https://docs.byteplus.com/docs/byteplus-media-live/docs-describecertdrm)<br><br>* [UpdateEncryptDRM](https://docs.byteplus.com/docs/byteplus-media-live/docs-updateencryptdrm)<br><br>* [DescribeEncryptDRM](https://docs.byteplus.com/docs/byteplus-media-live/docs-describecertdrm_2)<br><br>* [BindEncryptDRM](https://docs.byteplus.com/docs/byteplus-media-live/docs-describecertdrm_1)<br><br>* [UnBindEncryptDRM](https://docs.byteplus.com/docs/byteplus-media-live/docs-describecertdrm_3)<br><br>* [ListBindEncryptDRM](https://docs.byteplus.com/docs/byteplus-media-live/docs-describecertdrm_4) |新增 |在您的直播流上實作數位版權管理 (DRM) 加密。 |
|* [UpdateIPAccessRule](https://docs.byteplus.com/docs/byteplus-media-live/docs-updateipaccessrule)<br><br>* [DescribeIPAccessRule](https://docs.byteplus.com/docs/byteplus-media-live/docs-describeipaccessrule)<br><br>* [DeleteIPAccessRule](https://docs.byteplus.com/docs/byteplus-media-live/docs-deleteipaccessrule) |新增 |設定 IP 黑名單或白名單，以限制對網域的存取。 |
|* [UpdateRegionAccessRule](https://docs.byteplus.com/docs/byteplus-media-live/docs-updateregionaccessrule)<br><br>* [DescribeRegionAccessRule](https://docs.byteplus.com/docs/byteplus-media-live/docs-describeregionaccessrule)<br><br>* [DeleteRegionAccessRule](https://docs.byteplus.com/docs/byteplus-media-live/docs-deleteregionaccessrule) |新增 |限制來自特定地理區域的請求。 |
|* [UpdateFormatAccessRule](https://docs.byteplus.com/docs/byteplus-media-live/docs-updateformataccessrule)<br><br>* [DescribeFormatAccessRule](https://docs.byteplus.com/docs/byteplus-media-live/docs-describeformataccessrule)<br><br>* [DeleteFormatAccessRule](https://docs.byteplus.com/docs/byteplus-media-live/docs-deleteformataccessrule) |新增 |限制特定通訊協定的直播流拉取請求。 |

## 2024 年 1 月 11 日

|**API** |**類型** |**說明** |
|---|---|---|
|* [DescribeUserAgentAccessRule](https://docs.byteplus.com/docs/byteplus-media-live/docs-describeuseragentaccessrule)<br><br>* [DeleteUserAgentAccessRule](https://docs.byteplus.com/docs/byteplus-media-live/docs-deleteuseragentaccessrule_1)<br><br>* [UpdateUserAgentAccessRule](https://docs.byteplus.com/docs/byteplus-media-live/docs-updateuseragentaccessrule) |新增 |管理 User\-Agent (UA) 黑名單或白名單。 |

## 2023 年 10 月 31 日

|**API** |**類型** |**說明** |
|---|---|---|
|* [CreateDomainV2](https://docs.byteplus.com/docs/byteplus-media-live/docs-dj3h3u96xn) |新增 |建立一個或多個用於推流或拉流的網域。 |
|* [UpdateDomainVhost](https://docs.byteplus.com/docs/byteplus-media-live/docs-updatedomainvhost) |新增 |變更與網域關聯的網域名稱空間。 |
|* [UpdateClusterRateLimit](https://docs.byteplus.com/docs/byteplus-media-live/docs-updateclusterratelimit)<br><br>* [DeleteClusterRateLimit](https://docs.byteplus.com/docs/byteplus-media-live/docs-deleteclusterratelimit)<br><br>* [DescribeClusterRateLimit](https://docs.byteplus.com/docs/byteplus-media-live/docs-describeclusterratelimit) |新增 |管理拉流請求的頻率限制。 |
|* [DeleteRelaySourceV3](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deleterelaysourcev3-2023)<br><br>* [UpdateRelaySourceV3](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updaterelaysourcev3-2023?lang=en) |新增 |管理排程回源拉取任務。 |

## 2023 年 7 月 28 日

|**API** |**類型** |**說明** |
|---|---|---|
|* [UpdateRelaySourceV3](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updaterelaysourcev3-2023?lang=en)<br><br>* [DeleteRelaySourceV3](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deleterelaysourcev3-2023)<br><br>* [DescribeRelaySourceV3](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describerelaysourcev3-2023) |新增 |建立、更新和查詢回源拉取任務。 |
|* UpdateRelaySourceV2<br><br>* DeleteRelaySourceV2<br><br>* DescribeRelaySourceV2 |已刪除 |改用下列端點：<br><br><br>* [UpdateRelaySourceV3](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updaterelaysourcev3-2023?lang=en)<br><br>* [DeleteRelaySourceV3](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deleterelaysourcev3-2023)<br><br>* [DescribeRelaySourceV3](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describerelaysourcev3-2023) |

## 2023 年 7 月 6 日

|**API** |**類型** |**說明** |
|---|---|---|
|* [CreateRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createrecordpresetv2-2023)<br><br>* [ListVhostRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostrecordpresetv2-2023)<br><br>* [UpdateRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updaterecordpresetv2-2023) |新增 |建立、更新和查詢錄製範本。您現在可以使用 BytePlus VOD 儲存錄製內容。 |
|[DescribeRecordTaskFileHistory](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describerecordtaskfilehistory-2023) |已更新 |* 您現在可以查詢儲存在 BytePlus VOD 中的錄製內容。 |
|* [CreateTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/createtranscodepresetv2023)<br><br>* [UpdateTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatetranscodepreset_1)<br><br>* [ListVhostTransCodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhosttranscodepreset_1)<br><br>* [ListCommonTransPresetDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listcommontranspresetdetail-2023) |已更新 |* 已擴大多個參數的取值範圍。<br><br>* 新增參數 `Roi`。此參數決定是否使用低位元率 HD 模式進行轉碼。 |
|* [UpdateCallback](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatecallback-2023)<br><br>* [DescribeCallback](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describecallback-2023) |已更新 |* 您現在可以為回呼設定金鑰，以便驗證 BytePlus MediaLive 傳送的回呼。<br><br>* 此外，[回呼訊息](https://docs.byteplus.com/en/byteplus-media-live/docs/callback-description)新增了新欄位。 |
|* CreateRecordPreset<br><br>* ListVhostRecordPreset<br><br>* UpdateRecordPreset |已棄用 |改用下列端點：<br><br><br>* [CreateRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createrecordpresetv2-2023)<br><br>* [ListVhostRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostrecordpresetv2-2023)<br><br>* [UpdateRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updaterecordpresetv2-2023) |

## 2023 年 6 月 6 日

|**API** |**類型** |**說明** |
|---|---|---|
|* [DescribeLiveBatchPushStreamMetrics](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelivebatchpushstreammetrics-2023)<br><br>* [DescribeLiveSourceStreamMetrics](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivesourcestreammetrics)<br><br>* [DescribeLiveBatchSourceStreamMetrics](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivebatchsourcestreammetrics) |新增 |查詢單個或多個流的推流和拉流統計資料。 |
|* [DescribeLiveSourceTrafficData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivesourcetrafficdata)<br><br>* [DescribeLiveSourceBandwidthData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivesourcebandwidthdata) |新增 |查詢單個或多個流的回源拉流流量和頻寬，即從來源伺服器到邊緣伺服器的流量。 |
|[DescribeLivePlayStatusCodeData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveplaystatuscodedata) |新增 |查詢收到特定狀態碼的拉流請求數量和百分比。 |
|* CreateDomain<br><br>* DescribeDomain<br><br>* ListDomainDetail |已更新 |`Region` 參數現在支援其他值。 |
|[DescribeRecordTaskFileHistory](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describerecordtaskfilehistory-2023) |已更新 |* 回應中新增欄位 `URLExpire`。<br><br>* `TTL` 參數現已棄用。 |
|[DescribeLiveP95PeakBandwidthData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivep95peakbandwidthdata) |已更新 |您現在可以查詢指定網域、串流通訊協定和區域的頻寬資料。 |
|DescribeTranscodeData |已更新 |在回應中新增 `TranscodeType` 欄位，傳回轉碼任務的目標編解碼器和編碼模式。 |
|* [DescribeLiveBandwidthData](https://docs.byteplus.com/en/docs/byteplus-media-live/eescribelivebandwidthdata)<br><br>* [DescribeLiveTrafficData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivetrafficdata)<br><br>* DescribeRecordData<br><br>* DescribePullToPushBandwidthData<br><br>* [DescribeLiveStreamSessionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivestreamsessiondata)<br><br>* [DescribeLiveMetricTrafficData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivemetrictrafficdata)<br><br>* [DescribeLiveMetricBandwidthData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeLivemetricbandwidthdata) |已更新 |查詢跨度和範圍已擴展。在時間粒度為 300 秒時，您可以查詢過去 93 天的資料，並設定最長 31 天的時間範圍。 |
|* DescribeLiveDomainLog<br><br>* DescribeLivePullToPushLog |已更新 |日誌檔案的下載連結現在延長至七天，到期後失效。 |
|用量查詢 API 和統計與分析 API |已更新 |[區域對照表](https://docs.byteplus.com/en/byteplus-media-live/docs/region-map)支援其他區域和國家。 |
|[ListStorageSpaceDetail](https://docs.byteplus.com/en/byteplus-media-live/docs/liststoragespacedetail) |已更新 |`TTL` 參數現已棄用。 |
|DescribePlayResponseStatusStat |已棄用 |請改用 [DescribeLivePlayStatusCodeData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveplaystatuscodedata)。 |

## 2023 年 2 月 6 日

|**API** |**類型** |**說明** |**文件** |
|---|---|---|---|
|GeneratePushURL<br><br>GeneratePlayURL |新增 |* 為指定流產生推流位址。<br><br>* 為指定流產生拉流位址。 |[GeneratePushURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generatepushurl-2023)<br><br>[GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) |

## 2022 年 11 月 29 日

這是 BytePlus MediaLive OpenAPI 的首次發布。
