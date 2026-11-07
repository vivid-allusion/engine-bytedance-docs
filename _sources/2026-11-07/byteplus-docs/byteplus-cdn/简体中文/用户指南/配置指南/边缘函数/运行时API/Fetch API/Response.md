---
title: "Response"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Response-cn"
---

表示对请求的响应。参见 MDN 文档 [Response](https://developer.mozilla.org/zh-CN/docs/Web/API/Response)。

<span id="用法"></span>
## 用法

<span id="response-接口支持的方法"></span>
### Response 接口支持的方法

Response 接口支持以下方法。


* 创建一个 `Response` 对象的副本：`Response.clone()`。

* 使用其他 URL 创建新的响应：`Response.redirect(url,status)`。


<span id="content-length-头如何影响-payload-的传输方式"></span>
### Content\-Length 头如何影响 payload 的传输方式

`Request` 对象和 `Response` 对象中的 `Content-Length` 头会影响 payload 的传输方式：


* 如果 `Request` 对象或 `Response` 对象包含 `Content-Length` 头：

   * 如果 `Content-Length` 头的值是一个数字且大于或等于 0：运行时会根据 `Content-Length` 头的值，仅传输其指定的字节数的 payload。payload 的剩余部分会被丢弃。

   * 如果 `Content-Length` 头的值无效：运行时会忽略该 `Content-Length` 头，并使用分块传输编码（chunked transfer encoding）的方式传输 payload。

* 如果 `Request` 对象或 `Response` 对象不包含 `Content-Length` 头，运行时会使用分块传输编码的方式传输 payload。
