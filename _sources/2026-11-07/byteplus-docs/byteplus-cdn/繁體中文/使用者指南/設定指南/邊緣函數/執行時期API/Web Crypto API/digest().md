---
title: "digest()"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-digest-cn-zh-tw"
---

產生指定資料的摘要。參見 MDN 文件 [digest](https://developer.mozilla.org/zh-CN/docs/Web/API/SubtleCrypto/digest)。

<span id="支援的演算法"></span>
## 支援的演算法

參見 [支援的演算法](https://docs.byteplus.com/docs/byteplus-cdn/docs_cn-SupportedAlgorithms-cn-zh-tw)。

<span id="範例"></span>
## 範例

```JavaScript
// 基於 SHA256 演算法產生資料的摘要
async function digest_handle(data) {
  var algorithm = {name: "SHA256"};
  return await crypto.subtle.digest(algorithm, data);
}
```
