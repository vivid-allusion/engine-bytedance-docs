---
title: "Web 播放器 SDK：SDK 概述"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-introduction-to-the-player-sdk-for-web-zh-TW"
---

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">本文適用於 BytePlus MediaLive Web 播放器 SDK 1.x 版本。強烈建議升級至最新版本，以獲得最佳播放體驗。</div>


BytePlus MediaLive Web 播放器 SDK（亦稱 VePlayer），結合 [BytePlus MediaLive 的串流服務](https://www.byteplus.com/en/product/medialive)，為直播內容提供流暢、穩定且高品質的播放解決方案。此 SDK 支援多種作業系統。您可以輕鬆整合至現有的網頁應用程式。

<span id="fe6b462a"></span>
## SDK 示範

若要體驗 SDK 示範，請造訪 [VePlayer](https://demo.byteplus.com/common/veplayer/basic/example)，並切換不同分頁以探索各項功能。提供範例程式碼協助您學習如何實現功能，您亦可調整程式碼以觀察播放器行為的變化。

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4e7e7ac0d5984d6a88e824809da38da1~tplv-goo7wpa0wc-image.image) </span>

<span id="6e1358a3"></span>
## 協議支援

下表列出播放器 SDK 支援的串流協議：


|**協議** |**優缺點** |**H.264** ||**H.265** ||
|---|---|---|---|---|---|
|||**PC** |**行動裝置** |**PC** |**行動裝置** |
|HLS |* 相容性廣<br><br>* 延遲較高 |支援 |支援 |支援 |部分支援 |
|FLV |* 延遲低<br><br>* H5 支援度較差 |支援 |部分支援 |支援 |部分支援 |
|RTM |* 延遲低<br><br>* 弱網環境下表現穩定 |支援 |部分支援 |不支援 |不支援 |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">使用 RTM 協議播放時，瀏覽器必須支援 <a href="https://caniuse.com/?search=WebRTC%20Peer-to-peer%20connections">WebRTC</a>。</div>


* <div data-tips="true" data-tips-type="tip">在 Android 裝置上，部分瀏覽器可能會劫持播放器，導致部分功能無法使用。</div>


* <div data-tips="true" data-tips-type="tip">若要播放以 H.265 編碼且採用 HLS 或 FLV 協議的直播流，須先確認瀏覽器是否支援 H.265 軟體或硬體解碼。</div>



<span id="8af48d51"></span>
## 功能

播放器 SDK 相容主流瀏覽器。會根據作業系統自動選擇最佳播放方案。


|**功能** |**PC** |**行動裝置** |
|---|---|---|
|自訂播放器尺寸 |支援 |支援 |
|自訂封面圖片 |支援 |支援 |
|自動播放 |支援 |支援 |
|同頁多播放器 |支援 |支援 |
|解析度切換 |支援 |支援 |
|全螢幕 |支援 |支援 |
|影片旋轉 |支援 |支援 |
|音量控制 |支援 |支援 |
|畫中畫（PiP） |支援 |部分支援 |
|H.264 |支援 |支援 |
|H.265 |部分支援 |部分支援 |
|自訂錯誤訊息 |支援 |支援 |
|彈幕 |支援 |支援 |
|動態降級至備用串流 |支援 |支援 |
|動態降級至低解析度 |支援 |支援 |
|直播資訊面板 |支援 |支援 |
|日誌上傳 |支援 |支援 |
|播放時移直播內容 |支援 |支援 |
|拉取 RTM 串流 |部分支援 |部分支援 |
|監聽 SEI 訊息 |支援 |支援 |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Web 播放器 SDK 預設啟用自動播放。但部分瀏覽器政策可能會影響自動播放行為。例如，<a href="https://developer.chrome.com/blog/autoplay/">Chrome 的自動播放政策</a>。</div>


* <div data-tips="true" data-tips-type="tip"><a href="https://caniuse.com/?search=HEVC">支援 H.265 硬體解碼的瀏覽器</a>可直接播放 H.265 編碼影片，其他瀏覽器則可透過設定 <code>useSoftDecoding</code> 為 <code>true</code>，啟用軟體解碼以播放 H.265 編碼影片。</div>
