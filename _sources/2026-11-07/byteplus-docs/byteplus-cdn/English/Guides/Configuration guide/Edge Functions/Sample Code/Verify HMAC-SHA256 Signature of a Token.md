---
title: "Verify HMAC-SHA256 Signature of a Token"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/Verify_HMAC-SHA256_Signature_of_a_Token"
---

This example demonstrates how to verify the HMAC\-SHA256 signature of a Token embedded in the URL of a user request.

In this example, the Token is a URL\-encoded string concatenated with tildes (~) in the order of exp, acl, id, data, and hmac fields. The field descriptions are as follows:


* id: Session ID. It's an ASCII string. In this example, it's `01HZE*****AE07WYXHX`.

* exp: Session expiration time. It's a UNIX timestamp. In this example, it's `1667845428`.

* acl: URL filter, used to match URL paths and query parameters. Both paths and query parameters should end with a wildcard (\*). You can set multiple acls. Multiple acls are separated by exclamation marks (!). In this example, it's `/folder/file/*?foo=bar*`.

* data: Additional data. In this example, it's `baz=qux`.

* hmac: Signature of the exp, acl, id, and data fields. In this example, it's `5209d813a04f162f*************243b4dbad2edbe8f5c1d`. This field is generated as follows:

   1. Concatenate the exp, acl, id, and data fields in order using tildes (~).

   2. Sign the concatenated string using the HMAC\-SHA256 signature algorithm with the HMAC key.


For example, if the user's request URL is `https://www.example.com/folder/file?foo=bar`, the URL with the embedded Token would be `https://www.example.com/__token__exp%3D1667845428~acl%3D%2Ffolder%2Ffile%2F*%3Ffoo%3Dbar*~id%3D01HZE*****AE07WYXHX~data%3Dbaz%3Dqux~hmac%3D5209d813a04f162f*************243b4dbad2edbe8f5c1d/folder/file?foo=bar`. This Token ensures the validity and reliability of the user request through HMAC\-SHA256 signature.

When the function receives a user request, it verifies the Token's HMAC signature following these steps:


1. Retrieve the Token embedded in the user request URL and perform URL decoding. The result is `exp=1667845428~acl=/folder/file/*?foo=bar*~id=01HZE*****AE07WYXHX~data=baz=qux~hmac=3D5209d813a04f162f*************243b4dbad2edbe8f5c1d`

2. Extract all parts except the hmac field `exp=1667845428~acl=/folder/file/*?foo=bar*~id=01HZE*****AE07WYXHX~data=baz=qux~`, and calculate the signature using the HMAC key.

3. Verify if the calculated signature matches the signature in the hmac field.

   * If they match, proceed to the next step.

   * If they don't match, Token verification fails, return a 403 error code to the user with the reason TOKEN_INVALID.

4. Verify if the Token contains the id field.

   * If it does, proceed to the next step.

   * If it doesn't, Token verification fails, return a 403 error code to the user with the reason TOKEN_INVALID.

5. Extract the exp field from the Token and verify if the exp time is not earlier than the current time.

   * If it's not earlier, proceed to the next step.

   * If it's earlier, Token verification fails, return a 403 error code to the user with the reason TOKEN_EXPIRED.

6. Extract the acl field from the Token, first split the content of the acl field by exclamation marks (!), and iterate through all acls until any acl's glob matches the URL path and query parameters.

   * If any acl's glob matches the URL path and query parameters, Token verification succeeds.

   * If no acl's glob matches the URL path and query parameters, Token verification fails, return a 403 error code to the user with the reason TOKEN_INVALID.


```JavaScript
// HMAC key
const SECRERT_KEY = 'osiefuoiseufoisejfiurshfouirshou';
const PREFIX = '__token__';
const infoHeaderName = "x-byteplus-faas-info-verify-token"

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

function attrToString(obj) {
  return Object.entries(obj)
    .map(([key, value]) => `${key}=${value}`)
    .join('~');
}
function stringToAttr(str) {
  return str.split('~').reduce((acc, pair) => {
    const [key, ...value] = pair.split('=');
    acc[key] = value?.join('=');
    return acc;
  }, {});
}

function getTokenPart(url){
  return url.pathname.match(/__token__([^/]+)/)[1];
}

function globToRegExp(glob) {
  let regExpStr = glob.replace(/[.+^${}()|[\]\\]/g, '\\$&');
  regExpStr = regExpStr.replace(/\*/g, '.*').replace(/\?/g, '.');
  return new RegExp(`^${regExpStr}$`);
}

function matchGlob(pattern, str) {
  const regExp = globToRegExp(pattern);
  return regExp.test(str);
}

function invalidResponse(statusCode, msg) {
  return new Response(msg, {
    status: statusCode || 403,
    [infoHeaderName]: msg
  });
}

function validResponse() {
  return new Response('Valid token', {
    status: 200,
    [infoHeaderName]: 'Valid token'
  });
}

async function hmacSign(
  hashAlgo,
  secret,
  data
) {
  let enc = new TextEncoder();
  let key = enc.encode(secret);
  let msg = enc.encode(data);

  // [0] Import key
  const keyBuffer = await crypto.subtle.importKey(
    "raw",
    key,
    {
      name: "HMAC",
      hash: {
        name: hashAlgo
      }
    },
    false,
    ["sign"]
  );

  // [1] Sign
  const sigBuffer = await crypto.subtle.sign(
    "HMAC",
    keyBuffer,
    msg
  );

  // [2] Convert to hex
  return bin2hex(sigBuffer)
}

async function hmacVerify(
  hashAlgo,
  key,
  message,
  signature
) {
  const encoder = new TextEncoder();
  const encKey = encoder.encode(key);
  const encMsg = encoder.encode(message);
  const encSig = hex2bin(signature);

  const keyBuf = await crypto.subtle.importKey(
    "raw",
    encKey,
    {
      name: "HMAC",
      hash: {
        name: hashAlgo
      }
    },
    false,
    ["verify"]
  );

  return await crypto.subtle.verify(
    "HMAC",
    keyBuf,
    encSig,
    encMsg
  );
}

async function handleRequest(request) {
  try {
    let url = new URL(request.url);
    const token = getTokenPart(url);
    // Verify signature
    const decodeToken = decodeURIComponent(token);
    const removePrefix = decodeToken.replace(PREFIX, '');
    const obj = stringToAttr(removePrefix);
    const { hmac, ...attr } = obj;
    const authStr = attrToString(attr);
    const hashAuth = await hmacSign('SHA-256', SECRERT_KEY, authStr);
    if (hashAuth !== hmac) {
      return invalidResponse(403, JSON.stringify({
        reason: 'TOKEN_INVALID',
      }));
    }
    // Verify TTL
    const exp = parseInt(attr.exp);
    const now = Math.floor(Date.now()/1000);
    if (now > exp) {
      return invalidResponse(403, JSON.stringify({
        reason: 'TOKEN_EXPIRED',
      }));
    }
    // Verify Session ID
    if (!attr.id) {
      return invalidResponse(403, JSON.stringify({
        reason: 'TOKEN_INVALID',
      }));
    }
    // Verify ACL
    const acl = attr.acl;
    if (!acl) {
      return invalidResponse(403, JSON.stringify({
        reason: 'TOKEN_INVALID',
      }));
    }
    let tag = false;
    const aclArray = acl.split('!');
    for(let i = 0; i < aclArray.length; i++){
      const aclItem = aclArray[i];
      const pathname = url.pathname.replace(`/__token__${token}`, ``);
      const search = url.search;
      const resolvePath = `${pathname}${search}`;
      if(matchGlob(aclItem, resolvePath)){
        tag = true;
        break;
      }

    }
    if(!tag){
      return invalidResponse(403, JSON.stringify({
        reason: `TOKEN_INVALID`,
      }));
    }
    // Verification successful
    return validResponse();

  } catch (error) {
    let msg = "Internal Server Error";
    let error_message = "[JS]";
    if (error instanceof Error) {
      msg = error.message;
    }
    return invalidResponse(500, `ERROR: ${msg}`);
  }
}

addEventListener('fetch', event => {
  event.respondWith(handleRequest(event.request));
})
```


<span id="related-runtime-apis"></span>
## Related runtime APIs


* [addEventListener()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-addEventListener)

* [FetchEvent](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-FetchEvent)

* [Response](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Response)

* [sign()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-sign-verify)

* [verify()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-sign-verify)
