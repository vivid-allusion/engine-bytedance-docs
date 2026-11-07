---
title: "Headers"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Headers-cn-zh-tw"
---

對 HTTP 請求和回應標頭執行檢索、設定、新增和刪除等操作。參見 MDN 文件 [Headers](https://developer.mozilla.org/zh-CN/docs/Web/API/Headers)。

<span id="header-黑名單"></span>
## Header 黑名單

邊緣函數的執行階段預設將以下 Header 設為黑名單。若您的函數試圖讀寫黑名單中的 Header，將導致執行階段錯誤，並可能被判定有攻擊傾向，造成執行時期被暫時封禁。


* Expect

* Te

* Trailer

* Upgrade

* Proxy\-Connection

* Connection

* Host

* Keep\-Alive

* DNT

* 以 X\-Sparrow\- 為前綴的 Header

* 其他特殊內部 Header
