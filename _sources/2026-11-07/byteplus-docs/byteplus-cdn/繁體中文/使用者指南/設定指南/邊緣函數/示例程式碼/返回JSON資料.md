---
title: "返回JSON資料"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Return-JSON-cn-zh-tw"
---

本示例展示如何產生 JSON 格式的資料，並將該資料作為響應返回給用戶端。

```JavaScript
addEventListener("fetch", event => {
  return event.respondWith(handleRequest(event));
})

async function handleRequest(event) {
  // 建立包含{hello: "world"}的資料
  const data = {
    hello: "world"
  }
    // 將資料轉換為JSON格式
  const json = JSON.stringify(data);
  // 返回包含JSON資料的響應，並設定Content-Type為"application/json;charset=UTF-8"
  return new Response(json, {
      headers: {
        "content-type": "application/json;charset=UTF-8"
      }
    })

}
```


<span id="相關執行時-api"></span>
## 相關執行時 API


* [addEventListener() 方法](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-addEventListener-cn-zh-tw)

* [FetchEvent 介面](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-FetchEvent-cn-zh-tw)

* [Response 介面](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Response-cn-zh-tw)
