---
title: "DigestStream"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DigestStream-jp"
---

DigestStreamオブジェクトは、指定されたデータストリームのダイジェストを生成するための[TransformStream](https://docs.byteplus.com/docs/byteplus-cdn/docs-Streams-jp#transformstream)オブジェクトです。

<span id="コンストラクター"></span>
## コンストラクター

```JavaScript
let {readable, writable} = new DigestStream(algorithm)
```


<span id="パラメーター"></span>
### パラメーター


* `algorithm` *string/object*：ダイジェストアルゴリズム。文字列または、nameという文字列プロパティを含むオブジェクトを指定できます。文字列は以下の値を設定できます：

   * `SHA-1`：SHA\-1ダイジェストアルゴリズム

   * `SHA-256`：SHA\-256ダイジェストアルゴリズム

   * `SHA-384`：SHA\-384ダイジェストアルゴリズム

   * `SHA-512`：SHA\-512ダイジェストアルゴリズム

   * `MD5`：MD5ダイジェストアルゴリズム


<span id="サポートされているアルゴリズム"></span>
## サポートされているアルゴリズム

[サポートされているアルゴリズム](https://docs.byteplus.com/docs/byteplus-cdn/supported-web-crypto-stream-algo-jp)をご参照ください。

<span id="使用例"></span>
## 使用例

DigestStreamの使用方法は以下のサンプルコードを参考にしてください。サンプルコードの処理の流れは次の通りです：


1. fetch()を使用してウェブサイトのコンテンツを取得し、レスポンスボディを`ReadableStream`として取得します。同時に、`tee()`メソッドを使用して取得した`ReadableStream`を複製し、2つの`ReadableStream`を含む配列を返します。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><code>tee()</code>メソッドを使用する理由は、レスポンスボディに対する2つの異なる操作（SHA\-256ダイジェストの作成と新しいレスポンスの構築）を同時に処理するためです。   </div>
   

2. DigestStreamオブジェクトを作成し、ダイジェストアルゴリズムをSHA\-256に設定します。

3. `pipeThrough()`メソッドを使用して、`tee()`メソッドが返した一方の`ReadableStream`をDigestStreamに送信します。DigestStreamはその`ReadableStream`のSHA\-256ダイジェストを生成し、`readable`側にダイジェストを返します。

4. `tee()`メソッドが返したもう一方の`ReadableStream`を基に新しいレスポンスを構築します。

5. DigestStreamの`readable`側をUint8Arrayデータに変換し、最終的に16進数文字列に変換します。この16進数文字列は、新しいレスポンスのヘッダーに追加されます。


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
