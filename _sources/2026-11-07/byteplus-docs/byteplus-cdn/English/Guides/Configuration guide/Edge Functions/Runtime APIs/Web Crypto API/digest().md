---
title: "digest()"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-digest"
---

Generates a digest of the given data. See the [digest()](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/digest) in MDN documentation.

<span id="supported-algorithms"></span>
## Supported algorithms

See [Supported Algorithms](https://docs.byteplus.com/docs/byteplus-cdn/docs-SupportedAlgorithms)。

<span id="example"></span>
## Example

```JavaScript
// Generates digest of the data based on SHA256
async function digest_handle(data) {
  var algorithm = {name: "SHA256"};
  return await crypto.subtle.digest(algorithm, data);
}
```
