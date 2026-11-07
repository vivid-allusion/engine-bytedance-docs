---
title: "Response"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Response-cn-zh-tw"
---

代表對請求的回應。參見 MDN 文件 [Response](https://developer.mozilla.org/zh-CN/docs/Web/API/Response)。

<span id="用法"></span>
## 用法

<span id="response-介面支援的方法"></span>
### Response 介面支援的方法

Response 介面支援以下方法：


* 建立 `Response` 物件的副本：`Response.clone()`

* 使用其他 URL 建立新回應：`Response.redirect(url,status)`


<span id="content-length-標頭如何影響承載傳輸"></span>
### Content\-Length 標頭如何影響承載傳輸

`Request` 對象和 `Response` 對象中的 `Content-Length` 標頭會影響承載的傳輸方式：


* 如果`Request` 對象或`Response` 對象包含 `Content-Length` 標頭：

   * 如果 `Content-Length` 標頭的值是等於或大於 0 的數字：執行時期將遵循 `Content-Length` 標頭，並且只傳輸 `Content-Length` 標頭指定的承載位元組數。承載的其餘部分將被捨棄。

   * 如果 `Content-Length` 標頭的值無效：執行時期將忽略 `Content-Length` 標頭，並使用分塊傳輸編碼來傳輸承載。

* 如果`Request` 對象或`Response` 對象不包含 `Content-Length` 標頭，執行時期將使用分塊傳輸編碼來傳輸承載。
