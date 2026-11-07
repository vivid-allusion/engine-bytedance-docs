---
title: "sign()/verify()"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-sign-verify-cn-zh-tw"
---

sign() 用於產生數位簽章。verify() 用於驗證數位簽章。

參見 MDN 文件 [sign](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/sign)、[verify](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/verify)。

<span id="支援的演算法"></span>
## 支援的演算法

參見 [支援的演算法](https://docs.byteplus.com/docs/byteplus-cdn/docs_cn-SupportedAlgorithms-cn-zh-tw)。

<span id="範例"></span>
## 範例

```JavaScript
// 基於 RSASSA-PKCS1-v1_5 演算法產生數位簽章
async function sign_handle(priv_key, plain) {
 var algorithm = {name: "RSASSA-PKCS1-v1_5"};
 return await crypto.subtle.sign(algorithm, priv_key, plain);
}
// 驗證基於 RSASSA-PKCS1-v1_5 演算法產生的數位簽章
async function verify_handle(pub_key, plain, sig) {
 var algorithm = {name: "RSASSA-PKCS1-v1_5"};
 return await crypto.subtle.verify(algorithm, pub_key, sig, plain);
}
```
