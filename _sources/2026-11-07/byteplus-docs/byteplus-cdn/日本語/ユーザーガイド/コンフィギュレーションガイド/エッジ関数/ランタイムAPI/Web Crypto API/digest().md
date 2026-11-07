---
title: "digest()"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-digest-jp"
---

指定されたデータのダイジェストを生成します。MDNドキュメントの[digest()](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/digest)を参照してください。

<span id="サポートされているアルゴリズム"></span>
## サポートされているアルゴリズム

[サポートされているアルゴリズム](https://docs.byteplus.com/docs/byteplus-cdn/docs-SupportedAlgorithms-jp)を参照してください。

<span id="例"></span>
## 例

```JavaScript
// Generates digest of the data based on SHA256
async function digest_handle(data) {
  var algorithm = {name: "SHA256"};
  return await crypto.subtle.digest(algorithm, data);
}
```
