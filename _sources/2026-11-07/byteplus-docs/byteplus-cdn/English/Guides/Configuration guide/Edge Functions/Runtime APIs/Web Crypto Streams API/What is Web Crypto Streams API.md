---
title: "What is Web Crypto Streams API"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/WebCryptoStream-en"
---

When [Web Crypto API](https://docs.byteplus.com/docs/byteplus-cdn/web-crypto-overview-en) processes data, it needs to load the data into memory first. However, BytePlus edge functions limit the memory size available for each function. See [Usage Limits](https://docs.byteplus.com/docs/byteplus-cdn/Usage_Limits_Functions). If the data to be processed exceeds the memory limit, it cannot be loaded into memory.

To solve this problem, the edge functions runtime provides the Web Crypto Streams API. The Web Crypto Streams API is an extension of the Web Crypto API and can process data streams. By converting large data into data streams, you can avoid memory loading failures caused by memory size limitations.

The Web Crypto Streams API supports the following APIs:


* [DigestStream](https://docs.byteplus.com/docs/byteplus-cdn/DigestStream-en)
