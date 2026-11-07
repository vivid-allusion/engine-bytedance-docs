---
title: "sign()/verify()"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-sign-verify-cn"
---

sign() 用于生成数字签名。verify() 用于验证数字签名。

参见 MDN 文档 [sign](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/sign) 、[verify](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/verify)。

<span id="支持的算法"></span>
## 支持的算法

参见 [支持的算法](https://docs.byteplus.com/docs/byteplus-cdn/docs_cn-SupportedAlgorithms-cn)。

<span id="示例"></span>
## 示例

```JavaScript
// 基于 RSASSA-PKCS1-v1_5 算法生成数字签名
async function sign_handle(priv_key, plain) {
 var algorithm = {name: "RSASSA-PKCS1-v1_5"};
 return await crypto.subtle.sign(algorithm, priv_key, plain);
}
// 验证基于 RSASSA-PKCS1-v1_5 算法生成的数字签名
async function verify_handle(pub_key, plain, sig) {
 var algorithm = {name: "RSASSA-PKCS1-v1_5"};
 return await crypto.subtle.verify(algorithm, pub_key, sig, plain);
}
```
