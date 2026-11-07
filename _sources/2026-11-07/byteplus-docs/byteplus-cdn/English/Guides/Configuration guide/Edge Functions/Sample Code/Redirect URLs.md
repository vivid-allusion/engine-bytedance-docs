---
title: "Redirect URLs"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Redirect"
---

This example demonstrates how to redirect user requests to a specified URL.

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


<span id="related-runtime-apis"></span>
## Related runtime APIs


* [addEventListener()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-addEventListener)

* [FetchEvent](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-FetchEvent)

* [Response](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Response)
