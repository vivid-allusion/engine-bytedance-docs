---
title: "sign()/verify()"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-sign-verify"
---

sign() is used to generate a digital signature. verify() is used to verify a digital signature.

See MDN documentation for [sign()](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/sign) and [verify()](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/verify).

<span id="supported-algorithms"></span>
## Supported algorithms

See [Supported Algorithms](https://docs.byteplus.com/docs/byteplus-cdn/docs-SupportedAlgorithms)。

<span id="example"></span>
## Example

```JavaScript
// Generate digital signature based on RSASSA-PKCS1-v1_5 algorithm
async function sign_handle(priv_key, plain) {
 var algorithm = {name: "RSASSA-PKCS1-v1_5"};
 return await crypto.subtle.sign(algorithm, priv_key, plain);
}
// Verify digital signatures generated using the RSASSA-PKCS1-v1_5 algorithm
async function verify_handle(pub_key, plain, sig) {
 var algorithm = {name: "RSASSA-PKCS1-v1_5"};
 return await crypto.subtle.verify(algorithm, pub_key, sig, plain);
}
```
