---
title: "Headers"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Headers"
---

Perform operations such as retrieval, setting, adding, and deleting on HTTP request and response headers. Refer to the MDN documentation [Headers](https://developer.mozilla.org/en-US/docs/Web/API/Headers).

<span id="header-blocklist"></span>
## Header blocklist

The runtime of Edge Functions sets the following Headers as blocklisted by default. If your function attempts to read or write blocklisted Headers, it will cause a runtime error and may be considered as having malicious intent, resulting in a temporary ban of the runtime.


* Expect

* Te

* Trailer

* Upgrade

* Proxy\-Connection

* Connection

* Host

* Keep\-Alive

* DNT

* Headers prefixed with X\-Sparrow\-

* Other special internal Headers
