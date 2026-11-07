---
title: "返回HTML頁面"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Return-an-HTML-page-cn-zh-tw"
---

本示例展示如何生成包含靜態內容和動態內容的 HTML 頁面，並將該頁面作為響應返回給用戶端。

```JavaScript
addEventListener("fetch", event => {
  return event.respondWith(handleRequest(event));
})

async function handleRequest(event) {
  // 取得發送請求的使用者IP位址，若不可用則預設為"N/A"
  const clientIp = event.info ? event.info.clientIp : "N/A";
  // 取得請求內容
  const request = event.request;
  // 建立HTML內容，包含歡迎資訊和使用者IP位址
  const html = `<!DOCTYPE html>
    <body>
      <h1>Hello World</h1>
      <p>Hello from Sparrow Runtime.</p>
      <p>The visitor's ip is ${clientIp}</p>
    </body>`;
  // 建立並返回新響應，內容類型設定為 "text/html; charset=UTF-8"
  return new Response(html, {
    headers: {
      "Content-Type": "text/html; charset=UTF-8",
    },
  });
}
```


<span id="相關執行時-api"></span>
## 相關執行時 API


* [addEventListener() 方法](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-addEventListener-cn-zh-tw)

* [FetchEvent 介面](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-FetchEvent-cn-zh-tw)

* [Response 介面](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Response-cn-zh-tw)
