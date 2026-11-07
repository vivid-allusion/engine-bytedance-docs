---
title: "Player SDK for Web：版本資訊"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-changelog_2-zh-TW"
---

本主題是 Player SDK for Web 的官方變更記錄。您可以在此找到所有版本更新的詳細記錄，包括新功能、改進和錯誤修復。

|發行日期 |版本 |說明 |
|---|---|---|
|2026 年 10 月 19 日 |2.13.0 |在 [getRTMStats()](https://docs.byteplus.com/player-sdk-for-web-methods-and-properties-1789729567342#veplayerlive-getrtmstats) 和 [getFLVStats()](https://docs.byteplus.com/player-sdk-for-web-methods-and-properties-1789729567342#veplayerlive-getflvstats) 傳回的播放資訊中，新增 SEI 延遲統計資料。由 [SEIDelayStats](https://docs.byteplus.com/player-sdk-for-web-options-1789729565231#seidelaystats) 類型定義的新增 `delay_s2s` 和 `delay_s2e` 欄位，分別回報伺服器到伺服器延遲和伺服器到終端延遲。 |
|2026 年 6 月 23 日 |2.12.1 |最佳化海外地區的播放日誌上報。建議中國大陸以外地區的應用程式升級至此版本。 |
|2026 年 6 月 08 日 |2.12.0 |* 新增支援在 Tizen 和 webOS 智慧電視系統上整合 Player SDK for Web。建立 SDK 應用程式時，在 **Wildcard domain** 欄位中輸入應用程式識別碼。如需詳細資訊，請參閱[整合 Player SDK for Web](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-player-sdk-for-web_1) 和[取得 SDK 授權](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management)。<br><br>* 啟用嚴格的 app ID 驗證。整合 Player SDK for Web 時，必須同時設定 app ID 和授權。<br><br>* 新增 [isRTMSeiSupported](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1156178?lang=en#isrtmseisupported) 方法，用於檢查目前瀏覽器是否支援從 RTM 串流接收 SEI（Supplemental Enhancement Information）訊息。<br><br>* 修復 HarmonyOS 上百度瀏覽器的播放問題。在此情境中，播放現在預設會回退至 M3U8。<br><br>* 調整 RTM 串流播放實作，防止 `video` 元素的 `src` 被 HeyTap 瀏覽器錯誤攔截。 |
|2026 年 1 月 20 日 |2.11.2 |更新拉取 RTM 串流的自動回退機制。目前播放器僅在以下情況自動觸發回退：<br><br><br>* 瀏覽器或裝置環境不支援 RTM 通訊協定播放，或不支援播放以 H.264 編碼的 RTM 串流。<br><br>* 播放期間發生解碼例外。<br><br><br>對於網路例外造成的 RTM 串流拉取失敗，播放器會觸發自動重試（預設 3 次），不會直接回退。您可以使用 `retryCount` 參數自訂重試次數。 |
|2026 年 1 月 07 日 |2.11.0 |* 為進一步改進 Player SDK for Web 的功能和服務，BytePlus MediaLive 對 Player SDK for Web 啟用授權驗證，並更新計費規則。如需詳細資訊，請參閱 [Player SDK for Web 授權驗證公告](https://docs.byteplus.com/docs/byteplus-media-live/announcement_on_license_validation_for_player_sdk_for_web)。<br><br>* [RTM](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1155423?lang=en#rtm)、[FLV](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1155423?lang=en#flv) 和 [HLS](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1155423?lang=en#hls) 串流的 `retryCount` 預設值從 `0` 變更為 `3`。 |
|2025 年 11 月 27 日 |2.10.3 |* 支援透過 npm 匯入個別外掛程式，以縮減套件大小。如需詳細資訊，請參閱[步驟 1：匯入相依性](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-player-sdk-for-web_1#ceef554f)。<br><br>* 修復透過 `link` 標籤預先載入 JS 會導致錯誤的問題。 |
|2025 年 11 月 12 日 |2.10.2 |* 最佳化 RTM 和 FLV 串流首幀時間的日誌上報邏輯，支援上報各階段的時間分解。<br><br>* 修復 RTM 串流拉取錯誤後降級至其他通訊協定時，日誌上報會停止的問題。<br><br>* 修復 RTM 串流中斷連線後呼叫 [retry](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1156178#retry) 會導致重複錯誤的問題。<br><br>* 修復部分手機上非靜音播放被瀏覽器劫持，導致有音訊但無視訊的問題。 |
|2025 年 10 月 21 日 |2.10.0 |* 傳入 `appId`（應用程式 ID）後，支援設定下發。<br><br>* 修復以下情境中無法隱藏封面圖片的問題：設定 `poster` 參數、停用自動播放（`autoplay: false`），且正在播放 RTM 串流。 |
|2025 年 9 月 2 日 |2.9.2 |修復 HarmonyOS 中，RTM 串流期間點擊靜音或取消靜音無法生效的問題。 |
|2025 年 8 月 6 日 |2.9.1 |修復 RTM 播放失敗會觸發重複錯誤事件的問題。此問題僅影響 V2.8.2 至 V2.9.0 版本。 |
|2025 年 8 月 4 日 |2.9.0 |將 hls 外掛程式替換為 hlsjs 外掛程式。 |
|2025 年 7 月 24 日 |2.8.2 |處理不符合規範的 FLV 規格，以緩解畫面方向顯示不正確的問題。 |
|2025 年 7 月 15 日 |2.8.1 |最佳化 RTM Jitterbuffer 播放策略，根據即時網路狀況動態調整緩衝區時長，以平衡延遲和播放流暢度。 |
|2025 年 7 月 8 日 |2.8.0 |* 在 RTM 中新增 SEI 資料支援，用於同步顯示留言和標記。<br><br>* 啟用商業 DRM（FairPlay、Widevine、PlayReady）以保護影片內容。<br><br>* 改進 RTM 卡頓日誌，以協助診斷弱網路環境中的問題。<br><br>* 實作抖動緩衝區策略，讓 RTM 在網路狀況不佳時播放更流暢。 |
|2025 年 6 月 12 日 |2.7.1 |1. 修復 `userId` 未正確記錄的問題（僅影響 V2.6.1 至 V2.7.0 版本）。這可確保日誌資訊準確記錄使用者識別碼，便於問題追蹤和偵錯。<br><br>2. 修復當 `controls` 設為 `false` 時，切換清晰度或線路無效的問題。這可確保即使控制項被隱藏，切換清晰度或線路功能仍可正確運作。<br><br>3. 最佳化部分 OPPO 行動裝置上的 RTM 串流播放。這解決了在特定 OPPO 行動裝置上播放 RTM 串流時拋出錯誤的問題，確保播放體驗更順暢。 |
|2025 年 5 月 19 日 |2.7.0 |新增對多通訊協定回退的支援，可指定多個通訊協定 URL 和回退順序。回退情境包括：<br><br><br>* 根據定義的回退順序選取支援的通訊協定。<br><br>* RTM 播放失敗後，依序自動回退。<br><br>* 支援失敗時根據錯誤碼回退。<br><br>* 支援不同通訊協定的自訂回退策略。<br><br><br>如需詳細資訊，請參閱[拉取 RTM 串流](https://docs.byteplus.com/docs/byteplus-media-live/RTM-Streaming-Integration)和[拉取 FLV 串流](https://docs.byteplus.com/docs/byteplus-media-live/docs-flv-streaming-integration)。 |
|2025 年 4 月 21 日 |\- |\*\*文件更新：\*\*新增 ABR（Adaptive Bitrate）播放整合指南，可根據即時網路狀況動態調整畫質，以改善觀看體驗。 |
|2025 年 3 月 10 日 |2.6.1 |新增支援透過新的 `mediaElement` 參數傳入 `video` DOM 元素。這讓多個播放器可以共用同一個影片來源。 |
|2024 年 10 月 23 日 |2.5.1 |* isMseSupported、isMMSSupported 和 isFLVSupported 方法支援傳入字串類型的編碼資訊，以判斷瀏覽器對編碼和解碼資訊的支援。<br><br>* 新增日誌上傳設定檢查。未設定 AppID 時，瀏覽器開發者工具主控台會回報錯誤，並使用預設 AppID 進行日誌上報。 |
|2024 年 9 月 06 日 |2.5.0 |* 新功能：<br><br>   * [RTM](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1155423#rtm) 設定支援設定暫停播放後的中斷連線時間，以及中斷連線後重新拉流是否無縫。<br><br>   * 最佳化 LL\-HLS 的實作邏輯。<br><br>   * 新增檢查 iOS 瀏覽器是否支援 FLV 格式串流播放的方法，並支援在 iOS 17.1 及以上版本的瀏覽器中播放 FLV。請參閱 [isFLVSupported](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1156178#isflvsupported) 和 [isMMSSupported](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1156178#ismmssupported) 方法。 |
|2024 年 6 月 12 日 |2.4.0 |* 新功能：<br><br>   * 播放器在拉取 RTM 串流時新增 networkEvaluateInterval（網路評估時間間隔）設定。<br><br>   * 新增 [getRTMNetWorkInfo](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1156178#getrtmnetworkinfo) 方法，支援取得 RTM 拉流的網路評估資訊。<br><br>   * 新增 [getRTMStats](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1156178#getrtmstats) 方法，支援取得 RTM 拉流的播放資訊。<br><br>   * 新增 [getFLVStats](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1156178#getflvstats) 方法，支援取得 FLV 拉流的播放資訊。<br><br>   * FLV 拉流支援自適應位元率（ABR）拉流。<br><br>   * 新增播放器的 playTime 屬性，支援取得目前播放時長。 |
|2024 年 2 月 29 日 |2.3.0 |版本 2.x 相較於版本 1.x 具有以下改進：<br><br><br>* 改進整合流程並縮減套件大小。<br><br>* 增強播放器建立流程。<br><br>* 最佳化播放器設定、方法、屬性和事件格式。<br><br><br>> **说明**<br><br><br>> 版本 2.x 導入破壞性變更，且不相容於隨選視訊（VOD）。如果您想同時播放直播串流和 VOD，請改用舊版 SDK。請參閱 [Player SDK for Web：1.x 版本](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-web-1-x-versions)了解詳細資訊。<br> |
|2023 年 10 月 16 日 |1.6.3 |* 改進：自 v1.6.3 起，SDK 使用新的位址匯入 JS 和 CSS 檔案。您無法使用新位址匯入舊版本的 JS 和 CSS 檔案。請參閱[整合 Player SDK for Web](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-integrating-the-player-sdk-for-web)。<br><br>* 已修復問題：<br><br>   * SDK 播放 RTM 串流時，部分日誌資訊無法上傳。<br><br>   * 錯誤訊息中的 `userId` 值與透過 [liveLogger](https://docs.byteplus.com/docs/byteplus-media-live/docs-api-reference#liveLogger) 傳入的值不一致。 |
|2023 年 5 月 5 日 |1.0.1 |這是 BytePlus MediaLive Player SDK for Web 的第一個版本。 |
