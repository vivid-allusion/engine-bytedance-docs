---
title: "DigestStream"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DigestStream-zh-tw"
---

DigestStream 物件是一個 [TransformStream](https://docs.byteplus.com/docs/byteplus-cdn/docs_cn-Streams-cn-zh-tw#transformstream) 物件，用於產生指定資料流的摘要。

<span id="建構函數"></span>
## 建構函數

```JavaScript
let {readable, writable} = new DigestStream(algorithm)
```


<span id="參數說明"></span>
### 參數說明


* `algorithm` *string/object*：摘要演算法。您可以傳入一個字串或者一個包含 name 字串屬性的物件。您可以將字串設定為以下值：

   * `SHA-1`：SHA\-1 摘要演算法。

   * `SHA-256`：SHA\-256 摘要演算法。

   * `SHA-384`：SHA\-384 摘要演算法。

   * `SHA-512`：SHA\-512 摘要演算法。

   * `MD5`：MD5 摘要演算法。


<span id="支援的演算法"></span>
## 支援的演算法

參見 [支援的演算法](https://docs.byteplus.com/docs/byteplus-cdn/supported-web-crypto-stream-algo-zh-tw)。

<span id="範例"></span>
## 範例

您可以參考範例程式碼了解如何使用 DigestStream。範例程式碼的邏輯如下：


1. 使用 `fetch()` 方法獲取網站內容並以 `ReadableStream` 的形式獲取回應主體。同時，使用 `tee()` 方法對獲取的 `ReadableStream` 進行複製（tee），傳回包含兩個 `ReadableStream` 的陣列。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">使用 <code>tee()</code> 方法的原因是為了同時處理回應主體的兩個不同操作：一個用於建立 SHA\-256 摘要，另一個用於建構新的回應。   </div>
   

2. 建立一個 `DigestStream` 物件並將摘要演算法設定為 SHA\-256。

3. 透過 `pipeThrough()` 方法將 `tee()` 方法傳回的一個 `ReadableStream` 發送到 `DigestStream`。`DigestStream` 會產生該 `ReadableStream` 的 SHA\-256 摘要並將摘要傳回給 `readable` 端。

4. 基於 `tee()` 方法傳回的另一個 `ReadableStream` 建構一個新的回應。

5. 將 `DigestStream` 的 `readable` 端轉換為 Uint8Array 資料，最後再轉換為 16 進位字串。這個 16 進位字串隨後被新增到新的回應的 Header。


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
