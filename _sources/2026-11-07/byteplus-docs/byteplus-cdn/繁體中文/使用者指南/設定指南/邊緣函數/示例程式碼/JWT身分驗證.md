---
title: "JWT身分驗證"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/jwt-auth-cn-zh-tw"
---

本示例展示如何驗證 JWT。

<span id="什麼是-jwt"></span>
## 什麼是 JWT

JWT（JSON Web Token）以 JSON 物件的形式安全地傳輸資訊，在 [RFC 7519](https://datatracker.ietf.org/doc/html/rfc7519) 中定義。JWT 由 Header、Payload 和 Signature 組成，每部分之間用點號(.)連接，即 `Header.Payload.Signature`。


* Header：Token 的類型和簽章演算法。Header 需要被 Base64URL 編碼。

* Payload：JWT 的聲明，包含使用者資訊或其他 metadata。Payload 需要被 Base64URL 編碼。

* Signature：簽章，用於驗證 JWT 的真實性。Signature 的產生方式如下：

   1. 將 Header 和 Payload 部分分別進行 Base64URL 編碼。

   2. 將編碼後的 Header 和 Payload 用點號(.)連接成字串。

   3. 使用 Header 中指定的摘要演算法和密鑰對上一步得到的字串進行簽章。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">對於使用對稱加密的演算法，例如 HS256，簽章與驗證所使用的密鑰是相同的。   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">對於使用非對稱加密的演算法，例如 RS256，簽章使用私鑰；驗證使用公鑰。   </div>
   

   4. 將上一步得到的簽章結果進行 Base64URL 編碼，得到 Signature。


假設 JWT 編碼前的 Header、編碼前的 Payload 和密鑰分別如下：

編碼前的 Header：

```JSON
{
    "typ":"JWT",
    "alg":"HS256"
}
```


編碼前的 Payload:

```JSON
{
    "sub": "1234567890",
    "name": "John Doe",
    "iat": 1516239022,
    "exp": 1516242622,
    "iss": "example.com"
}
```


密鑰：`my-jwt-secret`。則 Signature 是 `g50NxVfIcxfsiX_cHbpS_-xQgzvoEc3R5roRzJuXeB4`。

那麼，JWT 是 `eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyLCJleHAiOjE1MTYyNDI2MjIsImlzcyI6ImV4YW1wbGUuY29tIn0.g50NxVfIcxfsiX_cHbpS_-xQgzvoEc3R5roRzJuXeB4`。

<span id="jwt-的驗證流程"></span>
## JWT 的驗證流程

JWT 驗證的目的是確保 JWT 沒有被篡改，並且來自可信的發布者。以 HS256 和 RS256 為例，JWT 的驗證流程如下：

HS256 JWT 的驗證步驟:


1. 取得 JWT，並從 JWT 中獲取 Header.Payload。

2. 用 HMAC 密鑰和 SHA\-256 簽章演算法對 Header.Payload 進行簽章。

3. 比對計算得到的簽章與 JWT 中的 Signature 是否相同。

   * 如果相同，則 JWT 驗證成功。

   * 如果不相同，則 JWT 驗證失敗。


RS256 JWT 的驗證步驟:


1. 取得 JWT，並從 Header 中獲取 kid，用 kid 找到對應的 RSA 公鑰。

2. 從 JWT 中獲取 Signature，用 Base64Url 解碼 Signature 並用 RSA 公鑰對其進行解密。解密完成後會得到一個 SHA\-256 摘要。

3. 從 JWT 中獲取 Header.Payload，用 SHA\-256 取得 Header.Payload 的 SHA\-256 摘要。

4. 比對兩個 SHA\-256 摘要是否相同。

   * 如果相同，則 JWT 驗證成功。

   * 如果不相同，則 JWT 驗證失敗。


<span id="示例程式碼"></span>
## 示例程式碼

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">為清晰展示實作邏輯，本示例包含多個 .js 檔案。編輯函式程式碼時，您需要將所有 .js 檔案打包為單一 default.js 檔案，打包後的程式碼需符合 ES6 標準。</div>


* <div data-tips="true" data-tips-type="warning">本示例不包含打包所需的入口檔案，也不包含監聽 fetch 事件的相關邏輯。您需要：</div>


   * <div data-tips="true" data-tips-type="warning">自行建立入口檔案</div>


   * <div data-tips="true" data-tips-type="warning">在入口檔案中呼叫 addEventListener() 方法監聽 fetch 事件</div>


   * <div data-tips="true" data-tips-type="warning">將 jwt.js 中的方法設定為回呼函式，例如：</div>


      * <div data-tips="true" data-tips-type="warning">驗證 HS256 JWT：呼叫 verifyHS256() 方法</div>


      * <div data-tips="true" data-tips-type="warning">驗證 RS256 JWT：先呼叫 keyRS256() 取得公鑰，再呼叫 verifyRS256() 驗證</div>



本示例包含多個 .js 檔案：


* util.js：實作了以下方法：

   * bin2hex()：將 ArrayBuffer 或 Uint8Array 轉換為十六進位字串

   * hex2bin()：將十六進位字串轉換為 Uint8Array

   * base64URLEncode()：Base64URL 編碼

   * base64URLDecod()：Base64URL 解碼

   * ab2binstr()：將 ArrayBuffer 轉換為二進位字串

   * binstr2ab()：將二進位字串轉換為 ArrayBuffer

* jwt.js：實作了以下方法：

   * signHS256()：透過 HMAC SHA256（即 JWT 中的 "HS256"）演算法實作 JWT 簽章。由於 HMAC 是對稱加密，因此簽章和驗證都使用相同密鑰

   * verifyHS256()：透過 HMAC SHA256（即 JWT 中的 "HS256"）演算法實作 JWT 驗證。由於 HMAC 是對稱加密，因此簽章和驗證都使用相同密鑰

   * signRS256()：透過 RSASSA\-PKCS1\-v1_5 和 SHA\-256（即 JWT 中的 "RS256"）演算法實作 JWT 簽章

   * verifyRS256()：透過 RSASSA\-PKCS1\-v1_5 和 SHA\-256（即 JWT 中的 "RS256"）演算法實作 JWT 驗證

   * keyRS256()：取得 RSA 公鑰或私鑰。由於 RSASSA\-PKCS1\-v1_5 是非對稱加密，因此簽章使用私鑰；驗證使用公鑰


<span id="util-js"></span>
### util.js

```JavaScript
function bin2hex(bin) {
  if (bin instanceof ArrayBuffer) bin = new Uint8Array(bin);

  return Array.from(bin).map(
    (byte) => byte.toString(16).padStart(2, '0')
  ).join('')
}

function hex2bin(hex) {
  const bytes = [];
  for (let i = 0; i < hex.length; i += 2) {
    bytes.push(parseInt(hex.substr(i, 2), 16));
  }
  return new Uint8Array(bytes);
}

// base64url used in JWT
function base64URLEncode(str) {
  return btoa(str)
        .replace(/\+/g, '-')
    .replace(/\//g, '_')
    .replace(/=/g, '');
}

function base64URLDecode(str) {
    str = str.replace(/-/g, '+').replace(/_/g, '/');
    const padding = '='.repeat((4 - str.length % 4) % 4);
    str = (str + padding).replace(/-/g, '+').replace(/_/g, '/');
    return atob(str);
}

function arrayBufferToBinaryString(buffer) {
  const uint8Array = new Uint8Array(buffer);
  let binaryString = '';

  uint8Array.forEach(byte => {
        binaryString += String.fromCharCode(byte);
    });

  return binaryString;
}

function binaryStringToArrayBuffer(binaryString) {
    const buffer = new ArrayBuffer(binaryString.length);
    const uint8Array = new Uint8Array(buffer);

    for (let i = 0; i < binaryString.length; i++) {
        uint8Array[i] = binaryString.charCodeAt(i);
    }

    return buffer;
}

module.exports = {
  "bin2hex": bin2hex,
  "hex2bin": hex2bin,
    "base64URLEncode": base64URLEncode,
    "base64URLDecode": base64URLDecode,
    "ab2binstr": arrayBufferToBinaryString,
    "binstr2ab": binaryStringToArrayBuffer
}

```


<span id="jwt-js"></span>
### jwt.js

```JavaScript
const U = require("../util.js");

function isNode() {
  return typeof isSparrow === "undefined" && typeof module !== "undefined";
}

if (isNode()) {
  crypto = globalThis.crypto;
}

function payload2str(payload) {
  if (typeof payload == "string") {
    return payload;
  } else {
    return JSON.stringify(payload);
  }
}

function formatSignData(
  headerEnc,
  payloadEnc
) {
  return new TextEncoder().encode(
    headerEnc + "." + payloadEnc
  );
}

function createSignData(
  header, // in strings
  payload // in strings
) {
  const headerStr = JSON.stringify(header);
  const payloadStr = payload2str(payload);
  const headerEnc = U.base64URLEncode(headerStr);
  const payloadEnc = U.base64URLEncode(payloadStr);
  return {
    "header": headerEnc,
    "payload": payloadEnc,
    "data": formatSignData(headerEnc, payloadEnc)
  }
}

async function doSign(
  key,       // already imported key
  input,     // input data
  jwtAlgo,   // jwt algorithm, used for header field
  signAlgo   // sign algorithm, can be HMAC or RSA related one
) {
  const {
    header,
    payload,
    data
  } = createSignData(
    {alg:jwtAlgo},
    input
  );
  const signature = await crypto.subtle.sign(signAlgo, key, data);
  const sig= U.base64URLEncode(U.ab2binstr(signature));
  return `${header}.${payload}.${sig}`;
}

async function doVerify(
  key,        // already imported
  token,      // input token
  jwtAlgo,    // jwt algorithm
  verifyAlgo, // verify algorithm
  verify      // whether verify header
) {
  const [header, payload, signatureEnc] = token.split('.');
  if (header === undefined ||
      payload === undefined ||
      signatureEnc == undefined) {
    throw new Error("invalid JWT token")
  }

  // parsing the header to verify whether the jwt algorithm is valid or not
  if (verify) {
    const jwtHeader = JSON.parse(header);
    if (!jwtHeader || jwtHeader.alg != jwtAlgo) {
      throw new Error("mismatched JWT algorithm");
    }
  }

  // perform verify
  const data = formatSignData(header, payload);
  const signature = U.binstr2ab(U.base64URLDecode(signatureEnc));
  return await crypto.subtle.verify(verifyAlgo, key, signature, data);
}

/** ---------------------------------------------------------------------------
 * JWT HS256
 ** --------------------------------------------------------------------------*/
async function keyHS256(rawKey) {
  const kbuf = new TextEncoder().encode(rawKey);
  return await crypto.subtle.importKey(
    'raw',
    kbuf,
    {
      name: "HMAC",
      hash: {
        name: "SHA-256"
      }
    },
    true,
    ["sign", "verify"]
  );
}

async function signHS256(rawKey, input) {
  const key = await keyHS256(rawKey);
  return doSign(
    key,
    input,
    "HS256",
    "HMAC"
  );
}

async function verifyHS256(rawKey, token) {
  const key = await keyHS256(rawKey);
  return doVerify(
    key,
    token,
    "HS256",
    "HMAC",
    false
  );
}

/** ---------------------------------------------------------------------------
 * JWT RS256
 ** --------------------------------------------------------------------------*/
async function keyRS256(keyString, keyType) {
    const keyData = Uint8Array.from(atob(keyString), c => c.charCodeAt(0));
    const importedKey = await crypto.subtle.importKey(
        'spki', // or 'pkcs8' based on keyType (public or private)
        keyData,
        { name: 'RSASSA-PKCS1-v1_5', hash: { name: 'SHA-256' } },
        true,
        (keyType === 'public') ? ['verify'] : ['sign']
    );
    return importedKey;
}

async function signRS256(privateKey, payload) {
  if (typeof privateKey === "string") {
    privateKey = await keyRS256(privateKey, "private")
  }
  return doSign(
    privateKey,
    payload,
    "RS256",
    "RSASSA-PKCS1-v1_5"
  );
}

async function verifyRS256(publicKey, token) {
  if (typeof publicKey === "string") {
    publicKey = await keyRS256(publicKey, "public")
  }
  return doVerify(
    publicKey,
    token,
    "RS256",
    "RSASSA-PKCS1-v1_5",
    false
  );
}

module.exports = {
  "HS256": {
    sign: signHS256,
    verify: verifyHS256
  },
  "RS256": {
    sign: signRS256,
    verify: verifyRS256,
    key: keyRS256
  }
}
```


<span id="相關執行時-api"></span>
## 相關執行時 API


* [importKey() 方法](https://docs.byteplus.com/docs/byteplus-cdn/docs_cn-importKey-exportKey-generateKey-cn-zh-tw)

* [sign() 方法](https://docs.byteplus.com/docs/byteplus-cdn/docs_cn-sign-verify-cn-zh-tw)

* [verify() 方法](https://docs.byteplus.com/docs/byteplus-cdn/docs_cn-sign-verify-cn-zh-tw)
