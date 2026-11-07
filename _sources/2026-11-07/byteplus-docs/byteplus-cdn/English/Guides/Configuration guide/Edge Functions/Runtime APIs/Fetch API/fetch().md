---
title: "fetch()"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-fetch"
---

Sends an HTTP or HTTPS request. See the MDN documentation for [fetch()](https://developer.mozilla.org/docs/Web/API/WindowOrWorkerGlobalScope/fetch).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If your function calls <code>fetch()</code> to get an HTTP response and modifies the HTML Body (for example, using <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/function-createHtmlStream">createHtmlStream()</a> to stream\-modify the HTML Body), it is recommended that you delete the <code>Content-Length</code> header from the original HTTP response. Otherwise, it may cause data transmission errors. This is because the HTTP response may contain a <code>Content-Length</code> header. If the runtime forwards the original response's <code>Content-Length</code> header while the function modifies the HTTP response's HTML Body, the actual size of the payload will differ from the value of the <code>Content-Length</code> header. See <a href="https://docs.byteplus.com/en/docs/18/17405#payload">How the Content\-Length Header affects the payload transmission</a> for more information.</div>


<span id="usage-limits"></span>
## Usage limits


* The `fetch()` method sends requests using the default ports. The default port for HTTP requests is 80, and the default port for HTTPS requests is 443.

* IP addresses are not allowed in the request address.

* The scheme cannot be omitted from the request address. For example, `fetch("www.example.com")` is incorrect. You need to change it to `fetch("https://www.example.com")`.


<span id="usage"></span>
## Usage

<span id="accessing-byteplus-cdn-domains"></span>
### Accessing BytePlus CDN domains

By default, `fetch()` sends requests over the internet. If the domain accessed by the `fetch()` method is a BytePlus CDN domain, it is recommended to configure the `fetch()` method to send requests internally within the edge node by using the `{proxy: "cdn"}` parameter. Since Edge Functions and BytePlus CDN share edge nodes, requests sent by the function will be directly forwarded to BytePlus CDN within the edge node.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">A BytePlus CDN domain is any domain name that is served by BytePlus CDN. The domain's status in BytePlus CDN must be <strong>Enabled</strong>.</div>


For example, you can use the following methods to request the BytePlus CDN domain `cdn.example.com` and the third\-party API service domain `api.example.com`:

```js
// Request the BytePlus CDN domain cdn.example.com
const responseCDN = await fetch("https://cdn.example.com", { proxy: "cdn" });

// Request the third-party API service domain api.example.com
const responseAPI = await fetch("https://api.example.com");
```


The following diagram shows the difference in request paths when the `{proxy: "cdn"}` parameter is passed and when it is not:

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_e0b83d3c4f38d9c7c09b64a8673fea6d.png) </span>

The following table compares the differences between passing and not passing the `{proxy: "cdn"}` parameter:


|Difference |With `{proxy: "cdn"}` |Without `{proxy: "cdn"}` (Default) |
|---|---|---|
|**Request path** |Requests sent by the function are directly forwarded to BytePlus CDN within the edge node. |Requests sent by the function are routed to an edge node via the internet through DNS resolution. This edge node is not necessarily the same one where the function is executed. |
|**Cost** |No traffic costs are incurred on the BytePlus CDN side. |If the requested domain is a BytePlus CDN domain, requests via the internet will incur traffic costs on the BytePlus CDN side. |
|**Applicable scenarios** |Only applicable for accessing BytePlus CDN domains. If the requested domain is not a BytePlus CDN domain, the request will fail. The function will return a 403 error code. |Applicable for accessing any domain that can be accessed via the internet, except for BytePlus CDN domains. If the requested domain is a BytePlus CDN domain, the request may be subject to the domain's access control (such as IP blocklists/allowlists, geographic restrictions, etc.). |


<span id="following-3xx-redirects"></span>
### Following 3xx redirects

You can configure how the `fetch()` method handles 3xx redirects using the `redirect` parameter.


* `{redirect: "manual"}` (default): Does not automatically follow 3xx redirects. You can handle redirects manually.

* `{redirect: "follow"}`: Automatically follows 3xx redirects. For the same request, the `fetch()` method will follow up to 4 redirects by default and allows cross\-domain and cross\-protocol redirects.

* `{redirect: "error"}`: Throws an error when a 3xx redirect is encountered.


The following example shows how to automatically follow 3xx redirects:

```js
const response = await fetch("https://www.example.com", {redirect: "follow"});
```


The redirect behavior of `fetch()` for different status codes is as follows:


|**Status Code** |**Redirect Behavior** |
|---|---|
|301, 302, 303, 308 |The request method of the redirected request is changed to GET. The request body is ignored. |
|307 |Only follows GET methods. For requests initiated with other HTTP methods, this method will not automatically follow the redirect and will throw an error. |


The redirect address is obtained from the `Location` response header. The `Location` response header currently accepts a comma\-separated list, but only the first URL will be followed, and the others will be ignored.

<span id="decompressing-response-data"></span>
### Decompressing response data

The `fetch()` method currently only supports decompressing response data in **gzip** format. You can use the `decompression` parameter to configure whether the `fetch()` method decompresses the response data:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The <code>fetch()</code> method identifies the compression format through the <code>Content-Encoding</code> header in the response. For example:</div>



* <div data-tips="true" data-tips-type="tip">If <code>Content-Encoding</code> is <code>gzip</code> or <code>gzip, identity</code>, the response will be identified as gzip compressed.</div>


* <div data-tips="true" data-tips-type="tip">If <code>Content-Encoding</code> is <code>brotli, gzip</code>, the <code>fetch()</code> method will only decompress the outermost gzip compression.</div>


* `manual`: **Does not decompress**. Returns the original response data directly.

* `fallbackIdentity`: (Default) **Decompresses automatically**. For unsupported compression formats, the original data will be returned.

* `decompress`: **Decompresses automatically**. For unsupported compression formats, an error will be thrown.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After decompression, the <code>Content-Length</code> response header will no longer accurately reflect the data size. To prevent data transmission errors, the runtime will delete this response header and add the <code>X-Content-Length-Before-Decompression</code> response header to record the original data size.</div>


The following example demonstrates how to set the `fetch()` method to automatically decompress the response data and return the original data for unsupported compression formats.

```js
const response = await fetch("https://www.example.com", {decompression: "fallbackIdentity"});
```


<span id="supported-compression-formats"></span>
#### Supported compression formats

`fetch()` currently only supports decompressing the **gzip** format. It identifies the compression format through the `Content-Encoding` header in the response.


* If `Content-Encoding` is `gzip` or `gzip, identity`, the response is identified as gzip compressed.

* If `Content-Encoding` is `brotli, gzip`, `fetch()` will only decompress the outermost gzip compression.


<span id="handling-of-the-content-encoding-header-after-decompression"></span>
#### Handling of the `Content-Encoding` Header after decompression

After decompression, `fetch()` modifies the `Content-Encoding` response header accordingly:


* `Content-Encoding: identity, gzip` will be changed to `Content-Encoding: identity`.

* `Content-Encoding: gzip` will be removed.

* `Content-Encoding: gzip, identity` will be removed.

* `Content-Encoding: brotli, gzip` will be changed to `Content-Encoding:brotli`。


<span id="additional-information"></span>
## Additional information

&nbsp;

<span id="how-the-content-length-header-affects-the-payload-transmission"></span>
### How the Content\-Length Header affects the payload transmission

The `Content-Length` header in a `Request` object and a `Response` object affects how the payload is transmitted:


* If the `Request` object or `Response` object contains a `Content-Length` header:

   * If the value of the `Content-Length` header is a number greater than or equal to 0: The runtime will adhere to the `Content-Length` header and only transmit the number of bytes of the payload specified by the `Content-Length` header. The rest of the payload will be discarded.

   * If the value of the `Content-Length` header is invalid: The runtime will ignore the `Content-Length` header and transmit the payload using chunked transfer encoding.

* If the `Request` object or `Response` object does not contain a `Content-Length` header, the runtime will transmit the payload using chunked transfer encoding.
