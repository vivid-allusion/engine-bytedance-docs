---
title: "JWT鉴权"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/jwt-auth-cn"
---

本示例展示了如何验证 JWT。

<span id="什么是-jwt"></span>
## 什么是 JWT

JWT（JSON Web Token）以 JSON 对象的形式安全地传输信息，在 [RFC 7519](https://datatracker.ietf.org/doc/html/rfc7519) 中定义。JWT 由 Header、Payload 和 Signature 组成，每部分之间用点（.）连接，即 `Header.Payload.Signature`。


* Header：Token 的类型和签名算法。Header 需要被 Base64URL 编码。

* Payload：JWT 的声明，包括用户信息或其他 metadata。Payload 需要被 Base64URL 编码。

* Signature：签名，用于验证 JWT 的真实性。Signature 的生成方式如下：

   1. 将 Header 和 Payload 部分分别进行 Base64URL 编码。

   2. 将编码后的 Header 和 Payload 用点（.）连接成字符串。

   3. 使用 Header 中指定的摘要算法和密钥对上一步得到的字符串进行签名。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">对于使用对称加密的算法，例如 HS256，签名与验证所使用的密钥是相同的。   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">对于使用非对称加密的算法，例如 RS256，签名使用私钥；验证使用公钥。   </div>
   

   4. 将上一步得到的签名结果进行 Base64URL 编码，得到 Signature。


假设 JWT 编码前的 Header、编码前的 Payload 和密钥分别如下：

编码前的 Header：

```JSON
{
    "typ":"JWT",
    "alg":"HS256"
}
```


编码前的 Payload:

```JSON
{
    "sub": "1234567890",
    "name": "John Doe",
    "iat": 1516239022,
    "exp": 1516242622,
    "iss": "example.com"
}
```


密钥：`my-jwt-secret`。则 Signature 是 `g50NxVfIcxfsiX_cHbpS_-xQgzvoEc3R5roRzJuXeB4`。

那么，JWT 是 `eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyLCJleHAiOjE1MTYyNDI2MjIsImlzcyI6ImV4YW1wbGUuY29tIn0.g50NxVfIcxfsiX_cHbpS_-xQgzvoEc3R5roRzJuXeB4`。

<span id="jwt-的验证过程"></span>
## JWT 的验证过程

JWT 验证的目的是确保 JWT 没有被篡改，并且来自可信的发布者。以 HS256 和 RS256 为例，JWT 的验证过程如下：

HS256 JWT 的验证步骤:


1. 获取 JWT，并从 JWT 中获取 Header.Payload。

2. 用 HMAC 密钥和 SHA\-256 签名算法对 Header.Payload 进行签名。

3. 比较计算得到的签名与 JWT 中的 Signature 是否相同。

   * 如果相同，则 JWT 验证成功。

   * 如果不相同，则 JWT 验证失败。


RS256 JWT 的验证步骤:


1. 获取 JWT，并从 Header 中获取 kid，用 kid 找到对应的 RSA 公钥。

2. 从 JWT 中获取 Signature，用 Base64Url 解码 Signature 并用 RSA 公钥对其进行解密。解密完成后会得到一个 SHA\-256 摘要。

3. 从 JWT 中获取 Header.Payload，用 SHA\-256 获取 Header.Payload 的 SHA\-256 摘要。

4. 比较两个 SHA\-256 摘要是否相同。

   * 如果相同，则 JWT 验证成功。

   * 如果不相同，则 JWT 验证失败。


<span id="示例代码"></span>
## 示例代码

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">为了能更清晰地展示具体的实现逻辑，本示例包含了多个 .js 文件。在编辑函数代码时，您需要把所有 .js 文件打包为一个 .js 文件，并把打包后的文件的内容作为 default.js 的内容。打包后的代码需要符合 ES6 标准。</div>


* <div data-tips="true" data-tips-type="warning">本示例不包含打包所需的入口文件，也不包含监听 fetch 事件的相关逻辑。您需要自行创建一个入口文件。在该入口文件中，您调用 addEventListener() 方法监听 fetch 事件并把 jwt.js 中的方法设置为回调函数。例如，如果您需要验证用户请求中的 JWT，您可以首先通过监听 fetch 事件获取用户请求中的 JWT。然后验证获取的 JWT：</div>


   * <div data-tips="true" data-tips-type="warning">对于 HS256 JWT：调用 verifyHS256() 验证 JWT。</div>


   * <div data-tips="true" data-tips-type="warning">对于 RS256 JWT：调用 keyRS256() 获取公钥，再调用 verifyRS256() 验证 JWT。</div>



本示例包含多个 .js 文件。


* util.js：实现了以下方法：

   * bin2hex()：将 ArrayBuffer 或 Uint8Array 转换为十六进制字符串。

   * hex2bin()：将十六进制字符串转换为 Uint8Array。

   * base64URLEncode()：Base64URL 编码。

   * base64URLDecod()：Base64URL 解码。

   * ab2binstr()：将 ArrayBuffer 转换为二进制字符串。

   * binstr2ab()：将二进制字符串转换为 ArrayBuffer。

* jwt.js：实现了以下方法：

   * signHS256()：通过 HMAC SHA256（即 JWT 中的 "HS256"）算法实现 JWT 签名。由于 HMAC 是对称加密，因此签名和验证都使用相同的密钥。

   * verifyHS256()：通过 HMAC SHA256（即 JWT 中的 "HS256"）算法实现 JWT 验证。由于 HMAC 是对称加密，因此签名和验证都使用相同的密钥。

   * signRS256()：通过 RSASSA\-PKCS1\-v1_5 和 SHA\-256（即 JWT 中的 "RS256"） 算法实现 JWT 签名。

   * verifyRS256()：通过 RSASSA\-PKCS1\-v1_5 和 SHA\-256（即 JWT 中的 "RS256"） 算法实现 JWT 验证。

   * keyRS256()：获取 RSA 公钥或私钥。由于 RSASSA\-PKCS1\-v1_5 是非对称加密，因此签名使用私钥；验证使用公钥。


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


<span id="相关运行时-api"></span>
## 相关运行时 API


* [importKey() 方法](https://docs.byteplus.com/docs/byteplus-cdn/docs_cn-importKey-exportKey-generateKey-cn)

* [sign() 方法](https://docs.byteplus.com/docs/byteplus-cdn/docs_cn-sign-verify-cn)

* [verify() 方法](https://docs.byteplus.com/docs/byteplus-cdn/docs_cn-sign-verify-cn)
