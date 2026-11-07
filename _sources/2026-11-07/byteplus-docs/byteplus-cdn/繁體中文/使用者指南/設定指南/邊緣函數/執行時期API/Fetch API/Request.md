---
title: "Request"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Request-cn-zh-tw"
---

代表資源請求。詳細定義及用法參見 MDN 文件 [Request](https://developer.mozilla.org/zh-CN/docs/Web/API/Request)。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">邊緣函數的執行時期不支援 Request 介面的以下屬性：</div>



* <div data-tips="true" data-tips-type="tip">context</div>


* <div data-tips="true" data-tips-type="tip">credentials</div>


* <div data-tips="true" data-tips-type="tip">destination</div>


* <div data-tips="true" data-tips-type="tip">integrity</div>


* <div data-tips="true" data-tips-type="tip">mode</div>


* <div data-tips="true" data-tips-type="tip">referrer</div>


* <div data-tips="true" data-tips-type="tip">referrerPolicy</div>


* <div data-tips="true" data-tips-type="tip">cache</div>



<span id="用法"></span>
## 用法

<span id="request-介面的標準屬性和標準方法"></span>
### Request 介面的標準屬性和標準方法

Request 介面支援以下標準屬性和標準方法。

<span id="屬性"></span>
#### 屬性

下列屬性均為唯讀：


* 取得請求方法: `request.method`

* 取得請求網址: `request.url`

* 取得請求標頭: `request.headers`

* 取得請求負載: `request.body`，body 為 ReadableStream 物件


<span id="方法"></span>
#### 方法


* 取得 JSON: `await request.json()`

* 取得表單資料: `await request.formData()`

* 取得 UTF8 字串: `await request.text()`


<span id="邊緣函數執行時期中獨有的非標準屬性"></span>
### 邊緣函數執行時期中獨有的非標準屬性

在標準 Request 介面屬性之外，邊緣函數執行時期新增以下非標準屬性：

下列屬性均為唯讀：


* 取得請求的 host 請求標頭: `request.host`

* 取得請求的網域名稱: `request.hostname`

* 取得請求的路徑: `request.path`

* 取得請求網址的參數: `request.query`


<span id="content-length-標頭如何影響承載傳輸"></span>
### Content\-Length 標頭如何影響承載傳輸

`Request` 對象和 `Response` 對象中的 `Content-Length` 標頭會影響承載的傳輸方式：


* 如果`Request` 對象或`Response` 對象包含 `Content-Length` 標頭：

   * 如果 `Content-Length` 標頭的值是等於或大於 0 的數字：執行時期將遵循 `Content-Length` 標頭，並且只傳輸 `Content-Length` 標頭指定的承載位元組數。承載的其餘部分將被捨棄。

   * 如果 `Content-Length` 標頭的值無效：執行時期將忽略 `Content-Length` 標頭，並使用分塊傳輸編碼來傳輸承載。

* 如果`Request` 對象或`Response` 對象不包含 `Content-Length` 標頭，執行時期將使用分塊傳輸編碼來傳輸承載。
