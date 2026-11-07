---
title: "トークンのHMAC-SHA256署名を検証する"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/Verify_HMAC-SHA256_Signature_of_a_Token-jp"
---

この例は、ユーザーからのリクエストのURLに埋め込まれたトークンのHMAC\-SHA256署名を検証する方法を示しています。

この例では、トークンはexp、acl、id、data、hmacフィールドの順にチルダ（~）で連結されたURL encodedされた文字列です。フィールドの説明は以下の通りです：


* id: セッションID。ASCII文字列です。この例では `01HZE*****AE07WYXHX` です。

* exp: セッション有効期限。UNIXタイムスタンプです。この例では `1667845428` です。

* acl: URLフィルター。URLパスとクエリパラメータのマッチングに使用されます。パスとクエリパラメータの両方がワイルドカード（\*）で終わる必要があります。複数のaclを設定できます。複数のaclは感嘆符（!）で区切られます。この例では `/folder/file/*?foo=bar*` です。

* data: 追加データ。この例では `baz=qux` です。

* hmac: exp、acl、id、dataフィールドの署名。この例では `5209d813a04f162f*************243b4dbad2edbe8f5c1d` です。このフィールドは以下のように生成されます：

   1. exp、acl、id、dataフィールドをこの順序でチルダ（~）を使って連結します。

   2. 連結された文字列をHMACキーを使用してHMAC\-SHA256署名アルゴリズムで署名します。


例えば、ユーザーのリクエストURLが `https://www.example.com/folder/file?foo=bar` の場合、トークンが埋め込まれたURLは `https://www.example.com/__token__exp%3D1667845428~acl%3D%2Ffolder%2Ffile%2F*%3Ffoo%3Dbar*~id%3D01HZE*****AE07WYXHX~data%3Dbaz%3Dqux~hmac%3D5209d813a04f162f*************243b4dbad2edbe8f5c1d/folder/file?foo=bar` となります。このトークンはHMAC\-SHA256署名を通じてユーザーからのリクエストの有効性と信頼性を確保します。

関数がユーザーからのリクエストを受け取ると、以下の手順でトークンのHMAC署名を検証します：


1. ユーザーからのリクエストURLに埋め込まれたトークンを取得し、URLデコードを行います。結果は `exp=1667845428~acl=/folder/file/*?foo=bar*~id=01HZE*****AE07WYXHX~data=baz=qux~hmac=3D5209d813a04f162f*************243b4dbad2edbe8f5c1d` となります。

2. hmacフィールドを除くすべての部分 `exp=1667845428~acl=/folder/file/*?foo=bar*~id=01HZE*****AE07WYXHX~data=baz=qux~` を抽出し、HMACキーを使用して署名を計算します。

3. 計算された署名がhmacフィールドの署名と一致するか検証します。

   * 一致する場合、次のステップに進みます。

   * 一致しない場合、トークン検証は失敗し、理由TOKEN_INVALIDとともに403エラーコードをユーザーに返します。

4. トークンにidフィールドが含まれているか検証します。

   * 含まれている場合、次のステップに進みます。

   * 含まれていない場合、トークン検証は失敗し、理由TOKEN_INVALIDとともに403エラーコードをユーザーに返します。

5. トークンからexpフィールドを抽出し、exp時間が現在時刻より早くないか検証します。

   * 早くない場合、次のステップに進みます。

   * 早い場合、トークン検証は失敗し、理由TOKEN_EXPIREDとともに403エラーコードをユーザーに返します。

6. トークンからaclフィールドを抽出し、まずaclフィールドの内容を感嘆符（!）で分割し、いずれかのaclのglobがURLパスとクエリパラメータにマッチするまですべてのaclを反復処理します。

   * いずれかのaclのglobがURLパスとクエリパラメータにマッチする場合、トークン検証は成功します。

   * どのaclのglobもURLパスとクエリパラメータにマッチしない場合、トークン検証は失敗し、理由TOKEN_INVALIDとともに403エラーコードをユーザーに返します。


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
    // Success
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


<span id="関連するランタイムapi"></span>
## 関連するランタイムAPI


* [addEventListener()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-addEventListener-jp)

* [FetchEvent](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-FetchEvent-jp)

* [Response](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Response-jp)

* [sign()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-sign-verify-jp)

* [verify()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-sign-verify-jp)
