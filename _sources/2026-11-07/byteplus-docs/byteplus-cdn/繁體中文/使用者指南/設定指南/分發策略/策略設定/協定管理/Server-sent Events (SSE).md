---
title: "Server-sent Events (SSE)"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/sse_zh-tw"
---

本文件介紹 BytePlus CDN 中對 SSE 的支援。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">由於協定的機制不同，SSE 與 WebSocket 無法同時啟用。</div>


<span id="e5eee699"></span>
## SSE 概述

Server\-sent Events（SSE）是基於 HTTP 協定的伺服器向用戶端**單向**即時推播技術，透過持久化長連線傳輸文字資料流，適配單向即時通訊場景。

<span id="de85d6a9"></span>
### 核心優勢


* 輕量易用：基於現有 HTTP 協定堆疊，用戶端透過原生 `EventSource` API 快速接入，開發成本低且相容主流瀏覽器。

* 原生可靠性：內建自動重連機制，支援 `id` 欄位實現斷點續傳，保障資料完整性。


<span id="121d7c22"></span>
### 使用場景


* 即時通知（包括社交訊息、訂單更新、維運告警）、即時資料監控（包括金融行情、感測器資料）等單向資料傳輸場景。

* LLM 流式輸出：將大型語言模型產生的回答分段推播給用戶端，實現「打字機」式即時回饋，避免使用者等候，降低傳輸壓力。


<span id="febd2412"></span>
## CDN 對 SSE 的支援

CDN 以「邊緣代理」角色最佳化 SSE 傳輸，核心工作機制聚焦三個關鍵環節：

<span id="6b9c6511"></span>
### 長連線橋接

用戶端請求被路由至就近 CDN 邊緣伺服器，伺服器將請求透傳到來源伺服器並與來源伺服器建立長連線，形成「用戶端 \- 邊緣伺服器 \- 來源伺服器」鏈路，縮短傳輸距離、降低延遲。

<span id="84f98c37"></span>
### 資料流透傳

採用「不篡改、不快取、即時轉發」策略。來源伺服器 SSE 格式資料流到達伺服器後立刻被推播至用戶端，確保資料即時性與完整性。

<span id="275ec1c5"></span>
### 連線複用與穩控

廣播式 SSE 複用來源伺服器連線，減少來源伺erv壓力；個人化 SSE 維護獨立連線鏈避免資料混淆。同時透過合理逾時設定、自動重連及容錯移轉，保障服務可用性。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">如果您啟用了 SSE，也建議您啟用 HTTP/2。HTTP/2 的多路複用特性允許邊緣伺服器與來源伺服器之間只需建立一條 TCP 連線。這條連線可透過多個「流」同時承載多個用戶端的 SSE 資料流（每個用戶端對應一個流），從而有效降低來源伺服器的連線壓力。</div>


<span id="71503458"></span>
## 操作步驟


1. 開啟 **Server\-sent Events** 設定頁面。操作步驟參見 [網域名稱設定](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_zh-tw)。

2. 設定 **狀態** 為啟用。

3. 設定完成後，點擊 **儲存**。


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_d2bd27b1bb4b3a7d6ae867908b77894f.png) </span>
