---
title: "流式返回改写的HTML页面"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Modify-the-footer-header-cn"
---

该示例展示了如何把获取的 HTML 页面写入可写流中，对可写流中的 HTML 页面进行改写，并将改写后的 HTML 页面作为响应流式返回给客户端。

```JavaScript
addEventListener('fetch', (event) => {
  event.respondWith(handle(event));
});

// 定义一个异步函数handle用于处理请求
async function handle(event) {

  // 创建一个可读写的TransformStream对象
  const {readable, writable} = new TransformStream();
  
  // 异步获取'http://www.example.com'的请求内容
  const request = await fetch('http://www.example.com');
  
  // 异步将请求内容写入可写流中，并在内容末尾添加一个注释作为页脚
  (async () => {
    await request.body.pipeTo(writable, {preventClose: true});
    {
      const writer = writable.getWriter();
      await writer.write('\n\n\n<!----------- 这就是footer哟！---------->');
      await writer.close();
    }
  })();


  // 将可读流作为Response对象的内容返回
  return new Response(readable);
}
```


<span id="相关运行时-api"></span>
## 相关运行时 API


* [addEventListener() 方法](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-addEventListener-cn)

* [FetchEvent 接口](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-FetchEvent-cn)

* [fetch() 方法](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-fetch-cn)

* [Streams 接口](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Streams-cn)
