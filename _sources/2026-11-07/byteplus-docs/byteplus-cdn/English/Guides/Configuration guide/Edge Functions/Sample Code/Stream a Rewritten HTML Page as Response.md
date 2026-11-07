---
title: "Stream a Rewritten HTML Page as Response"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Modify-the-footer-header"
---

This example demonstrates how to write the obtained HTML page into a writable stream, modify the HTML page in the writable stream, and then stream the modified HTML page back to the client as a response.

```JavaScript
addEventListener('fetch', (event) => {
  event.respondWith(handle(event));
});

async function handle(event) {

  // Create a readable and writable TransformStream object
  const {readable, writable} = new TransformStream();
  
  // Get the request of 'http://www.example.com'
  const request = await fetch('http://www.example.com');
  
  // Write the content to writable stream by adding a footer
  (async () => {
    await request.body.pipeTo(writable, {preventClose: true});
    {
      const writer = writable.getWriter();
      await writer.write('\n\n\n<!----------- This is a new footer---------->');
      await writer.close();
    }
  })();


  // Return the readable stream as response
  return new Response(readable);
}
```


<span id="related-runtime-apis"></span>
## Related runtime APIs


* [addEventListener()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-addEventListener)

* [FetchEvent](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-FetchEvent)

* [fetch()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-fetch)

* [Streams](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Streams)
