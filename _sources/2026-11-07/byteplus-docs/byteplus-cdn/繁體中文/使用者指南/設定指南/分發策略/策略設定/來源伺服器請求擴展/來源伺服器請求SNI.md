---
title: "來源伺服器請求SNI"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/origin-server-sni_zh-tw"
---

<span id="什麼是-sni"></span>
## 什麼是 SNI

SNI 的英文全稱是 Server Name Indication。SNI 是 TLS 協議的擴展。在同一台伺服器上部署了多個站點的場景下，SNI 解決了以下問題：


* 在用戶端使用 HTTPS 協議與伺服器建立連接時，伺服器端無法知道該發送給用戶端哪個站點的憑證。


如果用戶端使用不安全的 HTTP 協議與伺服器端通信，在數據傳輸時，伺服器端通過用戶端請求中的 Host 頭部判斷用戶端需要訪問的站點。但是如果用戶端使用 HTTPS 協議連接伺服器，在數據傳輸開始前有一個 TLS 握手的過程。在該過程中，用戶端還未傳遞 Host 頭部給伺服器。因此伺服器無法獲得 Host 字段信息來判斷需要發送給用戶端的站點憑證。此時，用戶端可以使用 SNI 頭部告知伺服器端需要的目標站點。這樣伺服器端就能在 TLS 握手階段發送相應的憑證給用戶端了。

<span id="來源伺服器請求-sni"></span>
## 來源伺服器請求 SNI

本文討論的 SNI 是 BytePlus CDN 的 "來源伺服器請求 SNI" 配置。 "來源伺服器請求 SNI" 指定了 CDN 在使用 HTTPS 協議向來源伺服器請求內容時需要訪問的來源伺服器網域名稱。如果您的網域名稱啟用了 HTTPS，系統有預設的 "來源伺服器請求 SNI" 設置。預設的 "來源伺服器請求 SNI" 設置如下：


* 如果您沒有指定 "來源伺服器請求 Host"，"來源伺服器請求 SNI" 與網域名稱相同。

* 如果您指定了 "來源伺服器請求 Host"，"來源伺服器請求 SNI" 與 "來源伺服器請求 Host" 相同。


但是在某些場景下，"來源伺服器請求 SNI" 與 "來源伺服器請求 Host" 不相同。如果您有這樣的場景，可以在 CDN 控制台配置 "來源伺服器請求 SNI"。

<span id="操作步驟"></span>
## 操作步驟


1. 打開 **來源伺服器請求 SNI** 設定頁面。操作步驟參見 [網域名稱設定](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_zh-tw)。

2. 在 **來源伺服器請求 SNI** 下方，設置 **狀態** 為 **開啟**。

3. 設置 **SNI 網域名稱** 為目標站點的網域名稱，長度不能超過 1024 個字符。

4. 配置完成後，點擊 **保存**。
