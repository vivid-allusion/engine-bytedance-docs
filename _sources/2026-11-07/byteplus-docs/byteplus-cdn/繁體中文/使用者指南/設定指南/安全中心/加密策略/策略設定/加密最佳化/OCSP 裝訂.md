---
title: "OCSP 裝訂"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/ocsp-staping_zh-tw"
---

本文件介紹 BytePlus CDN 提供的 "OCSP 裝訂" 功能。

<span id="什麼是-ocsp-裝訂"></span>
## 什麼是 OCSP 裝訂

OCSP 是線上憑證狀態協定，英文全稱是 Online Certificate Status Protocol。在 TLS 握手階段，用戶端獲取憑證後會向該憑證的 CA 機構查詢該憑證的狀態。CA 機構會向用戶端發送 OCSP 響應。

由於用戶端在獲得憑證時就會向 CA 機構查詢憑證的狀態，容易造成 CA 機構收到大量的查詢請求。如果 CA 機構響應慢，會增加 TLS 握手的時間。為了避免這個問題，OCSP 裝訂就產生了。OCSP 裝訂允許伺服器定期向 CA 機構查詢憑證狀態並在伺服器快取該狀態。當伺服器向用戶端發送憑證時，會一起發送該憑證的 OCSP 響應。OCSP 響應是經過 CA 機構簽名的，不易被偽造。

<span id="ocsp-裝訂的優缺點"></span>
## OCSP 裝訂的優缺點

OCSP 裝訂極大降低了用戶端向 CA 機構發送的查詢請求，也降低了 TLS 的握手時間。缺點就是用戶端獲取到的憑證狀態不一定是最新的。但是可以通過配置伺服器向 CA 機構查詢憑證的時間間隔來降低該缺點帶來的影響。

<span id="啟用-ocsp-裝訂"></span>
## 啟用 OCSP 裝訂

BytePlus CDN 提供 "OCSP 裝訂" 功能，可以提高 TLS 握手效率，提升用戶體驗。

<span id="前提條件"></span>
### 前提條件

要開啟該配置，網域名稱必須已經開啟了 HTTPS 加密服務。

<span id="操作步驟"></span>
## 操作步驟


1. 打開 **OCSP 裝訂** 設定頁面。操作步驟參見 [網域名稱設定](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_zh-tw)。

2. 在 **OCSP 裝訂** 下方，設置 **狀態** 為 **開啟**。

3. 配置完成後，點擊 **保存**。
