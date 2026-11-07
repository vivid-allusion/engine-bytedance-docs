---
title: "Request"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Request"
---

Represents a resource request. For detailed definitions and usage, refer to the MDN documentation [Request](https://developer.mozilla.org/en-US/docs/Web/API/Request).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The runtime of Edge Functions does not support the following properties of the Request interface:</div>



* <div data-tips="true" data-tips-type="tip">context</div>


* <div data-tips="true" data-tips-type="tip">credentials</div>


* <div data-tips="true" data-tips-type="tip">destination</div>


* <div data-tips="true" data-tips-type="tip">integrity</div>


* <div data-tips="true" data-tips-type="tip">mode</div>


* <div data-tips="true" data-tips-type="tip">referrer</div>


* <div data-tips="true" data-tips-type="tip">referrerPolicy</div>


* <div data-tips="true" data-tips-type="tip">cache</div>



<span id="usage"></span>
## Usage

<span id="standard-properties-and-methods-of-the-request-interface"></span>
### Standard properties and methods of the Request interface

The Request interface supports the following standard properties and methods.

<span id="properties"></span>
#### Properties

All of the following properties are read\-only.


* Get the request method: `request.method`.

* Get the request URL: `request.url`.

* Get the request headers: `request.headers`.

* Get the request payload: `request.body`, body is a ReadableStream object.


<span id="methods"></span>
#### Methods


* Get JSON: `await request.json()`.

* Get form data: `await request.formData()`.

* Get UTF8 string: `await request.text()`.


<span id="non-standard-properties-unique-to-edge-functions-runtime"></span>
### Non\-standard properties unique to Edge Functions runtime

In addition to the standard properties of the Request interface, the Edge Functions runtime also adds the following non\-standard properties:

All of the following properties are read\-only.


* Get the host request header: `request.host`.

* Get the request domain name: `request.hostname`.

* Get the request path: `request.path`.

* Get the parameters of the request URL: `request.query`.


<span id="how-the-content-length-header-affects-the-payload-transmission"></span>
### How the Content\-Length Header affects the payload transmission

The `Content-Length` header in a `Request` object and a `Response` object affects how the payload is transmitted:


* If the `Request` object or `Response` object contains a `Content-Length` header:

   * If the value of the `Content-Length` header is a number greater than or equal to 0: The runtime will adhere to the `Content-Length` header and only transmit the number of bytes of the payload specified by the `Content-Length` header. The rest of the payload will be discarded.

   * If the value of the `Content-Length` header is invalid: The runtime will ignore the `Content-Length` header and transmit the payload using chunked transfer encoding.

* If the `Request` object or `Response` object does not contain a `Content-Length` header, the runtime will transmit the payload using chunked transfer encoding.
