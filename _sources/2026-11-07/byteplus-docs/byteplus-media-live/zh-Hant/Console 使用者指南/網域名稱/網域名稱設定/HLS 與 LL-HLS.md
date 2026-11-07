---
title: "HLS 與 LL-HLS"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/hls-and-ll-hsl-zh-TW"
---

為了降低延遲並提升直播的相容性，您可以設定 HLS 與低延遲 HLS（LL\-HLS）的封裝參數。本主題提供在 BytePlus MediaLive 控制台調整分段時長與數量等參數的逐步操作說明。

<span id="395df62c"></span>
## HLS 的運作方式

瞭解 HLS 傳送直播影片的基本原理，有助於您更有效地設定相關參數。

HLS 會將您的連續直播流切割成多個較小的影片片段，稱為**segments**。HLS 協議會將這些片段的網路位址（URI）列在一個稱為**playlist**（副檔名為`.m3u8`）的文字檔案中。

對於直播流，該播放清單會持續更新：新片段產生時，其位址會加入清單，舊片段的位址則會移除。播放器會重複下載此播放清單，以尋找並播放最新的片段。

這種切割機制就是您會看到**Segment duration**等設定項目的原因。您所設定的片段時長會直接影響播放延遲、穩定性，以及觀眾回溯觀看的能力。

<span id="a77e62f0"></span>
## 限制


* HLS/LL\-HLS 封裝適用於推流、FLV 與 RTMP 協議的源站拉流，以及使用 HLS 的拉流。但不支援基於 HLS 的源站拉流。

* HLS/LL\-HLS 封裝設定不僅適用於此網域下的流，也適用於同一網域空間下其他相關網域的流。

* 若啟用[HLS-ABR](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-configuring-an-hls-abr-task)功能，HLS/LL\-HLS 封裝設定將不適用於該應用。

* 封裝設定約於 3 至 5 分鐘內生效。


<span id="5291f43e"></span>
## 先決條件

需使用支援 LL\-HLS 的播放器。

<span id="1b226441"></span>
## 操作流程


1. 登入[BytePlus MediaLive 控制台](https://console.byteplus.com/live)。

2. 於左側導覽欄點選**Domains**。

3. 找到您欲設定拉流的網域名稱，並於**Actions**欄點選**Settings**。

4. 點選**Advanced settings**頁籤。

5. 於 HLS/LL\-HLS 區塊點選**Edit**，開啟對話框並設定以下參數：

   * **S** **egment duration**：可輸入 1 至 60 的整數。建議直播流的 GOP（畫面組）大小穩定，且片段時長等於或為 GOP 大小的倍數。

   * **Segment number**：播放清單中包含的媒體片段數量。可輸入 2 至 10 的整數。

   * **Segment number in the initial playlist**：初始播放清單中的媒體片段數量。較小的數值可加快初始播放速度。

   * **Low latency HLS**：低延遲 HLS 擴展協議，能在維持可擴展性的同時實現低延遲影片串流。此功能預設為關閉。

   * **Partial segment duration**：低延遲 HLS 會將每個媒體片段分割為更多較小的檔案。這些較小的檔案稱為 Partial Segments。一般媒體片段可能為 6 秒，而 Partial Segment 範例可能僅為 200 毫秒。

   * **Insert PDT**：指定是否在 M3U8 播放清單中插入 #EXT\-X\-PROGRAM\-DATE\-TIME 標籤。

   * **PDT Interval**：若啟用 PDT 插入，則設定插入間隔（秒）。該數值的範圍可以是 0 到 3600。

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">如果將 PDT 間隔設為 0 或小於片段持續時間的值，則每個片段都會插入一個 PDT 標籤。      </div>
