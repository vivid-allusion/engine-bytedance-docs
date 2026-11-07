---
title: "HTMLページを返す"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/return-an-html-page-jp"
---

この例は、静的コンテンツと動的コンテンツの両方を含むHTMLページを生成し、それをユーザーへのレスポンスとして返す方法を示しています。

```JavaScript
addEventListener("fetch", event => {
  return event.respondWith(handleRequest(event));
})

async function handleRequest(event) {
  // Get the IP address of the user sending the request, default to "N/A" if unavailable
  const clientIp = event.info ? event.info.clientIp : "N/A";
  // Get the request content
  const request = event.request;
  // Create HTML content, including a welcome message and the user's IP address
  const html = `<!DOCTYPE html>
    <body>
      <h1>Hello World</h1>
      <p>Hello from Sparrow Runtime.</p>
      <p>The visitor's ip is ${clientIp}</p>
    </body>`;
  // Create and return a new response with the above HTML content and content type "text/html; charset=UTF-8"
  return new Response(html, {
    headers: {
      "Content-Type": "text/html; charset=UTF-8",
    },
  });
}
```


<span id="関連するランタイムapi"></span>
## 関連するランタイムAPI


* [addEventListener()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-addEventListener-jp)

* [FetchEvent](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-FetchEvent-jp)

* [Response](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Response-jp)
