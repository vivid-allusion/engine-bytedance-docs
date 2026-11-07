---
title: "HTTP/2"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/HTTP2_zh-tw"
---

本文件介紹 BytePlus CDN 中對 HTTP/2 協定的支援。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">由於協定的機制不同，HTTP/2 與 Websocket 無法同時啟用。</div>


<span id="前提條件"></span>
## 前提條件

要啟用該設定，您的網域名稱必須已經啟用了 HTTPS 加密服務。

<span id="什麼是-http-2"></span>
## 什麼是 HTTP/2

HTTP/2 擴展了 HTTP/1.x 的功能。相容 HTTP/1.x，同時增加了二進制分幀層、標頭壓縮、多路複用、伺服器端推送等功能。

HTTP/2 不強制要求網站啟用 HTTPS。但是主流瀏覽器對 HTTP/2 的支援都是基於 SSL/TLS 實現的。目前使用 HTTP/2 的網站都是啟用 HTTPS 的。

<span id="操作步驟"></span>
## 操作步驟


1. 打開 **HTTP/2** 設定頁面。操作步驟參見 [網域名稱設定](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_zh-tw)。

2. 在 **HTTP/2** 下方，設置 **狀態** 為 **開啟**。

3. 配置完成後，點擊 **儲存**。


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_f4718edb459c53de8dc7fa03211daacb.png) </span>
