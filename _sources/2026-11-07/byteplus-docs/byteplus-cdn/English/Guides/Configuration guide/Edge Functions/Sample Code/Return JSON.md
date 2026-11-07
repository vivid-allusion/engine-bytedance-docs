---
title: "Return JSON"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Return-JSON"
---

This example demonstrates how to generate data in JSON format and return it as a response to the client.

```JavaScript
addEventListener("fetch", event => {
  return event.respondWith(handleRequest(event));
})

async function handleRequest(event) {
  // Create data containing {hello: "world"}
  const data = {
    hello: "world"
  }
  // Convert the data to JSON format
  const json = JSON.stringify(data);
  // Return a response containing JSON data and set Content-Type to "application/json;charset=UTF-8"
  return new Response(json, {
      headers: {
        "content-type": "application/json;charset=UTF-8"
      }
    })
}
```


<span id="related-runtime-apis"></span>
## Related runtime APIs


* [addEventListener()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-addEventListener)

* [FetchEvent](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-FetchEvent)

* [Response](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Response)
