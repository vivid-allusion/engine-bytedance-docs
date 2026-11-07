---
title: "HTTP/3 (QUIC)"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/QUIC_zh-tw"
---

本文件介紹 BytePlus CDN 對 HTTP/3 和 QUIC 協定支援。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">由於協定的機制不同，HTTP/3 (QUIC) 與 Websocket 無法同時啟用。</div>


<span id="概述"></span>
## 概述

CDN 支援的 QUIC 協定包括以下這些：


* Google QUIC (gQUIC)：支援的 gQUIC 版本是 Q043、Q046、Q050。

* IETF QUIC：IETF QUIC 是 HTTP/3 使用的傳輸層協定。


綜上所述，CDN 支援 HTTP/3 以及特定版本的 gQUIC。

在 CDN 中，您可以啟用 "HTTP/3 (QUIC)" 特性。該特性啟用後，CDN 可以處理使用上述協定的使用者請求。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">CDN 支援 QUIC 請求的連線複用。當 CDN 節點收到一個 QUIC 請求，且請求的網域啟用了 HTTPS，則該請求就可以複用節點上其他 QUIC 請求的連線，只要這些 QUIC 請求使用相同的憑證。</div>


<span id="http-3-介紹"></span>
## HTTP/3 介紹

HTTP/3 基於 IETF QUIC，是 HTTP 協定的最新版本，具備以下優勢：


* **低延遲**：QUIC 使金鑰交換和支援的協定成為初始握手過程的一部分。在伺服器回應客戶端連線時，回應資料包包含了資料加密所需要的資料。客戶端可以使用該資料生成金鑰用來加密需要發送的資料包。在建立 HTTPS 連線時，客戶端和伺服器端首先需要進行 TCP 握手，然後再進行 TLS 握手以建立安全連線。

* **網路切換效能較優**：QUIC 包含一個交談識別碼。該識別碼唯一地標識客戶端與伺服器之間的連線。即使客戶端的 IP 位址發生了變化，客戶端只需要發送一個包含此 ID 的資料包即可與伺服器端建立連線。對於 TCP 來說，如果客戶端的 IP 位址發生了變化，已有的 TCP 連線會逾時。之後，客戶端不得不進行冗長的過程與伺服器重新建立連線。

* **弱網情況下的效能良好**：QUIC 基於 UDP。在丟包和網路延遲嚴重的情況下，QUIC 仍可保障服務的可用性。


<span id="前提條件"></span>
## 前提條件

要啟用該設定，您的網域名稱必須已經啟用了 HTTPS 加密服務。

<span id="操作步驟"></span>
### 操作步驟

要對一個網域名稱啟用該配置，您需要在一個未發布的加密策略中進行配置，然後發布該策略並將其綁定該網域名稱。如果該網域名稱已綁定了一個策略，可以通過 [策略複製](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-policy-cn#%E5%A4%8D%E5%88%B6%E7%AD%96%E7%95%A5) 創建一個未發布的策略。


1. 打開 **HTTP/3 (QUIC)**  設定頁面。操作步驟參見 [網域名稱設定](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_zh-tw)。

2. 在 **HTTP/3 (QUIC)**  下方，設置 **狀態** 為啟用。

3. 配置完成後，點擊 **儲存**。


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_b61bb6ab0f0334cda0c030a75649a632.png) </span>
