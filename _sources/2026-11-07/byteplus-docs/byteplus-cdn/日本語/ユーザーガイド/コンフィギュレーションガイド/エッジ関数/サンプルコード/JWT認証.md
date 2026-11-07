---
title: "JWT認証"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/functions_JWT_Authentication-jp"
---

この例は、JWTを検証する方法を示しています。

<span id="jwtとは"></span>
## JWTとは

JWT（JSON Web Token）は、[RFC 7519](https://datatracker.ietf.org/doc/html/rfc7519)で定義されているように、JSONオブジェクトの形式で情報を安全に伝送します。JWTはHeader、Payload、Signatureで構成され、各部分はドット（.）で区切られ、`Header.Payload.Signature`の形式になります。


* Header：トークンのタイプと署名アルゴリズム。HeaderはBase64URLエンコードする必要があります。

* Payload：JWTのクレーム。ユーザー情報やその他のメタデータを含みます。PayloadはBase64URLエンコードする必要があります。

* Signature：JWTの真正性を検証するために使用されます。Signatureは以下のように生成されます：

   1. HeaderとPayloadをそれぞれBase64URLエンコードします。

   2. エンコードされたHeaderとPayloadをドット（.）で連結します。

   3. Headerで指定されたダイジェストアルゴリズムと秘密鍵を使用して、結果の文字列に署名します。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">HS256などの対称暗号化を使用するアルゴリズムでは、署名と検証に同じ鍵が使用されます。   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">RS256などの非対称暗号化を使用するアルゴリズムでは、署名に秘密鍵が使用され、検証に公開鍵が使用されます。   </div>
   

   4. 前のステップの署名結果をBase64URLエンコードして、Signatureを取得します。


エンコード前のHeader、エンコード前のPayload、および秘密鍵が以下のようであると仮定します：

エンコード前のHeaderは：

```JSON
{
    "typ":"JWT",
    "alg":"HS256"
}
```


エンコード後のHeaderは：

```JSON
{
    "sub": "1234567890",
    "name": "John Doe",
    "iat": 1516239022,
    "exp": 1516242622,
    "iss": "example.com"
}
```


鍵は`my-jwt-secret`です。そして、Signatureは `g50NxVfIcxfsiX_cHbpS_-xQgzvoEc3R5roRzJuXeB4`です。

したがって、JWTは `eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyLCJleHAiOjE1MTYyNDI2MjIsImlzcyI6ImV4YW1wbGUuY29tIn0.g50NxVfIcxfsiX_cHbpS_-xQgzvoEc3R5roRzJuXeB4`となります。

<span id="jwt検証プロセス"></span>
## JWT検証プロセス

JWT検証の目的は、JWTが改ざんされておらず、信頼できる発行者からのものであることを確認することです。HS256とRS256を例にとると、JWT検証プロセスは以下の通りです：

HS256 JWT検証手順：


1. JWTを取得し、そこからHeader.Payloadを抽出します。

2. HMACキーとSHA\-256署名アルゴリズムを使用してHeader.Payloadに署名します。

3. 計算された署名とJWT内のSignatureを比較します。

   * 同じ場合、JWT検証は成功します。

   * 異なる場合、JWT検証は失敗します。


RS256 JWT検証手順：


1. JWTを取得し、Headerからkidを抽出し、そのkidを使用して対応するRSA公開鍵を見つけます。

2. JWTからSignatureを抽出し、SignatureをBase64Urlデコードし、RSA公開鍵を使用して復号化します。復号化後、SHA\-256ダイジェストが得られます。

3. JWTからHeader.Payloadを抽出し、SHA\-256を使用してそのSHA\-256ダイジェストを取得します。

4. 2つのSHA\-256ダイジェストを比較します。

   * 同じ場合、JWT検証は成功します。

   * 異なる場合、JWT検証は失敗します。


<span id="サンプルコード"></span>
## サンプルコード

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">具体的な実装ロジックをより明確に示すため、この例では複数の.jsファイルを含んでいます。関数コードを編集する際は、すべての.jsファイルを1つの.jsファイルにバンドルし、バンドルされたファイルの内容をdefault.jsの内容として使用する必要があります。バンドルされたコードはES6標準に準拠している必要があります。</div>


* <div data-tips="true" data-tips-type="warning">この例では、バンドルに必要なエントリーファイルや、fetchイベントをレッスンするためのロジックは含まれていません。エントリーファイルを自身で作成する必要があります。このエントリーファイルで、addEventListener()メソッドを呼び出して fetchイベントをレッスンし、jwt.jsのメソッドをコールバック関数として設定します。例えば、ユーザーからのリクエスト内のJWTを検証する必要がある場合、fetchイベントをリッスンしてユーザーからのリクエストからJWTを取得し、その後検証することができます：</div>


   * <div data-tips="true" data-tips-type="warning">HS256 JWTの場合：<code>verifyHS256()</code>を呼び出してJWTを検証します。</div>


   * <div data-tips="true" data-tips-type="warning">RS256 JWTの場合：<code>keyRS256()</code>を呼び出して公開鍵を取得し、その後<code>verifyRS256()</code>を呼び出してJWTを検証します。</div>



この例には複数の.jsファイルが含まれています。


* util.js：以下のメソッドを実装しています：

   * `bin2hex()`：ArrayBufferまたはUint8Arrayを16進数文字列に変換します。

   * `hex2bin()`：16進数文字列をUint8Arrayに変換します。

   * `base64URLEncode()`：Base64URLエンコーディングを行います。

   * `base64URLDecode()`：Base64URLデコーディングを行います。

   * `ab2binstr()`：ArrayBufferをバイナリ文字列に変換します。

   * `binstr2ab()`：バイナリ文字列をArrayBufferに変換します。

* jwt.js：以下のメソッドを実装しています：

   * `signHS256()`：HMAC SHA256アルゴリズム（JWTでは"HS256"）を使用してJWT署名を実装します。HMACは対称暗号化なので、署名と検証に同じ鍵が使用されます。

   * `verifyHS256()`：HMAC SHA256アルゴリズム（JWTでは"HS256"）を使用してJWT検証を実装します。HMACは対称暗号化なので、署名と検証に同じ鍵が使用されます。

   * `signRS256()`：RSASSA\-PKCS1\-v1_5およびSHA\-256アルゴリズム（JWTでは"RS256"）を使用してJWT署名を実装します。

   * `verifyRS256()`：RSASSA\-PKCS1\-v1_5およびSHA\-256アルゴリズム（JWTでは"RS256"）を使用してJWT検証を実装します。

   * `keyRS256()`：RSA公開鍵または秘密鍵を取得します。RSASSA\-PKCS1\-v1_5は非対称暗号化なので、署名には秘密鍵が使用され、検証には公開鍵が使用されます。


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


<span id="関連するランタイムapi"></span>
## 関連するランタイムAPI


* [importKey()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-importKey-exportKey-generateKey-jp)

* [sign()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-sign-verify-jp)

* [verify()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-sign-verify-jp)
