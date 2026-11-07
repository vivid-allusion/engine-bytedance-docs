---
title: "将HTTP重定向到HTTPS"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/redirect-http-to-https"
---

该示例展示了如何将用户请求使用的 HTTP 协议重定向为 HTTPS 协议。

```JavaScript
addEventListener("fetch", (event) => {
  event.respondWith(upgradeToSSL(event));
});

//定义一个异步函数，将HTTP重定向为HTTPS
async function upgradeToSSL(event) {
  // 获取传入请求对象
  const incomingRequest = event.request;
  // 解析请求的URL
  const url = new URL(incomingRequest.url);

  // 检查请求所使用的协议是否为HTTP
  if (url.protocol == 'http:') {
    // 如果是HTTP协议，则将协议更改为HTTPS
    url.protocol = 'https';
    // 发送一个新的请求到HTTPS地址，原始请求中协议以外的其他部分正常透传
    return fetch(url.toString(), {
      method: incomingRequest.method,
      headers: incomingRequest.headers,
      body: incomingRequest.body
    });
  } else {
    // 如果是HTTPS协议，则直接发送原始请求。
    return fetch(incomingRequest);
  }
}
```


<span id="相关运行时-api"></span>
## 相关运行时 API


* [addEventListener() 方法](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-addEventListener-cn)

* [FetchEvent 接口](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-FetchEvent-cn)

* [Response 接口](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Response-cn)

* [fetch() 方法](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-fetch-cn)
