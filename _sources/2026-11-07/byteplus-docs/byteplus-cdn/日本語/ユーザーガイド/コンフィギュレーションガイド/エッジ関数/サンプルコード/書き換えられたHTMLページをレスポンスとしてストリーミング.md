---
title: "書き換えられたHTMLページをレスポンスとしてストリーミング"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Modify-the-footer-header-jp"
---

この例は、取得したHTMLページを書き込み可能なストリームに書き込み、書き込み可能なストリーム内のHTMLページを修正し、その後、修正されたHTMLページをクライアントにレスポンスとしてストリーミングする方法を示しています。

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


<span id="関連するランタイムapi"></span>
## 関連するランタイムAPI


* [addEventListener()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-addEventListener-jp)

* [FetchEvent](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-FetchEvent-jp)

* [fetch()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-fetch-jp)

* [Streams](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Streams-jp)
