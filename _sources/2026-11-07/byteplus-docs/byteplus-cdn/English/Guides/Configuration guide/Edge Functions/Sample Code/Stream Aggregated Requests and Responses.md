---
title: "Stream Aggregated Requests and Responses"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Aggregate-requests"
---

This example demonstrates how to aggregate multiple different requests into a single streaming request, and how to aggregate the responses from these requests into a single streaming response to be returned to the user.

```JavaScript
addEventListener('fetch', (event) => {
  event.respondWith(handle(event));
});

async function aggRequest(urlBase, urlQuery, writable) {
  const path_list = urlQuery.split(',');
  let preventClose = true;
  const size = path_list.length;
  let idx = 0;

  for (const p of path_list) {
    const u = urlBase + p;
    const req = await fetch(urlBase + p);
    if (idx === (size - 1)) preventClose = false;

    // Start to pipe the data into the corresponding writable, so that the readable can read the data.
    await req.body.pipeTo(writable, {preventClose});

    // Write footer to help identify different responses.
    if (preventClose) {
      const writer = writable.getWriter();
      await writer.write(
    `\n\n\n\n`);
      writer.releaseLock();
    }
    ++idx;
  }
}

async function handle(event) {
  const url = new URL(event.request.url);
  const {readable, writable} = new TransformStream();

  await aggRequest(
      url.protocol + '//' + url.hostname + '/', url.search.substring(1),
      writable);
      
  return readable;
}

```


<span id="related-runtime-apis"></span>
## Related runtime APIs


* [addEventListener()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-addEventListener)

* [FetchEvent](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-FetchEvent)

* [Response](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Response)

* [fetch()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-fetch)

* [Streams](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Streams)
