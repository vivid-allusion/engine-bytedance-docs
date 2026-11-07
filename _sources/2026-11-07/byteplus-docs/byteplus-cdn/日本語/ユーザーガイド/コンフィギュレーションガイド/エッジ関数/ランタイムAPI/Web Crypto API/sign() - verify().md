---
title: "sign()/verify()"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-sign-verify-jp"
---

sign()はデジタル署名を生成するために使用され、verify()はデジタル署名を検証するために使用されます。

MDNドキュメントの[sign()](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/sign)と[verify()](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/verify)を参照してください。

<span id="サポートされているアルゴリズム"></span>
## サポートされているアルゴリズム

[サポートされているアルゴリズム](https://docs.byteplus.com/docs/byteplus-cdn/docs-SupportedAlgorithms-jp)を参照してください。

<span id="例"></span>
## 例

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
