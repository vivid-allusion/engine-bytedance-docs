---
title: "Headers"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Headers-cn"
---

对 HTTP 请求和响应头执行检索、设置、添加和删除等操作。参见 MDN 文档 [Headers](https://developer.mozilla.org/zh-CN/docs/Web/API/Headers)。

<span id="header-黑名单"></span>
## Header 黑名单

边缘函数的运行时默认将以下 Header 设置为黑名单。如果您的函数试图读写黑名单的 Header，会造成运行时错误，并可能被认为有攻击倾向，造成运行时被短暂封禁。


* Expect

* Te

* Trailer

* Upgrade

* Proxy\-Connection

* Connection

* Host

* Keep\-Alive

* DNT

* 以 X\-Sparrow\- 为前缀的 Header

* 其他特殊内部 Header
