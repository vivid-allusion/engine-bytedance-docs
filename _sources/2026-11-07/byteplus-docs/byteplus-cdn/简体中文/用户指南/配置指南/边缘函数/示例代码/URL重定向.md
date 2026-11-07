---
title: "URL重定向"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Redirect-cn"
---

该示例展示了如何将用户请求重定向到指定的 URL 。

```JavaScript
addEventListener("fetch", async event => {
  event.respondWith(handleRequest(event.request))
})

//定义您希望将请求重定向到的URL
const destinationURL = "https://www.example.com/"
//状态码301表示永久重定向
const statusCode = 301

//定义一个异步函数，用于处理请求并重定向至指定URL。
async function handleRequest(request) {
  return Response.redirect(destinationURL, statusCode)
}

```


<span id="相关运行时-api"></span>
## 相关运行时 API


* [addEventListener() 方法](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-addEventListener-cn)

* [FetchEvent 接口](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-FetchEvent-cn)

* [Response 接口](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Response-cn)
