---
title: "importKey()/exportKey()/generateKey()"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-importKey-exportKey-generateKey-cn-zh-tw"
---

importKey() 用於匯入金鑰。exportKey() 用於匯出金鑰。generateKey() 用於產生金鑰或金鑰對。

參見 MDN 文件 [importKey](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/importKey)、[exportKey](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/exportKey)、[generateKey](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/generateKey)。

<span id="支援的演算法"></span>
## 支援的演算法

參見 [支援的演算法](https://docs.byteplus.com/docs/byteplus-cdn/docs_cn-SupportedAlgorithms-cn-zh-tw)。

<span id="範例"></span>
## 範例

```JavaScript
async function handle() {
  var algorithm = {name: "HMAC", hash: {name: "SHA-512"}};
  // 產生 HMAC 金鑰，宣告此金鑰用於產生數位簽章和驗證數位簽章
  var key = await crypto.subtle.generateKey(algorithm, 
      true, ['sign', 'verify']);
  
  // 匯出產生的 HMAC 金鑰，格式為 Raw 格式
  var raw_key = await crypto.subtle.exportKey("Raw", key);

  // 匯入先前匯出的 HMAC 金鑰，宣告此金鑰用於產生數位簽章和驗證數位簽章
  var import_key = await crypto.subtle.importKey("Raw", raw_key, algorithm, 
      true, ['sign', 'verify']);
}
```
