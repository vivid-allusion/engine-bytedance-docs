---
title: "encrypt()/decrypt()"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-encrypt-decrypt-jp"
---

encrypt()はデータを暗号化するために使用され、decrypt()は暗号化されたデータを復号化するために使用されます。

MDNドキュメントの[encrypt](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/encrypt)と[decrypt](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/decrypt)を参照してください。

<span id="サポートされているアルゴリズム"></span>
## サポートされているアルゴリズム

[サポートされているアルゴリズム](https://docs.byteplus.com/docs/byteplus-cdn/docs-SupportedAlgorithms-jp)を参照してください。

<span id="例"></span>
## 例

```JavaScript
// Encrypt data based on AES-CBC
async function encrypt_handle(key, plain) {
  var algorithm = {name: "AES-CBC"};
  return await crypto.subtle.encrypt(algorithm, key, plain);
}
// Decrypt data encrypted based on AES-CBC
async function decrypt_handle(key, cipher) {
  var algorithm = {name: "AES-CBC"};
  return await crypto.subtle.decrypt(algorithm, key, cipher);
}
```
