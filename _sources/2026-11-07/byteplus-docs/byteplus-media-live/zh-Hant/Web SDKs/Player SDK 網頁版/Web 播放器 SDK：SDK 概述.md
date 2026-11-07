---
title: "Web 播放器 SDK：SDK 概述"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-web-sdk-overview-zh-TW"
---

BytePlus MediaLive Web 播放器 SDK（亦稱 VePlayer），結合 [BytePlus MediaLive 的串流服務](https://www.byteplus.com/en/product/medialive)，為直播內容提供流暢、穩定且高品質的播放解決方案。此 SDK 支援多種作業系統。您可以輕鬆整合至現有的網頁應用程式。

<span id="ff05fffc"></span>
## 授權類型

Web 播放器 SDK 提供三種授權類型：基礎、進階及試用。


* **基礎授權**：適用於僅需基本拉流功能的直播場景，例如體育賽事、娛樂、電商及教育。

* **進階授權**：適用於需同時具備基本拉流功能及進階功能（如自適應碼率（ABR）串流、自適應緩衝策略及 [Real Time Media（RTM）](https://docs.byteplus.com/en/byteplus-media-live/docs/introduction-to-real-time-media)）的直播場景。如需更多資訊，請參閱 [功能](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-web-sdk-overview-zh-TW#ba9be9fe)。

* **試用授權**：適用於測試等試用場景。包含 Web 播放器 SDK 的所有功能。


<span id="b49f0040"></span>
## 版本

Web 播放器 SDK 2.x 相較於 1.x 版本，具備以下優化：


* 整合流程優化，並減少套件體積；

* 播放器建立流程增強；

* 播放器配置、方法、屬性及事件格式優化。


這些優化大幅提升播放器效能與用戶體驗，同時促進整合與使用。建議升級至 2.x 版本，以獲得更佳的播放器效能與體驗。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">2.x 版本引入不相容變更，且不支援隨選視訊（VOD）功能。若需播放直播與 VOD，請使用先前版本的 SDK。詳情請參閱 <a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-web-1-x-versions">Web 播放器 SDK：1.x 版本</a>。</div>


<span id="356d2ba0"></span>
## SDK 示範

如需體驗 SDK 示範，請造訪 [VePlayer](https://demo.byteplus.com/common/veplayer/v2/basic/example?tab=function-display)，並切換標籤以探索不同功能。提供範例程式碼，協助您學習功能實現方式，並可調整程式碼以觀察播放器行為變化。

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ee01088a972943a385f4f2ba99ab856b~tplv-goo7wpa0wc-image.image) </span>

<span id="600333d3"></span>
## 協議支援

下表列出 Web 播放器 SDK 支援的串流協議：


|**協議** |**特性** |**H.264** ||**H.265** ||
|---|---|---|---|---|---|
|||**PC** |**行動裝置** |**PC** |**行動裝置** |
|HLS |* 廣泛相容性<br><br>* 高延遲 |支援 |支援 |支援 |部分支援 |
|FLV |* 低延遲<br><br>* H5 支援較差 |支援 |部分支援 |支援 |部分支援 |
|RTM |* 低延遲<br><br>* 弱網路連線下具韌性 |支援 |部分支援 |不支援 |不支援 |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">使用 RTM 協議播放時，瀏覽器必須支援 <a href="https://caniuse.com/?search=WebRTC%20Peer-to-peer%20connections">WebRTC</a>。</div>


* <div data-tips="true" data-tips-type="tip">在 Android 裝置上，部分瀏覽器可能會劫持播放器，導致部分功能無法使用。</div>


* <div data-tips="true" data-tips-type="tip">若需播放以 H.265 編碼且採用 HLS 或 FLV 協議的直播流，請先確認瀏覽器是否支援 H.265 軟體或硬體解碼。</div>



<span id="ba9be9fe"></span>
## 功能

Web 播放器 SDK 相容主流瀏覽器。會根據作業系統自動選擇最佳播放方案。


|**功能** |**PC** |**行動裝置** |
|---|---|---|
|自訂播放器尺寸 |支援 |支援 |
|自訂封面圖片 |支援 |支援 |
|自動播放 |支援 |支援 |
|同頁多播放器 |支援 |支援 |
|解析度切換 |支援 |支援 |
|截圖 |支援 |支援 |
|全螢幕 |支援 |支援 |
|影片旋轉 |支援 |支援 |
|音量控制 |支援 |支援 |
|畫中畫（PiP） |支援 |不支援 |
|H.264 |支援 |支援 |
|H.265 |部分支援 |部分支援 |
|URL 驗證 |支援 |支援 |
|Referer 允許清單與封鎖清單 |支援 |支援 |
|IP 允許清單與封鎖清單 |支援 |支援 |
|自訂錯誤訊息 |支援 |支援 |
|彈幕 |支援 |支援 |
|動態降級至備用串流 |支援 |支援 |
|動態降級至較低解析度 |支援 |支援 |
|直播資訊面板 |支援 |支援 |
|日誌上傳 |支援 |支援 |
|播放時移直播內容 |支援 |支援 |
|監聽 SEI 訊息 |支援 |支援 |
|[播放 RTM 串流](https://docs.byteplus.com/en/docs/byteplus-media-live/RTM-Streaming-Integration) |僅高級版或試用授權部分支援 |僅高級版或試用授權部分支援 |
|[ABR 串流](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-adaptive-bitrate-streaming-abr) |僅高級版或試用授權支援 |僅高級版或試用授權部分支援 |
|[自適應緩衝策略](https://docs.byteplus.com/en/docs/byteplus-media-live/adaptive-buffer-strategy) |僅高級版或試用授權部分支援 |僅高級版或試用授權部分支援 |
|[低延遲 FLV 拉流](https://docs.byteplus.com/en/docs/byteplus-media-live/achieving_2-3s_live_stream_latency_with_low-latency_FLV_web) |僅高級版或試用授權支援 |僅高級版或試用授權部分支援 |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Web 版 Player SDK 預設啟用自動播放。但部分瀏覽器政策可能會影響自動播放行為。例如，請參閱<a href="https://developer.chrome.com/blog/autoplay/">Chrome 的自動播放政策</a>。</div>


* <div data-tips="true" data-tips-type="tip">畫中畫（PiP）功能是基於 PC 端 Chrome 瀏覽器所提供的<a href="https://www.w3.org/TR/picture-in-picture/">畫中畫</a>支援實現。</div>


* <div data-tips="true" data-tips-type="tip"><a href="https://caniuse.com/?search=HEVC">支援 H.265 硬體解碼的瀏覽器</a>可直接播放 H.265 視訊。對於其他瀏覽器，可透過設定<code>degradation</code>參數啟用軟體解碼。</div>
