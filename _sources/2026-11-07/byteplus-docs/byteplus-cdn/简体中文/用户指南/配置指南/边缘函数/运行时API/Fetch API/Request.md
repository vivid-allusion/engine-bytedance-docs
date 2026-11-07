---
title: "Request"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Request-cn"
---

表示资源请求。详细定义及用法参见 MDN 文档 [Request](https://developer.mozilla.org/zh-CN/docs/Web/API/Request)。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">边缘函数的运行时不支持 Request 接口的以下属性：</div>



* <div data-tips="true" data-tips-type="tip">context</div>


* <div data-tips="true" data-tips-type="tip">credentials</div>


* <div data-tips="true" data-tips-type="tip">destination</div>


* <div data-tips="true" data-tips-type="tip">integrity</div>


* <div data-tips="true" data-tips-type="tip">mode</div>


* <div data-tips="true" data-tips-type="tip">referrer</div>


* <div data-tips="true" data-tips-type="tip">referrerPolicy</div>


* <div data-tips="true" data-tips-type="tip">cache</div>



<span id="用法"></span>
## 用法

<span id="request-接口的标准属性和标准方法"></span>
### Request 接口的标准属性和标准方法

Request 接口支持以下标准属性和标准方法。

<span id="属性"></span>
#### 属性

下列属性都是只读的。


* 获得请求方法: `request.method`。

* 获得请求 url: `request.url`。

* 获得请求头：`request.headers`。

* 获得请求负载：`request.body`，body 是一个 ReadableStream 对象。


<span id="方法"></span>
#### 方法


* 获得 JSON：`await request.json()`。

* 获得表单数据：`await request.formData()`。

* 获得 UTF8 字符串：`await request.text()`。


<span id="边缘函数运行时中独有的非标准属性"></span>
### 边缘函数运行时中独有的非标准属性

在标准的 Request 接口的属性外，边缘函数运行时还添加了以下非标准属性：

下列属性都是只读的。


* 获得请求的 host 请求头：`request.host`。

* 获得请求的域名：`request.hostname`。

* 获得请求的路径：`request.path`。

* 获得请求 url 的参数:`request.query`。


<span id="content-length-头如何影响-payload-的传输方式"></span>
### Content\-Length 头如何影响 payload 的传输方式

`Request` 对象和 `Response` 对象中的 `Content-Length` 头会影响 payload 的传输方式：


* 如果 `Request` 对象或 `Response` 对象包含 `Content-Length` 头：

   * 如果 `Content-Length` 头的值是一个数字且大于或等于 0：运行时会根据 `Content-Length` 头的值，仅传输其指定的字节数的 payload。payload 的剩余部分会被丢弃。

   * 如果 `Content-Length` 头的值无效：运行时会忽略该 `Content-Length` 头，并使用分块传输编码（chunked transfer encoding）的方式传输 payload。

* 如果 `Request` 对象或 `Response` 对象不包含 `Content-Length` 头，运行时会使用分块传输编码的方式传输 payload。
