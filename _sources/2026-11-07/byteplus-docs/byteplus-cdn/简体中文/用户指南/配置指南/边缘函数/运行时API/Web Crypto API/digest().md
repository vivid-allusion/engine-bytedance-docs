---
title: "digest()"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-digest-cn"
---

生成指定数据的摘要。参见 MDN 文档 [digest](https://developer.mozilla.org/zh-CN/docs/Web/API/SubtleCrypto/digest)。

<span id="支持的算法"></span>
## 支持的算法

参见 [支持的算法](https://docs.byteplus.com/docs/byteplus-cdn/docs_cn-SupportedAlgorithms-cn)。

<span id="示例"></span>
## 示例

```JavaScript
// 基于 SHA256 算法生成数据的摘要
async function digest_handle(data) {
  var algorithm = {name: "SHA256"};
  return await crypto.subtle.digest(algorithm, data);
}
```
