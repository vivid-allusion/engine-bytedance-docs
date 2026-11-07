---
title: "修改HTTP请求头或响应头"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Reverse-proxy-cn"
---

该示例展示了如何修改用户请求中的 HTTP 请求头和返回给用户的响应中的响应头。

```JavaScript
addEventListener("fetch", (event) => {
  event.respondWith(handle(event));
});

// 定义一个异步函数，处理fetch请求并添加自定义请求头信息
async function handle(event) {
  // 获取客户端传入的请求
  const request = event.request;

  // 在请求头中添加一个自定义请求头"x-via-sparrow-start"，值为当前时间戳
  request.headers.append("x-via-sparrow-start", `${Date.now()}`);

  // fetch 反向代理，发送请求并等待响应。
  const response = await fetch(request);

  // 在响应头中添加一个自定义响应头"x-via-sparrow-done"，值为当前时间戳
  response.headers.append("x-via-sparrow-done", `${Date.now()}`);
  
  // 将处理后的响应对象返回给客户端
  return response;
}
```


<span id="相关运行时-api"></span>
## 相关运行时 API


* [addEventListener() 方法](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-addEventListener-cn)

* [FetchEvent 接口](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-FetchEvent-cn)

* [Headers 接口](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Headers-cn)

* [Response 接口](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Response-cn)

* [fetch() 方法](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-fetch-cn)
