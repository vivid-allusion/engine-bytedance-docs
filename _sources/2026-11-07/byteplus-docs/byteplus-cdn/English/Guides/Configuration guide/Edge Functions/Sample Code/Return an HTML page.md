---
title: "Return an HTML page"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Return-an-HTML-page"
---

This example demonstrates how to generate an HTML page containing both static and dynamic content, and return it as a response to the client.

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


<span id="related-runtime-apis"></span>
## Related runtime APIs


* [addEventListener()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-addEventListener)

* [FetchEvent](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-FetchEvent)

* [Response](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Response)
