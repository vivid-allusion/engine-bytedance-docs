---
title: "Retrieve and Process JSON"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-JSON-processing"
---

This example demonstrates how to retrieve and process JSON data.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This example does not show specific JSON data processing logic. You can add your own data processing logic in the <code>handleJSON()</code> method. For instance, Edge Functions can serve as a middleware layer (Backend\-for\-Frontend, BFF) to implement the following logic:</div>



* <div data-tips="true" data-tips-type="tip">Preprocess JSON data returned from the server for data extraction or cleansing.</div>


* <div data-tips="true" data-tips-type="tip">Set up a GraphQL server at edge nodes using a GraphQL library. Users can query JSON data using GraphQL language.</div>


* <div data-tips="true" data-tips-type="tip">Summarize and analyze JSON data returned from the server.</div>



```JavaScript
addEventListener('fetch', (event) => {
  event.respondWith(handle(event));
});

function handleJSON(json) {
  // Process your JSON data here
}

async function handle(event) {
  // Request a JSON API and parse it
  const req = await fetch("http://www.example.com/json");
  const json = await req.json();

  const data = handleJSON(json);
  // Return the processed data
  return data;
} 
```


<span id="related-runtime-apis"></span>
## Related runtime APIs


* [addEventListener()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-addEventListener)

* [FetchEvent](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-FetchEvent)

* [Response](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Response)

* [fetch()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-fetch)
