---
title: "URLのリダイレクト"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Redirect-jp"
---

この例は、ユーザーからのリクエストを指定されたURLにリダイレクトする方法を示しています。

```JavaScript
addEventListener("fetch", async event => {
  event.respondWith(handleRequest(event.request))
})

// Define the URL you want to redirect requests to
const destinationURL = "https://www.example.com/"
// Status code 301 indicates a permanent redirect
const statusCode = 301

// Define an asynchronous function to handle requests and redirect to the specified URL
async function handleRequest(request) {
  return Response.redirect(destinationURL, statusCode)
}
```


<span id="関連するランタイムapi"></span>
## 関連するランタイムAPI


* [addEventListener()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-addEventListener-jp)

* [FetchEvent](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-FetchEvent-jp)

* [Response](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Response-jp)
