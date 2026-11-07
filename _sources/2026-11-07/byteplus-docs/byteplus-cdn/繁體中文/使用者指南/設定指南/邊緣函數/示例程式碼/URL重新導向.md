---
title: "URL重新導向"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Redirect-cn-zh-tw"
---

本示例展示如何將使用者請求重新導向至指定 URL

```JavaScript
addEventListener("fetch", async event => {
  event.respondWith(handleRequest(event.request))
})

// 定義您希望將請求重新導向到的URL
const destinationURL = "https://www.example.com/"
// 狀態碼301表示永久重新導向
const statusCode = 301

// 定義非同步函式用於處理請求並重新導向至指定URL
async function handleRequest(request) {
  return Response.redirect(destinationURL, statusCode)
}

```


<span id="相關執行時-api"></span>
## 相關執行時 API


* [addEventListener() 方法](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-addEventListener-cn-zh-tw)

* [FetchEvent 介面](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-FetchEvent-cn-zh-tw)

* [Response 介面](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Response-cn-zh-tw)
