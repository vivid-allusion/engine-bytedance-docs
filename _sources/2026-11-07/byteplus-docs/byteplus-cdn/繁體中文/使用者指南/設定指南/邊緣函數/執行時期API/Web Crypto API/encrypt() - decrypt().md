---
title: "encrypt()/decrypt()"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-encrypt-decrypt-cn-zh-tw"
---

encrypt() 用於加密資料。decrypt() 用於解密已加密的資料。

參見 MDN 文件 [encrypt](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/encrypt)、[decrypt](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/decrypt)。

<span id="支援的演算法"></span>
## 支援的演算法

參見 [支援的演算法](https://docs.byteplus.com/docs/byteplus-cdn/docs_cn-SupportedAlgorithms-cn-zh-tw)。

<span id="範例"></span>
## 範例

```JavaScript
// 基於 AES-CBC 演算法加密資料
async function encrypt_handle(key, plain) {
  var algorithm = {name: "AES-CBC"};
  return await crypto.subtle.encrypt(algorithm, key, plain);
}
// 解密基於 AES-CBC 演算法加密的資料
async function decrypt_handle(key, cipher) {
  var algorithm = {name: "AES-CBC"};
  return await crypto.subtle.decrypt(algorithm, key, cipher);
}
```
