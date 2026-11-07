---
title: "驗證Token的HMAC-SHA256 簽章"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-hmac-auth-zh-tw"
---

本示例展示如何驗證使用者請求的 URL 中嵌入的 Token 之 HMAC\-SHA256 簽章。

本示例中的 Token 由 exp、acl、id、data、hmac 等欄位依序透過波浪號（~）拼接後經 URL 編碼組成。各欄位說明如下：


* id：Session ID。為 ASCII 字串。本示例值為 `01HZE*****AE07WYXHX`

* exp：Session 過期時間。為 UNIX 時間戳記。本示例值為 `1667845428`

* acl：URL 過濾規則，用於匹配 URL 路徑與查詢參數。路徑與參數需以萬用字元（\*）結尾。可設定多組 acl，以驚嘆號（!）分隔。本示例值為 `/folder/file/*?foo=bar*`

* data：附加資料。本示例值為 `baz=qux`

* hmac：exp/acl/id/data 欄位之簽章。本示例值為 `5209d813a04f162f*************243b4dbad2edbe8f5c1d`。產生方式為：

   1. 將 exp/acl/id/data 欄位依序用波浪號（~）拼接

   2. 使用 HMAC 金鑰透過 HMAC\-SHA256 簽章演算法生成簽章


例如使用者請求 URL 為 `https://www.example.com/folder/file?foo=bar`，嵌入 Token 後的 URL 為：

`https://www.example.com/__token__exp%3D1667845428~acl%3D%2Ffolder%2Ffile%2F*%3Ffoo%3Dbar*~id%3D01HZE*****AE07WYXHX~data%3Dbaz%3Dqux~hmac%3D5209d813a04f162f*************243b4dbad2edbe8f5c1d/folder/file?foo=bar`，該 Token 透過 HMAC\-SHA256 簽章確保請求有效性。

函式驗證 Token 簽章流程如下：


1. 取得 URL 中 Token 並 URL 解碼，獲得 `exp=1667845428~acl=/folder/file/*?foo=bar*~id=01HZE*****AE07WYXHX~data=baz=qux~hmac=3D5209d813a04f162f*************243b4dbad2edbe8f5c1d`

2. 提取 hmac 欄位外的內容 `exp=1667845428~acl=/folder/file/*?foo=bar*~id=01HZE*****AE07WYXHX~data=baz=qux~`，使用 HMAC 金鑰計算簽章

3. 比對計算簽章與 hmac 欄位

   * 相符則繼續

   * 不符則返回 403 錯誤（TOKEN_INVALID）

4. 檢查 Token 是否包含 id 欄位

   * 存在則繼續

   * 不存在則返回 403 錯誤（TOKEN_INVALID）

5. 驗證 exp 時間是否未過期

   * 未過期則繼續

   * 已過期則返回 403 錯誤（TOKEN_EXPIRED）

6. 解析 acl 欄位並用驚嘆號（!）分割，逐一比對 URL 路徑與參數

   * 任一規則匹配則驗證成功

   * 全不匹配則返回 403 錯誤（TOKEN_INVALID）


```JavaScript
// HMAC 金鑰
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

  // [0] 导入金鑰
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

  // [1] 簽章
  const sigBuffer = await crypto.subtle.sign(
    "HMAC",
    keyBuffer,
    msg
  );

  // [2] 轉換為 16 進位
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
    // 驗證簽章
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
    // 驗證過期時間
    const exp = parseInt(attr.exp);
    const now = Math.floor(Date.now()/1000);
    if (now > exp) {
      return invalidResponse(403, JSON.stringify({
        reason: 'TOKEN_EXPIRED',
      }));
    }
    // 驗證 Session ID
    if (!attr.id) {
      return invalidResponse(403, JSON.stringify({
        reason: 'TOKEN_INVALID',
      }));
    }
    // 驗證 ACL
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
    // 驗證成功
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


<span id="相關執行時-api"></span>
## 相關執行時 API


* [addEventListener() 方法](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-addEventListener-cn-zh-tw)

* [FetchEvent 介面](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-FetchEvent-cn-zh-tw)

* [Response 介面](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Response-cn-zh-tw)

* [sign() 方法](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-sign-verify-cn-zh-tw)

* [verify() 方法](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-sign-verify-cn-zh-tw)
