---
title: "WebSocket"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/websocket_zh-tw"
---

本文檔介紹 BytePlus CDN 中對於 Websocket 的支援。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">由於協議的機制不同，如果您啟用了 WebSocket，就無法啟用 HTTP/2 和 HTTP/3 (QUIC)。同樣，如果您啟用了 HTTP/2 或 HTTP/3 (QUIC)，就無法啟用 WebSocket。</div>


<span id="websocket-概述"></span>
## Websocket 概述

Websocket 是一種在單個 TCP 連接上進行全雙工通訊的應用層協定。它允許用戶端和伺服器之間實時雙向通訊，與傳統的 HTTP 請求\-回應模式不同。

Websocket 提供了以下優點：


1. 實時性：伺服器可以向用戶端推送訊息，無需用戶端定期查詢伺服器的狀態，減少了訊息延遲和頻寬消耗。

2. 雙向通訊：用戶端和伺服器都可以向對方發送資料，實現靈活的互動。

3. 高效性：減少了不必要的 HTTP 請求和回應，提高了通訊效率。

4. 持久連接：TCP 連接在建立後可以保持，減少了每次通訊都需要建立連接的開銷。


Websocket 常用於實時聊天、線上遊戲、實時資料更新等場景。Websocket 為實時性要求較高的應用提供了一種有效的解決方案。

<span id="cdn-對-websocket-的支援"></span>
## CDN 對 Websocket 的支援

CDN 支援 Websocket。該特性預設是禁用。如果您需要用戶端和来源伺服器之間進行雙向通訊，您可以啟用該特性。Websocket 啟用後，如果收到了用戶端的 Websocket 請求，CDN 會在 CDN 與来源伺服器之間尋找一條低延遲的公網路由，然後與来源伺服器建立 Websocket 連接。之後，用戶端，CDN，来源伺服器之間就可以進行低延遲雙向通訊了。

對於 CDN 與来源伺服器之間建立的 Websocket 連接，預設的逾時時間是 60s。也就是說，如果 60s 內一個 Websocket 連接上沒有資料傳輸，CDN 會斷開該 Websocket 連接。在開啟 Websocket 時，您也可以指定一個逾時時間。

<span id="操作步驟"></span>
## 操作步驟


1. 打開 **WebSocket** 設定頁面。操作步驟參見 [網域名稱設定](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_zh-tw)。

2. 設定 **狀態** 為啟用。

3. 設定 **WebSocket 逾時時間**。該配置的單位是秒，範圍是 1\-300，預設值是 60。

4. 設定完成後，點擊 **儲存**。


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_b18c64608c5e2805f0fb0771aeab863a.png) </span>
