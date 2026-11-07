---
title: "返回HTML页面"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Return-an-HTML-page-cn"
---

该示例展示了如何生成一个包含静态内容和动态内容的 HTML 页面，并将该页面作为响应返回给客户端。

```JavaScript
addEventListener("fetch", event => {
  return event.respondWith(handleRequest(event));
})

async function handleRequest(event) {
  // 获取发送请求的用户的IP地址，如果不可用则默认为"N/A"
  const clientIp = event.info ? event.info.clientIp : "N/A";
  // 获取请求内容
  const request = event.request;
  // 创建 HTML 内容，包含欢迎信息和用户IP地址
  const html = `<!DOCTYPE html>
    <body>
      <h1>Hello World</h1>
      <p>Hello from Sparrow Runtime.</p>
      <p>The visitor's ip is ${clientIp}</p>
    </body>`;
  // 创建并返回一个新的响应，内容为上述 HTML，内容类型为 "text/html; charset=UTF-8"
  return new Response(html, {
    headers: {
      "Content-Type": "text/html; charset=UTF-8",
    },
  });
}
```


<span id="相关运行时-api"></span>
## 相关运行时 API


* [addEventListener() 方法](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-addEventListener-cn)

* [FetchEvent 接口](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-FetchEvent-cn)

* [Response 接口](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Response-cn)
