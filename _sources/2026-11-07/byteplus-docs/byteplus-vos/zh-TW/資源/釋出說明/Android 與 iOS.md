---
title: "Android 與 iOS"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/docs-release-notes-zh-TW"
---

本文件總結了 VideoOne 每個版本的新功能、改進及已修復的缺陷。請參考這些說明，及時瞭解最新產品更新。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">為確保整合順暢並避免與其他 BytePlus SDK 產生依賴衝突，請參考每個版本的元件詳細列表：<a href="https://docs.byteplus.com/docs/byteplus-vos/docs-version-combination-zh-TW">客戶端 SDK 元件</a>。</div>


<span id="a5f5b012"></span>
## 5.5.0

釋出日期：2026/07/13（iOS），2026/07/16（Android）


|**主要更新** |**具體內容** |**說明** |
|---|---|---|
|新增場景並設有獨立入口 |賽事直播 |新增基於 BytePlus MediaLive 構建的賽事直播解決方案，支援多機位視角切換、自適應位元速率（ABR）播放、低延遲直播協議以及互動觀看（禮物、評論、點贊）。[瞭解更多](https://docs.byteplus.com/docs/byteplus-vos/docs-live-sport-streaming-solution-overview-zh-TW) |
|新功能 |投屏 |新增影片播放投屏功能。在 Android 上，演示透過 Chromecast（Google Cast）投屏；在 iOS 上，透過 AirPlay 投屏。 |
|最佳化 |SDK 版本升級 |基礎媒體 SDK 版本已升級至最新，以提升效能與可靠性。請參考[客戶端 SDK 元件](https://docs.byteplus.com/docs/byteplus-vos/docs-version-combination-zh-TW)頁面，以獲取各媒體 SDK 的最新版本。 |


<span id="f50c8ec1"></span>
## 5.4.0

釋出日期：2026/03/05（iOS），2026/03/26（Android）


|**主要更新** |**具體內容** |**說明** |
|---|---|---|
|新功能 |客戶端廣告插入（CSAI） |為短劇解決方案新增客戶端廣告插入（CSAI）能力，實現客戶端無縫廣告整合與變現。詳見[CSAI 整合概述](https://docs.byteplus.com/docs/byteplus-vos/csai-integration-overview-zh-TW)。 |
|（僅限 Android） |新增 ABR 能力 |VideoOne 現已支援影片播放的自適應位元速率流（ABR）。您可在所有 VoD 演示的新設定頁面啟用此功能，自動根據網路狀況調整影片質量。 |
||SDK 版本升級 |基礎媒體 SDK 版本已升級至最新，以提升效能與可靠性。 |
||移除 KTV 演示 |本版本已移除線上 KTV 場景。 |
||缺陷修復 |修復了若干已知問題，提升應用穩定性。 |


<span id="48e1756b"></span>
## 5.3.0

釋出日期：2026/01/27

本次釋出僅包含 **iOS** 演示應用的更新。您可在我們的 [GitHub repository](https://github.com/byteplus-sdk/VideoOneSolutions/commit/bf1667ab02df5bc041f9431919de364a560586a6) 獲取最新程式碼。


|**主要更新** |**具體內容** |**說明** |
|---|---|---|
|新功能 |新增 ABR 能力 |VideoOne 現已支援影片播放的自適應位元速率流（ABR）。您可在所有 VoD 演示的新設定頁面啟用此功能，自動根據網路狀況調整影片質量。 |
|最佳化 |SDK 版本升級 |基礎媒體 SDK 版本已升級至最新，以提升效能與可靠性。 |
||移除 KTV 演示 |本版本已移除線上 KTV 場景。 |
||缺陷修復 |修復了若干已知問題，提升應用穩定性。 |


<span id="1fbd88ba"></span>
## 5.2.0

釋出日期：2025/09/02


|**主要更新** |**具體內容** |**說明** |
|---|---|---|
|通用更新 |證書更新 |iOS 與 Android 的 Effect SDK 證書已更新。 |
|平臺最佳化 |iOS \- 依賴變更 |TTSDK 的依賴方式已由靜態庫變更為動態庫。此舉有助於減小應用安裝包體積，並可能提升效能。 |
||Android \- 合規性更新 |為符合最新標準，我們進行了如下調整：<br><br><br>* 已禁用對非必要感測器資訊的收集。<br><br>* 移除了 MediaLive 的強制許可權及不必要的讀寫許可權，以更好地保護使用者隱私。<br><br>* 修復了若干已知問題，提升了應用的整體穩定性和使用者體驗。 |


<span id="b60dd40e"></span>
## 5.0.0

釋出日期：2025/01/17


|**關鍵更新** |**具體內容** |**描述** |
|---|---|---|
|新增場景並設有獨立入口 |* 短劇 |VideoOne 釋出了新版本，提供專為短劇定製的全套雲端解決方案。 |


<span id="37ddf50f"></span>
## 4.0.1

釋出日期：2024/12/26


|**關鍵更新** |**具體內容** |**描述** |
|---|---|---|
|新增場景並設有獨立入口 |* 媒體上下滑動切換 |VideoOne 釋出了新版本，支援影片與直播的組合播放。同時支援僅包含影片或僅包含直播的播放列表，並允許使用者透過上下滑動切換媒體內容。 |
|TTSDK 版本升級 |* iOS: 1.41.300.203\-rtc —\> 1.43.300.2\-premium<br><br>* Android: 1.41.300.201\-rtc —\> 1.43.300.3 |您也可以參考[客戶端 SDK 元件](https://docs.byteplus.com/docs/byteplus-vos/docs-version-combination-zh-TW)，以獲取 VideoOne 所用各媒體 SDK 的**最新版本**。 |


<span id="e758678f"></span>
## 3.3.0

釋出日期：2024/07/26


|**關鍵更新** |**具體內容** |**描述** |
|---|---|---|
|新增功能並設有獨立入口 |* 首頁使用者介面最佳化<br><br>* RTC API 示例<br><br>* 合唱功能 |本次釋出為線上 KTV 方案新增了合唱場景，提供了 RTC API 示例的接入指引，並最佳化了首頁使用者介面。 |
|TTSDK 版本升級 |* iOS: 1.40.200.5\-premium —\> 1.41.300.203\-rtc<br><br>* Android: 1.39.100.9.onekit —\> 1.41.300.201\-rtc |您也可以參考[客戶端 SDK 元件](https://docs.byteplus.com/docs/byteplus-vos/docs-version-combination-zh-TW)，以獲取 VideoOne 所用各媒體 SDK 的**最新版本**。 |


<span id="e9f89b4f"></span>
## 3.1.0

釋出日期：2024/05/23


|**關鍵更新** |**具體內容** |**描述** |
|---|---|---|
|新增功能並設有獨立入口 |* 直播推流<br><br>* 直播拉流 |本次釋出新增了一個演示，展示如何透過不同來源發起直播，包括攝像頭採集流、螢幕共享流、本地或線上影片檔案及音訊流。同時提供了推流和拉流的附加設定，幫助您快速實現專案中的直播推送與觀看功能。<br><br>實現方式請參考[直播流](https://docs.byteplus.com/docs/byteplus-vos/docs-live-streaming-zh-TW)。 |


<span id="80846653"></span>
## 3.0.0

釋出日期：2024/03/22

本次釋出新增了 **線上 KTV** 場景的解決方案。您可以[安裝應用](https://docs.byteplus.com/docs/byteplus-vos/docs-byteplus-videoone-demo-app-1-zh-TW)進行試用，或參考[整合指南](https://docs.byteplus.com/docs/byteplus-vos/docs-online-ktv-solution-overview-zh-TW)在您的應用中實現該場景。

<span id="d4b47464"></span>
## 2.4.0

釋出日期：2024/01/31


|**關鍵更新** |**具體內容** |**描述** |
|---|---|---|
|**TTSDK** 版本升級 |* iOS: 1.37.200.5\-premium —\> 1.40.200.5\-premium<br><br>* Android: 1.37.200.6.onekit —\> 1.39.100.9.onekit |本次升級對部分 API 進行了調整，尤其涉及互動直播方案相關內容。如果您已將 VideoOne 整合至專案中用於搭建互動直播場景，請務必根據新版本更新程式碼。請參考以下文件中提供的最新示例程式碼，完成必要修改，確保專案正常執行：<br><br><br>* iOS: [在 iOS 上實現互動直播](https://docs.byteplus.com/docs/byteplus-vos/docs-implementing-interactive-live-for-ios-zh-TW)<br><br>* Android: [在 Android 上實現互動直播](https://docs.byteplus.com/docs/byteplus-vos/docs-implementing-interactive-live-for-android-zh-TW)<br><br><br>您也可以參考[客戶端 SDK 元件](https://docs.byteplus.com/docs/byteplus-vos/docs-version-combination-zh-TW)，以獲取 VideoOne 所用各媒體 SDK 的**最新版本**。 |
|**新增功能**並設有獨立入口 |新增功能：<br><br><br>* 常用播放器功能，包括手勢控制、畫中畫等。<br><br>* 影片播放列表<br><br>* 智慧多語種字幕<br><br>* 防錄屏功能 |在本次釋出中，我們精心整理並展示了在主流音影片場景中常用的關鍵功能演示。<br><br>您可以透過點選演示應用底部導航欄中新增加的“**功能**”標籤體驗這些功能，或在開源專案中探索其實現方式。 |


<span id="dd873133"></span>
## 2.3.0

釋出日期：2023/12/07

本版本為演示應用的 **影片播放與編輯**場景新增以下功能。


1. 短影片沉浸式播放模式現已支援橫屏影片播放，並可切換至全屏播放。

2. 在所有型別影片的全屏播放頁面，支援觀眾互動，如點贊和評論。

3. 中長影片半屏播放頁面現新增推薦影片列表。

4. 支援自定義媒體源的播放。詳情請參閱[自定義媒體源播放](https://docs.byteplus.com/docs/byteplus-vos/docs-custom-media-source-playback-zh-TW)文件。


<span id="3ee7537d"></span>
## 2.0.0

釋出日期：2023/11/10


|**功能** |**型別** |**描述** |**相關文件** |
|---|---|---|---|
|影片播放與編輯 |新增 |演示應用已更新，包含影片播放與編輯演示。演示中重點展示以下功能：<br><br><br>* 影片播放<br><br>* 影片拍攝與多軌編輯<br><br>* 媒體上傳 |* [試用 Demo 應用](https://docs.byteplus.com/docs/byteplus-vos/docs-byteplus-videoone-demo-app-1-zh-TW)<br><br>* [方案概述](https://docs.byteplus.com/docs/byteplus-vos/docs-video-playback-edit-solution-overview-zh-TW) |
|無 |文件更新 |新增了一篇文章。該文章全面列出了每個版本的 VideoOne 演示應用所整合的 SDK。按照本文中的版本組合進行整合，可有效避免不同 BytePlus SDK 之間的依賴衝突和相容性問題。 |* [客戶端 SDK 元件](https://docs.byteplus.com/docs/byteplus-vos/docs-version-combination-zh-TW) |


<span id="00391e48"></span>
## 1.0.0

釋出日期：2023/08/04

BytePlus Video One Solution（VideoOne）首次釋出。


|**功能** |**型別** |**描述** |**相關文件** |
|---|---|---|---|
|BytePlus VideoOne 演示應用 |新增 |該開源演示應用整合了多種 BytePlus 媒體 SDK，並結合 BytePlus 影片雲服務，針對行業場景提供演示。<br><br>演示應用重點展示以下功能：<br><br><br>* 直播推流與播放<br><br>* 聯合直播，包括與觀眾或其他直播間主播（主播 PK 對戰）<br><br>* 彈幕<br><br>* 禮物<br><br>* 直播間管理。 |* [試用 Demo 應用](https://docs.byteplus.com/docs/byteplus-vos/docs-byteplus-videoone-demo-app-1-zh-TW)<br><br>* [方案概述](https://docs.byteplus.com/docs/byteplus-vos/docs-interactive-live-streaming-solution-overview-zh-TW) |
