---
title: "DigestStream"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DigestStream-cn"
---

DigestStream 对象是一个 [TransformStream](https://docs.byteplus.com/docs/byteplus-cdn/docs_cn-Streams-cn#transformstream) 对象，用于生成指定数据流的摘要。

<span id="构造函数"></span>
## 构造函数

```javascript
let {readable, writable} = new DigestStream(algorithm)
```


<span id="参数说明"></span>
### 参数说明


* `algorithm` *string/object*：摘要算法。您可以传入一个字符串或者一个包含 name 字符串属性的对象。您可以把字符串设置为以下值：

   * `SHA-1`：SHA\-1 摘要算法。

   * `SHA-256`：SHA\-256 摘要算法。

   * `SHA-384`：SHA\-384 摘要算法。

   * `SHA-512`：SHA\-512 摘要算法。

   * `MD5`：MD5 摘要算法。


<span id="支持的算法"></span>
## 支持的算法

参见 [支持的算法](https://docs.byteplus.com/docs/byteplus-cdn/supported-web-crypto-stream-algo-cn)。

<span id="示例"></span>
## 示例

您可以参考示例代码了解如何使用 DigestStream。示例代码的逻辑如下：


1. 使用 `fetch()` 方法获取网站内容并以 `ReadableStream` 的形式获取响应体。同时，使用 `tee()` 方法对获取的 `ReadableStream` 进行拷贝（tee），返回包含两个 `ReadableStream` 的数组。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">使用 <code>tee()</code> 方法的原因是为了同时处理响应体的两个不同操作：一个用于创建 SHA\-256 摘要，另一个用于构建新的响应。   </div>
   

2. 创建一个 `DigestStream` 对象并把摘要算法设置为 SHA\-256。

3. 通过 `pipeThrough()` 方法把 `tee()` 方法返回的一个 `ReadableStream` 发送到 `DigestStream`。`DigestStream` 会生成该 `ReadableStream` 的 SHA\-256 摘要并把摘要返回给 `readable` 端。

4. 基于 `tee()` 方法返回的另一个 `ReadableStream` 构建一个新的响应。

5. 把 `DigestStream` 的 `readable` 端转换为 Uint8Array 数据，最后再转换为 16 进制字符串。这个 16 进制字符串随后被添加到新的响应的 Header。


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
