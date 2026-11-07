---
title: "DASH 與 LL-DASH"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/dash-and-ll-dash-zh-TW"
---

在動態自適應串流（DASH）與低延遲 DASH（LL\-DASH）中，直播串流會被切分為 Common Media Application Format（CMAF）片段。您可以調整片段時長與片段數量設定，以有效降低延遲並提升直播兼容性。

<span id="a77e62f0"></span>
## 限制


* DASH 封裝適用於推流、原點拉流（HLS、FLV 和 RTMP 協議），以及使用 DASH over CMAF 進行拉流。

* DASH 封裝配置適用於指定網域及同一網域名稱空間下的所有其他網域。

* 封裝配置於 3 至 5 分鐘內生效。


<span id="5291f43e"></span>
## 先決條件


* 需使用支援 DASH 的播放器。

* iOS 10.0、macOS 10.12 和 tvOS 10.0 或更高版本的作業系統支援 CMAF 內容。


<span id="1b226441"></span>
## 操作流程


1. 前往 [BytePlus MediaLive 控制台 > 網域](https://console.byteplus.com/live/main/domain/list)。

2. 找到您要配置拉流的網域名稱，並於 **操作**欄點擊 **設定**。

3. 點擊 **進階設定**頁籤。

4. 於 DASH 區塊點擊 **編輯**，開啟對話框並配置以下設定：

   * **CMAF** **片段時長**：您可輸入 1 至 60 的整數。為獲得最佳效能，請確保直播串流的 GOP（Group of Pictures）大小穩定，並將片段時長設為 GOP 大小的整數倍或相等。

   * **片段數量**：播放列表中包含的媒體片段數。您可輸入 3 至 10 的整數。

   * **低延遲 DASH**：低延遲 DASH 擴展協議以實現低延遲視訊串流，同時維持可擴展性。
