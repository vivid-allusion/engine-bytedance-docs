---
title: "importKey()/exportKey()/generateKey()"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-importKey-exportKey-generateKey-jp"
---

importKey()は鍵をインポートするために使用され、exportKey()は鍵をエクスポートするために使用されます。generateKey()は鍵または鍵ペアを生成するために使用されます。

MDNドキュメントの[importKey()](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/importKey)、[exportKey()](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/exportKey)、[generateKey()](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/generateKey)を参照してください。

<span id="サポートされているアルゴリズム"></span>
## サポートされているアルゴリズム

[サポートされているアルゴリズム](https://docs.byteplus.com/docs/byteplus-cdn/docs-SupportedAlgorithms-jp)を参照してください。

<span id="例"></span>
## 例

```JavaScript
async function handle() {
  var algorithm = {name: "HMAC", hash: {name: "SHA-512"}};
  // Generate an HMAC key and declare that the key is used to generate and verify electronic signatures
  var key = await crypto.subtle.generateKey(algorithm, 
      true, ['sign', 'verify']);
  
  // Export the generated HMAC key in Raw format
  var raw_key = await crypto.subtle.exportKey("Raw", key);

  // Import the previously exported HMAC key and declare it to be used for generating and verifying electronic signatures
  var import_key = await crypto.subtle.importKey("Raw", raw_key, algorithm, 
      true, ['sign', 'verify']);
}
```
