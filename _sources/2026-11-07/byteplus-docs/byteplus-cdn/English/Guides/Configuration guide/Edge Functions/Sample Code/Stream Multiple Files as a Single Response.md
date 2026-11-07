---
title: "Stream Multiple Files as a Single Response"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/Stream_Multiple_Files_as_a_Single_Response"
---

This example demonstrates how to request multiple files in a single request and return these files as a stream.

When a web page needs to load multiple static files without dependencies, the browser typically requests each file separately. However, browsers have a limit on the number of concurrent resource requests. To reduce the number of HTTP requests sent, you can combine the browser's static resource requests. This can be implemented by merging multiple file requests using URL query parameters.

For example, the value of the src attribute in a <script\> tag on a web page includes a query parameter named urllist. This query parameter contains the URL paths of multiple .js files.

```html
<script src="http://www.example.com/?urllist=/react/a.min.js,/react/b.min.js"></script>
```


When the function receives a user request, it first reads the query parameter to obtain the URL path of each .js file. It then concatenates these paths into complete URLs. The function then asynchronously requests and accesses each URL to retrieve the files. While retrieving the files, the function streams the obtained files back to the user.

```JavaScript
async function handle(event) {
  const request = event.request; 
  const url = new URL(request.url);
  const fetchList = url.searchParams.get("urllist").split(",");
  const {readable, writable} = new TransformStream();
  
  (async () => {
    let idx = 0;
    for (const u of fetchList) {
      const resp = await fetch (`http://${url.host}${u}`);
      const close = (idx == fetchList.length - 1);
      resp.body.pipeTo(writable, {preventClose: close});
      idx++;
    }
  })();
  
  return new Response(readable, {
    status: 200
  });
}

addEventListener('fetch', (event) => {
  event.respondWith(handle(event));
});
```


<span id="related-runtime-apis"></span>
## Related runtime APIs


* [addEventListener()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-addEventListener)

* [FetchEvent](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-FetchEvent)

* [fetch()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-fetch)

* [Streams](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Streams)
