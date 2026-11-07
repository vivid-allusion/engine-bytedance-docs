---
title: "Redirect HTTP Requests to HTTPS Requests"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/Redirect_HTTP_Requests_to_HTTPS_Requests"
---

This example demonstrates how to redirect user requests from the HTTP protocol to the HTTPS protocol.

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


<span id="related-runtime-apis"></span>
## Related runtime APIs


* [addEventListener()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-addEventListener)

* [FetchEvent](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-FetchEvent)

* [Response](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Response)

* [fetch()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-fetch)
