---
title: "Modify HTTP Request Headers or Response Headers"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Reverse-proxy"
---

This example demonstrates how to modify HTTP request headers in user requests and response headers in responses returned to users.

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


<span id="related-runtime-apis"></span>
## Related runtime APIs


* [addEventListener()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-addEventListener)

* [FetchEvent](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-FetchEvent)

* [Headers](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Headers)

* [Response](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Response)

* [fetch()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-fetch)
