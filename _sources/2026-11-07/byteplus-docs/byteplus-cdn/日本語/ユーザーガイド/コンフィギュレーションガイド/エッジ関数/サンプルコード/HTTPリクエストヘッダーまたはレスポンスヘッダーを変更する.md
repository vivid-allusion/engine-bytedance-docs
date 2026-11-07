---
title: "HTTPリクエストヘッダーまたはレスポンスヘッダーを変更する"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Reverse-proxy-jp"
---

この例は、ユーザーからのリクエストのHTTPリクエストヘッダーとユーザーに返されるレスポンスのレスポンスヘッダーを変更する方法を示しています。

```JavaScript
addEventListener("fetch", (event) => {
  event.respondWith(handle(event));
});

// Define an asynchronous function to handle fetch requests and add custom request headers
async function handle(event) {
  // Get the request from the client
  const request = event.request;

  // Add a custom request header "x-via-sparrow-start" to the request headers, with the current timestamp as its value
  request.headers.append("x-via-sparrow-start", `${Date.now()}`);

  // Fetch reverse proxy, send the request and wait for the response
  const response = await fetch(request);

  // Add a custom response header "x-via-sparrow-done" to the response headers, with the current timestamp as its value
  response.headers.append("x-via-sparrow-done", `${Date.now()}`);
  
  // Return the processed response object to the client
  return response;
}
```


<span id="関連するランタイムapi"></span>
## 関連するランタイムAPI


* [addEventListener()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-addEventListener-jp)

* [FetchEvent](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-FetchEvent-jp)

* [Headers](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Headers-jp)

* [Response](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Response-jp)

* [fetch()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-fetch-jp)
