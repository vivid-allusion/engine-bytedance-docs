---
title: "什么是 Web Crypto Streams API"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/WebCryptoStream-cn"
---

[Web Crypto API](https://docs.byteplus.com/docs/byteplus-cdn/web-crypto-overview-cn) 在处理数据时，需要先把数据加载到内存。但是，边缘函数限制了每个函数可使用的内存大小。参见 [使用限制](https://docs.byteplus.com/docs/byteplus-cdn/functions-usage-limits)。如果需要被处理的数据大小超出了内存限制，就无法被加载到内存。

为了解决这个问题，边缘函数运行时提供了 Web Crypto Streams API。Web Crypto Streams API 是对 Web Crypto API 的扩展，能处理数据流。您把较大的数据转换为数据流后，就可以避免因内存大小限制造成数据无法被加载到内存的问题。

Web Crypto Streams API 支持以下 API：


* [DigestStream](https://docs.byteplus.com/docs/byteplus-cdn/DigestStream-cn)
