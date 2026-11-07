---
title: "DigestStream"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DigestStream-en"
---

The DigestStream object is a [TransformStream](https://docs.byteplus.com/docs/byteplus-cdn/docs-Streams#transformstream) that generates digests for specified data streams.

<span id="constructor"></span>
## Constructor

```javascript
let {readable, writable} = new DigestStream(algorithm)
```


<span id="parameters"></span>
### Parameters


* `algorithm` *string/object* ：Digest algorithm. Accepts either a string or an object containing a name string property. Valid string values are:

   * `SHA-1`: SHA\-1 digest algorithm

   * `SHA-256`: SHA\-256 digest algorithm

   * `SHA-384`: SHA\-384 digest algorithm

   * `SHA-512`: SHA\-512 digest algorithm

   * `MD5`: MD5 digest algorithm


<span id="supported-algorithms"></span>
## Supported Algorithms

See [Supported Algorithms](https://docs.byteplus.com/docs/byteplus-cdn/supported-web-crypto-stream-algo-en).

<span id="example"></span>
## Example

You can refer to the sample code below to understand how to use DigestStream. The logic of the sample code is as follows:


1. Use the `fetch()` method to retrieve website content and obtain the response body as a `ReadableStream`. Simultaneously, use the `tee()` method to copy the obtained `ReadableStream`, returning an array containing two `ReadableStream` instances.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The <code>tee()</code> method is used to handle two different operations on the response body simultaneously: one for creating SHA\-256 digests and another for constructing new responses.   </div>
   

2. Create a `DigestStream` object with the digest algorithm set to SHA\-256.

3. Pipe one of the `ReadableStream` instances returned by `tee()` through the `DigestStream` using the `pipeThrough()` method. The `DigestStream` will generate a SHA\-256 digest for this `ReadableStream` and return the digest through the `readable` end.

4. Construct a new response using the other `ReadableStream` instance returned by `tee()`.

5. Convert the `readable` end of the `DigestStream` into Uint8Array data, then transform it into a hexadecimal string. This hexadecimal string is subsequently added to the new response's headers.


```JavaScript
addEventListener('fetch', (event) => {
  event.respondWith(handle(event));
});

async function handle(event) {
  const resp = await fetch('https://www.example.com');
    
  // we need to read the body twice
  const [bodyOne, bodyTwo] = resp.body.tee();

  // create a SHA-256 digest stream
  const digestStream = new DigestStream('SHA-256');
 
  // pipe the body to digest stream
  const readable = bodyTwo.pipeThrough(digestStream);

  // get the digest result
  const data = await flushStreamReader(readable.getReader());

  // turn it into a hex string and set it in response header
  const newResp = new Response(bodyOne);
  const hexString = [...new Uint8Array(data)].map((b) => b.toString(16).padStart(2, '0')).join('');
  newResp.headers.set('x-content-sha256', hexString);
  return newResp;
}

async function flushStreamReader(reader) {
  let buf = [];
  let sz = 0;

  while (true) {
    let { value, done } = await reader.read();
    if (done) {
      break;
    }
    sz += value.length;
    buf.push(value);
  }

  let result = new Uint8Array(sz);
  let idx = 0;

  for (const x of buf) {
    result.set(x, idx);
    idx += x.length;
  }

  return result;
}

```
