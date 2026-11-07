---
title: "importKey()/exportKey()/generateKey()"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-importKey-exportKey-generateKey"
---

importKey() is used to import a key. exportKey() is used to export a key. generateKey() is used to generate a key or key pair.

See MDN documentation for [importKey()](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/importKey), [exportKey()](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/exportKey), [generateKey()](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/generateKey).

<span id="supported-algorithms"></span>
## Supported algorithms

See [Supported Algorithms](https://docs.byteplus.com/docs/byteplus-cdn/docs-SupportedAlgorithms)。

<span id="example"></span>
## Example

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
