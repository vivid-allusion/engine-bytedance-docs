---
title: "SDK簡介"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-introduction-zh-TW"
---

BytePlus MediaLive 提供適用於 Android、iOS、React Native 和 Flutter 的 Player SDK。

BytePlus MediaLive SDK 提供三種類型的授權：基本版、高級版和試用版。


* **基本授權**：適用於僅需基本拉流功能的直播場景，例如體育賽事、娛樂、電商和教育。

* **高級授權**：適用於需要基本拉流功能及進階功能（如自適應碼率（ABR）串流、超解析度（SR）和[Real Time Media (RTM)](https://docs.byteplus.com/en/byteplus-media-live/docs/introduction-to-real-time-media)）的直播場景。如需更多資訊，請參閱[Player SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-introduction-zh-TW#b1681aaf)。

* **試用授權**：適用於測試等試用場景。包含 BytePlus MediaLive SDK 的所有功能。


<span id="2a8ebace"></span>
## 功能

Player SDK 支援的功能如下。


|功能 ||描述 |Android 與 iOS |Flutter |React Native |
|---|---|---|---|---|---|
|播放格式 |FLV |支援播放延遲為 6 至 10 秒的 FLV 串流。 |支援 |支援 |支援 |
||FLV（低延遲） |支援播放延遲為 2 至 3 秒的 FLV 串流。 |僅高級授權或試用授權支援 |不支援 |不支援 |
||HLS |支援播放 HLS 串流。 |支援 |支援 |支援 |
||RTM |支援播放高併發、低延遲的 RTM 串流。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">不支持純音訊或純視訊流。</div><br> |僅高級授權或試用授權支援 |支援 |支援 |
||RTMP |支援播放 RTMP 串流。 |支援 |支援 |支援 |
||CMAF |支援播放 CMAF 串流。 |* iOS：不支援<br><br>* Android：僅高級授權或試用授權支援 |* iOS：不支援<br><br>* Android：支援 |* iOS：不支援<br><br>* Android：支援 |
|傳輸協議 |TCP |支援 TCP 協議。 |支援 |支援 |支援 |
||QUIC |支援 QUIC 協議，有效提升影片傳輸效率。 |僅高級授權或試用授權支援 |支援 |支援 |
||TLS |支援 TLS 協議。 |支援 |支援 |支援 |
||HTTP 2.0 |支援 HTTP 2.0 協議。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">不支持 RTM 流。</div><br> |支援 |支援 |支援 |
||HTTP header |請求影片資源時支援自訂 HTTP 標頭。 |支援 |不支援 |支援 |
|影片解碼 |H.264 硬體解碼 |支援 H.264 硬體解碼。 |支援 |支援 |支援 |
||H.264 軟體解碼 |支援 H.264 軟體解碼。 |支援 |支援 |支援 |
||H.265 硬體解碼 |支援 H.265 硬體解碼。透過裝置封鎖清單和智慧播放策略等功能優化 H.265 硬體解碼使用，搭配 H.265 轉碼可降低直播成本並提升影片品質。 |僅高級授權或試用授權支援 |僅高級授權或試用授權支援 |僅高級授權或試用授權支援 |
||H.265 軟體解碼 |支援 H.265 軟體解碼，可提升低階裝置的相容性，協助降低直播成本並提升觀看體驗。 |僅高級授權或試用授權支援 |僅高級授權或試用授權支援 |僅高級授權或試用授權支援 |
||H.265 降級 |若 H.265 硬體解碼失敗，播放器會自動降級，先嘗試切換至已配置的 H.264 備用串流，若無法取得則嘗試使用 H.265 軟體解碼。 |支援 |支援 |支援 |
||H.266 軟體解碼 |支援 H.266 軟體解碼，可提升低階裝置的相容性，協助降低直播成本並提升觀看體驗。 |* iOS：不支援<br><br>* Android：僅高級版或試用授權支援 |不支援 |不支援 |
||AAC\-HE |支援 AAC\-HE 音訊編碼格式。 |支援 |支援 |支援 |
||AAC\-LC |支援 AAC\-LC 音訊編碼格式。 |支援 |支援 |支援 |
|播放控制 |開始與停止播放 |支援開始或停止播放。 |支援 |支援 |支援 |
||暫停與恢復播放 |支援暫停或恢復播放。 |支援 |支援 |支援 |
||取得目前播放狀態 |支援取得目前播放狀態。 |支援 |支援 |支援 |
||手動切換畫質 |支援手動切換不同畫質等級。 |支援 |不支援 |支援 |
||設定播放器緩衝時間 |播放器會預先下載一定量的資料，以確保播放的連續性與流暢性。緩衝時間越長，播放器在網路波動或延遲時越能維持不中斷的影音播放。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">如需實現此功能，請聯繫 BytePlus MediaLive <a href="https://console.byteplus.com/workorder/create">技術支援</a>。</div><br> |支援 |不支援 |支援 |
|視訊效果 |設定渲染視窗 |設定渲染視窗以顯示播放器的視訊內容。 |支援 |支援 |支援 |
||螢幕填充模式 |支援調整播放畫面的填充模式。 |支援 |支援 |支援 |
||螢幕旋轉角度 |支援設定播放畫面的旋轉角度，可順時針旋轉至 0°、90°、180°、270°。 |支援 |支援 |支援 |
||鏡像 |支援設定播放畫面的鏡像模式，例如水平或垂直鏡像。 |支援 |不支援 |支援 |
||子母畫面（PiP）播放 |透過將播放器視窗縮小並置於介面角落，觀眾可在觀看直播的同時瀏覽其他內容或開啟其他應用程式，提升使用者體驗。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">如需實現此功能，請聯繫 BytePlus MediaLive <a href="https://console.byteplus.com/workorder/create">技術支援</a>。</div><br> |支援 |不支援 |支援 |
||SDR（標準動態範圍）視訊播放 |支援 SDR 視訊播放。 |支援 |支援 |支援 |
||超解析度 |超解析度是指從觀察到的低解析度影像重建高解析度影像的過程。即時行動裝置超解析度利用演算法技術，在裝置上即時重建低解析度畫面，並於螢幕上顯示高解析度畫面。此功能可提升視訊內容的細節與對比，優化整體清晰度與觀看體驗。 |僅高級版或試用授權支援 |不支援 |僅高級版或試用授權支援 |
||視訊銳化 |視訊銳化是一種影像處理技術，用於提升視訊影像的清晰度與細節。透過銳化，視訊中的邊緣與細節會更加明顯，使畫面看起來更清晰且更鮮明。 |僅高級版或試用授權支援 |不支援 |支援 |
|音效 |音量調整 |支援調整播放音量。 |支援 |支援 |支援 |
||靜音 |支援靜音播放。 |支援 |支援 |支援 |
||取得靜音狀態 |支援取得目前靜音狀態。 |支援 |支援 |支援 |
||背景音訊播放 |當應用程式切換至背景時，音訊可持續播放。 |支援 |支援 |支援 |
||純音訊播放 |支援播放純音訊。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">僅適用於 FLV 流。</div><br> |支援 |支援 |支援 |
||立體聲音訊 |支援播放立體聲音訊。 |支援 |支援 |支援 |
|播放策略 |播放失敗重試 |若因網路問題或其他狀況導致直播中斷，播放器會嘗試重新播放。 |支援 |支援 |支援 |
||本地 DNS 預解析 |啟用本地 DNS 預解析可優化播放器的啟動時間。 |支持 |支持 |支持 |
||配置一個或多個播放地址 |支持配置一個或多個播放地址。通過配置多個播放地址，可實現依賴多路流的功能，例如 ABR 串流與主備流切換。 |支持 |支持 |支持 |
||ABR 串流 |ABR 是一種串流技術，通過一系列演算法策略動態切換不同畫質的媒體流。此技術可根據網路頻寬變化自適應，有助於防止直播過程中卡頓，提升播放品質與觀看體驗。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">僅適用於 FLV 流。</div><br> |僅高級版或試用授權支持 |支持 |支持 |
||IP 位址串流 |支持直接使用播放域名的 IP 位址進行串流，以縮短首幀時間。 |支持 |不支持 |支持 |
||主備流切換 |當主流地址失效或發生播放錯誤時，播放器會自動切換至備流地址。當備流地址失效或發生播放錯誤時，播放器會切換回主流地址。 |僅高級版或試用授權支持 |支持 |支持 |
||多實例 |支持在同一介面新增多個播放器同時播放。 |支持 |支持 |支持 |
||動態追幀 |直播過程中，視訊流可能因網路波動或其他因素出現延遲或卡頓。動態追幀技術會調整畫面播放速度或跳過部分畫面，以與直播進度同步，降低延遲。 |支持 |支持 |支持 |
||即時播放優化 |縮短首幀時間，實現即時播放。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">若要實現此功能，請聯絡 BytePlus MediaLive <a href="https://console.byteplus.com/workorder/create">技術支援</a>。</div><br> |支持 |不支持 |支持 |
|其他功能 |截圖 |支持在播放器內擷取當前直播畫面。 |支持 |不支持 |支持 |
||SEI 訊息接收 |SEI 會將文字數據嵌入音視頻流，由主播端發送，觀眾端接收，確保文字與音視頻內容精確同步。 |僅高級版或試用授權支持 |支持 |支持 |
||配置事件監聽器 |通過配置事件監聽器，可接收播放器內部狀態資訊，包括播放狀態、錯誤資訊、音視頻首幀回調及週期性統計數據。 |支持 |支持 |支持 |
||訂閱音視頻數據 |訂閱接收解碼後的音視頻畫面，進行自訂處理或渲染。 |支持 |不支持 |不支持 |
|視訊安全 |商用 DRM（數位版權管理） |支持播放 DRM 加密流，並提供 Widevine、FairPlay、PlayReady 等 DRM 解決方案。 |僅高級版或試用授權支持 |不支持 |不支持 |
|品質保證 |日誌上報 |支持上報 SDK 日誌，並收集、分析與音視頻直播相關的播放追蹤數據。 |支持 |支持 |支持 |


<span id="db2409b9"></span>
## 使用 SDK

下表列出整合各 SDK 時可能有用的主題：


|**SDK** |**主題** |
|---|---|
|Android 版播放器 SDK |* [整合 Android Player SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-android-zh-TW)<br><br>* [初始化 Android 版 Player SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-initializing-for-android-zh-TW)<br><br>* [Player SDK for Android: Basic features](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-basic-features-2)<br><br>* [Player SDK for Android: Advanced features](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2)<br><br>* [Player SDK for Android: Overview](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-overview) |
|iOS 版播放器 SDK |* [整合 iOS 的 Player SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-ios-zh-TW)<br><br>* [初始化 iOS 版 Player SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-initializing-for-ios-zh-TW)<br><br>* [Player SDK for iOS: Basic features](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-basic-features-3)<br><br>* [Player SDK for iOS: Advanced features](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3)<br><br>* [Player SDK for iOS: Overview](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api-overview) |
|React Native 版播放器 SDK |* [整合 Player SDK 至 React Native](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-rn-zh-TW)<br><br>* [初始化 React Native 的 Player SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-initializing-for-rn-zh-TW)<br><br>* [Player SDK for React Native: Basic features](https://docs.byteplus.com/docs/byteplus-media-live/docs-rnplayer-basic-features)<br><br>* [Player SDK for React Native: Advanced features](https://docs.byteplus.com/docs/byteplus-media-live/docs-rnplayer-advanced-features)<br><br>* [Player SDK for React Native: Overview](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-api-overview) |
|Flutter 版播放器 SDK |* [整合 Player SDK 至 Flutter](https://docs.byteplus.com/docs/byteplus-media-live/integrating-the-player-sdk-for-flutter-zh-TW)<br><br>* [初始化 Flutter 的 Player SDK](https://docs.byteplus.com/docs/byteplus-media-live/initializing-the-player-sdk-for-flutter-zh-TW)<br><br>* [Player SDK for Flutter: Basic features](https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-basic-features)<br><br>* [Player SDK for Flutter: Advanced features](https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-advanced-features) |


<span id="f202fd8c"></span>
## 詞彙表

如需 SDK 相關術語說明，請參閱[Glossary](https://docs.byteplus.com/docs/byteplus-media-live/docs-glossary)。
