---
title: "HTTPからHTTPSへのリダイレクト"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/Redirect_HTTP_Requests_to_HTTPS_Requests-jp"
---

この例は、ユーザーからのリクエストをHTTPプロトコルからHTTPSプロトコルにリダイレクトする方法を示しています。

```JavaScript
addEventListener("fetch", (event) => {
  event.respondWith(upgradeToSSL(event));
});

// Define an asynchronous function to redirect HTTP to HTTPS
async function upgradeToSSL(event) {
  // Get the incoming request object
  const incomingRequest = event.request;
  // Parse the URL of the request
  const url = new URL(incomingRequest.url);

  // Check if the protocol used by the request is HTTP
  if (url.protocol == 'http:') {
    // If it's HTTP protocol, change the protocol to HTTPS
    url.protocol = 'https';
    // Send a new request to the HTTPS address, passing through all parts of the original request except for the protocol
    return fetch(url.toString(), {
      method: incomingRequest.method,
      headers: incomingRequest.headers,
      body: incomingRequest.body
    });
  } else {
    // If it's HTTPS protocol, send the original request directly
    return fetch(incomingRequest);
  }
} 
```


<span id="関連するランタイムapi"></span>
## 関連するランタイムAPI


* [addEventListener()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-addEventListener-jp)

* [FetchEvent](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-FetchEvent-jp)

* [Response](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Response-jp)

* [fetch()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-fetch-jp)
