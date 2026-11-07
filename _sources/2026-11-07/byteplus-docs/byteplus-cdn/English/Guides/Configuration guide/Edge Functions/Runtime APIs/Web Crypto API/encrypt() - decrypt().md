---
title: "encrypt()/decrypt()"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-encrypt-decrypt"
---

encrypt() is used to encrypt data. decrypt() is used to decrypt encrypted data.

See MDN documentation for [encrypt](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/encrypt) and [decrypt](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/decrypt).

<span id="supported-algorithms"></span>
## Supported algorithms

See [Supported Algorithms](https://docs.byteplus.com/docs/byteplus-cdn/docs-SupportedAlgorithms)。

<span id="example"></span>
## Example

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
