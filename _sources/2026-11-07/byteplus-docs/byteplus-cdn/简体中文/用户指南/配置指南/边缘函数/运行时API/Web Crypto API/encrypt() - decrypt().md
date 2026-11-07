---
title: "encrypt()/decrypt()"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-encrypt-decrypt-cn"
---

encrypt() 用于加密数据。decrypt() 用于解密已加密的数据。

参见 MDN 文档 [encrypt](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/encrypt) 、[decrypt](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/decrypt)。

<span id="支持的算法"></span>
## 支持的算法

参见 [支持的算法](https://docs.byteplus.com/docs/byteplus-cdn/docs_cn-SupportedAlgorithms-cn)。

<span id="示例"></span>
## 示例

```JavaScript
// 基于 AES-CBC 算法加密数据
async function encrypt_handle(key, plain) {
  var algorithm = {name: "AES-CBC"};
  return await crypto.subtle.encrypt(algorithm, key, plain);
}
// 解密基于 AES-CBC 算法加密的数据
async function decrypt_handle(key, cipher) {
  var algorithm = {name: "AES-CBC"};
  return await crypto.subtle.decrypt(algorithm, key, cipher);
}
```
