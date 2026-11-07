---
title: "Response"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Response"
---

Represents the response to a request. Refer to the MDN documentation [Response](https://developer.mozilla.org/en-US/docs/Web/API/Response).

<span id="usage"></span>
## Usage

<span id="methods-supported-by-the-response-interface"></span>
### Methods supported by the Response interface

The Response interface supports the following methods.


* Create a copy of a `Response` object: `Response.clone()`.

* Create a new response with a different URL: `Response.redirect(url, status)`.


<span id="how-the-content-length-header-affects-the-payload-transmission"></span>
### How the Content\-Length Header affects the payload transmission

The `Content-Length` header in a `Request` object and a `Response` object affects how the payload is transmitted:


* If the `Request` object or `Response` object contains a `Content-Length` header:

   * If the value of the `Content-Length` header is a number greater than or equal to 0: The runtime will adhere to the `Content-Length` header and only transmit the number of bytes of the payload specified by the `Content-Length` header. The rest of the payload will be discarded.

   * If the value of the `Content-Length` header is invalid: The runtime will ignore the `Content-Length` header and transmit the payload using chunked transfer encoding.

* If the `Request` object or `Response` object does not contain a `Content-Length` header, the runtime will transmit the payload using chunked transfer encoding.
