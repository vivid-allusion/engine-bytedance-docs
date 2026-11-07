---
title: "JWT Authentication"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/functions_JWT_Authentication"
---

This example demonstrates how to verify a JWT.

<span id="what-is-jwt"></span>
## What is JWT

JWT (JSON Web Token) securely transmits information in the form of a JSON object, as defined in [RFC 7519](https://datatracker.ietf.org/doc/html/rfc7519). A JWT consists of a Header, Payload, and Signature, with each part separated by a dot (.), forming `Header.Payload.Signature`.


* Header: The type of token and the signing algorithm. The Header needs to be Base64URL encoded.

* Payload: The claims of the JWT, including user information or other metadata. The Payload needs to be Base64URL encoded.

* Signature: Used to verify the authenticity of the JWT. The Signature is generated as follows:

   1. Base64URL encode the Header and Payload separately.

   2. Concatenate the encoded Header and Payload with a dot (.).

   3. Sign the resulting string using the digest algorithm specified in the Header and the secret key.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For algorithms using symmetric encryption, such as HS256, the same key is used for both signing and verification.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For algorithms using asymmetric encryption, such as RS256, the private key is used for signing, and the public key is used for verification.   </div>
   

   4. Base64URL encode the signature result from the previous step to obtain the Signature.


Suppose the Header before encoding, the Payload before encoding, and the secret key are as follows:

The Header before encoding is：

```JSON
{
    "typ":"JWT",
    "alg":"HS256"
}
```


The Payload before encoding is:

```JSON
{
    "sub": "1234567890",
    "name": "John Doe",
    "iat": 1516239022,
    "exp": 1516242622,
    "iss": "example.com"
}
```


The key is`my-jwt-secret`. Then Signature is `g50NxVfIcxfsiX_cHbpS_-xQgzvoEc3R5roRzJuXeB4`.

Therefore, JWT is `eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyLCJleHAiOjE1MTYyNDI2MjIsImlzcyI6ImV4YW1wbGUuY29tIn0.g50NxVfIcxfsiX_cHbpS_-xQgzvoEc3R5roRzJuXeB4`.

<span id="jwt-verification-process"></span>
## JWT verification process

The purpose of JWT verification is to ensure that the JWT has not been tampered with and comes from a trusted issuer. Taking HS256 and RS256 as examples, the JWT verification process is as follows:

HS256 JWT verification steps:


1. Obtain the JWT and extract the `Header.Payload` from it.

2. Sign the `Header.Payload` using the HMAC key and SHA\-256 signing algorithm.

3. Compare the calculated signature with the Signature in the JWT.

   * If they are the same, JWT verification succeeds.

   * If they are different, JWT verification fails.


RS256 JWT verification steps:


1. Obtain the JWT and extract the kid from the Header, then use the kid to find the corresponding RSA public key.

2. Extract the Signature from the JWT, Base64Url decode the Signature, and decrypt it using the RSA public key. After decryption, you will get a SHA\-256 digest.

3. Extract the `Header.Payload` from the JWT, and obtain its SHA\-256 digest using SHA\-256.

4. Compare the two SHA\-256 digests.

   * If they are the same, JWT verification succeeds.

   * If they are different, JWT verification fails.


<span id="sample-code"></span>
## Sample code

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">This example includes multiple .js files for demonstration purposes. When editing the function code, you need to bundle all .js files into a single .js file and use the content of the bundled file as the content of default.js. The bundled file must comply with ES6 standards.</div>


* <div data-tips="true" data-tips-type="warning">This example does not include the entry file required for bundling or the logic for listening to fetch events. You need to create an entry file yourself. In this entry file, you call the addEventListener() method to listen for fetch events and set the method from jwt.js as the callback function. For example, if you need to verify the JWT in a user request, you can first obtain the JWT from the user request by calling addEventListener() to listen to the fetch event and then verify the obtained JWT:</div>


   * <div data-tips="true" data-tips-type="warning">For HS256 JWT: Call <code>verifyHS256()</code> to verify the JWT.</div>


   * <div data-tips="true" data-tips-type="warning">For RS256 JWT: Call <code>keyRS256()</code> to obtain the public key, then call <code>verifyRS256()</code> to verify the JWT.</div>



This example includes multiple .js files.


* util.js: Implements the following methods:

   * `bin2hex()`: Converts ArrayBuffer or Uint8Array to a hexadecimal string.

   * `hex2bin()`: Converts a hexadecimal string to Uint8Array.

   * `base64URLEncode()`: Base64URL encoding.

   * `base64URLDecode()`: Base64URL decoding.

   * `ab2binstr()`: Converts ArrayBuffer to a binary string.

   * `binstr2ab()`: Converts a binary string to ArrayBuffer.

* jwt.js: Implements the following methods:

   * `signHS256()`: Implements JWT signing using the HMAC SHA256 algorithm (i.e., "HS256" in JWT). Since HMAC is symmetric encryption, the same key is used for both signing and verification.

   * `verifyHS256()`: Implements JWT verification using the HMAC SHA256 algorithm (i.e., "HS256" in JWT). Since HMAC is symmetric encryption, the same key is used for both signing and verification.

   * `signRS256()`: Implements JWT signing using the RSASSA\-PKCS1\-v1_5 and SHA\-256 algorithms (i.e., "RS256" in JWT).

   * `verifyRS256()`: Implements JWT verification using the RSASSA\-PKCS1\-v1_5 and SHA\-256 algorithms (i.e., "RS256" in JWT).

   * `keyRS256()`: Obtains the RSA public or private key. Since RSASSA\-PKCS1\-v1_5 is asymmetric encryption, the private key is used for signing, and the public key is used for verification.


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


<span id="related-runtime-apis"></span>
## Related runtime APIs


* [importKey()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-importKey-exportKey-generateKey)

* [sign()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-sign-verify)

* [verify()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-sign-verify)
