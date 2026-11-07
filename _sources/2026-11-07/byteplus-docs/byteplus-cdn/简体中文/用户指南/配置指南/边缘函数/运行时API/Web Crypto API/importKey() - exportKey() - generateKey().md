---
title: "importKey()/exportKey()/generateKey()"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-importKey-exportKey-generateKey-cn"
---

importKey() 用于导入密钥。exportKey() 用于导出密钥。generateKey() 用于生成密钥或密钥对。

参见 MDN 文档 [importKey](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/importKey)、[exportKey](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/exportKey)、[generateKey](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/generateKey)。

<span id="支持的算法"></span>
## 支持的算法

参见 [支持的算法](https://docs.byteplus.com/docs/byteplus-cdn/docs_cn-SupportedAlgorithms-cn)。

<span id="示例"></span>
## 示例

```JavaScript
async function handle() {
  var algorithm = {name: "HMAC", hash: {name: "SHA-512"}};
  // 生成 HMAC 密钥，声明该密钥用于生成电子签名和验证电子签名
  var key = await crypto.subtle.generateKey(algorithm, 
      true, ['sign', 'verify']);
  
  // 导出生成的 HMAC 密钥，格式为 Raw 格式
  var raw_key = await crypto.subtle.exportKey("Raw", key);

  // 导入之前导出的 HMAC 密钥，声明该密钥用于生成电子签名和验证电子签名
  var import_key = await crypto.subtle.importKey("Raw", raw_key, algorithm, 
      true, ['sign', 'verify']);
}
```
