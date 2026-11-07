---
title: "JSONを返す"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/return-json-jp"
---

この例は、JSONフォーマットでデータを生成し、ユーザーへのレスポンスとして返す方法を示しています。

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


<span id="関連するランタイムapi"></span>
## 関連するランタイムAPI


* [addEventListener()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-addEventListener-jp)

* [FetchEvent](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-FetchEvent-jp)

* [Response](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Response-jp)
