---
title: "返回JSON数据"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Return-JSON-cn"
---

该示例展示了如何生成 JSON 格式的数据，并将该数据并作为响应返回给客户端。

```JavaScript
addEventListener("fetch", event => {
  return event.respondWith(handleRequest(event));
})

async function handleRequest(event) {
  // 创建包含{hello: "world"}的数据
  const data = {
    hello: "world"
  }
    // 将数据转换为JSON格式
  const json = JSON.stringify(data);
  // 返回一个包含JSON数据的响应，并设置Content-Type为"application/json;charset=UTF-8"
  return new Response(json, {
      headers: {
        "content-type": "application/json;charset=UTF-8"
      }
    })

}
```


<span id="相关运行时-api"></span>
## 相关运行时 API


* [addEventListener() 方法](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-addEventListener-cn)

* [FetchEvent 接口](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-FetchEvent-cn)

* [Response 接口](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Response-cn)
