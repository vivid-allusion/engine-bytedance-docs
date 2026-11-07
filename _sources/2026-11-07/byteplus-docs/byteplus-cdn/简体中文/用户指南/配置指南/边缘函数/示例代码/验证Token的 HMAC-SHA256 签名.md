---
title: "验证Token的 HMAC-SHA256 签名"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-hmac-auth"
---

本示例展示了如何验证用户请求的 URL 中嵌入的 Token 的 HMAC\-SHA256 签名。

本示例中的 Token 是由 exp、acl、id、data、hmac 字段按先后顺序通过波浪号（~）拼接后，经过 URL 编码的字符串。字段的描述如下：


* id：Session ID。是一个 ASCII 码字符串。该字段在本示例中为 `01HZE*****AE07WYXHX`。

* exp：Session 的过期时间。是一个 UNIX 时间戳。该字段在本示例中为 `1667845428`。

* acl：URL 过滤器，用于匹配 URL 的路径和查询参数。路径和查询参数都需要以通配符（\*）结尾。您可以设置多个 acl。多个 acl 之间以感叹号（!）分隔。该字段在本示例中为 `/folder/file/*?foo=bar*`。

* data：附加数据。该字段在本示例中为 `baz=qux`。

* hmac：exp、acl、id、data 字段的签名。该字段在本示例中为 `5209d813a04f162f*************243b4dbad2edbe8f5c1d`。该字段的生成方法为：

   1. 把 exp、acl、id、data 字段按先后顺序通过波浪号（~）拼接。

   2. 基于 HMAC\-SHA256 签名算法，使用 HMAC 密钥对拼接的字符串进行签名。


例如，如果用户请求的 URL 是 `https://www.example.com/folder/file?foo=bar`，则嵌入 Token 后的 URL 是 `https://www.example.com/__token__exp%3D1667845428~acl%3D%2Ffolder%2Ffile%2F*%3Ffoo%3Dbar*~id%3D01HZE*****AE07WYXHX~data%3Dbaz%3Dqux~hmac%3D5209d813a04f162f*************243b4dbad2edbe8f5c1d/folder/file?foo=bar`。该 Token 通过 HMAC\-SHA256 签名保证用户请求的有效性和可靠性。

函数收到用户请求时，验证 Token 的 HMAC 签名的步骤如下：


1. 获取用户请求的 URL 中嵌入的 Token 并进行 URL 解码。结果为 `exp=1667845428~acl=/folder/file/*?foo=bar*~id=01HZE*****AE07WYXHX~data=baz=qux~hmac=3D5209d813a04f162f*************243b4dbad2edbe8f5c1d`

2. 提取除 hmac 字段外的其他部分 `exp=1667845428~acl=/folder/file/*?foo=bar*~id=01HZE*****AE07WYXHX~data=baz=qux~`，并使用 HMAC 密钥计算签名。

3. 验证计算得到的签名是否与 hmac 字段的签名相同。

   * 如果相同，则进行下一步。

   * 如果不同，则 Token 验证失败，向用户返回 403 错误码，原因为 TOKEN_INVALID。

4. 验证 Token 是否包含 id 字段。

   * 如果包含，则进行下一步。

   * 如果不包含，则 Token 验证失败，向用户返回 403 错误码，原因为 TOKEN_INVALID。

5. 提取 Token 中的 exp 字段并验证 exp 字段的时间是否不早于当前时间。

   * 如果不早于当前时间，则进行下一步。

   * 如果早于当前时间，则 Token 验证失败，向用户返回 403 错误码，原因为 TOKEN_EXPIRED。

6. 提取 Token 中的 acl 字段，首先用感叹号（!）分割 acl 字段的内容，并遍历所有 acl 直到任意一个 acl 的 glob 匹配 URL 路径和查询参数。

   * 如果有任意一个 acl 的 glob 匹配 URL 路径和查询参数，则 Token 验证成功。

   * 如果没有任何一个 acl 的 glob 匹配 URL 路径和查询参数，则 Token 验证失败，向用户返回 403 错误码，原因为 TOKEN_INVALID。


```JavaScript
// HMAC 密钥
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

  // [0] 导入密钥
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

  // [1] 签名
  const sigBuffer = await crypto.subtle.sign(
    "HMAC",
    keyBuffer,
    msg
  );

  // [2] 转换为 16 进制
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
    // 验证签名
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
    // 验证过期时间
    const exp = parseInt(attr.exp);
    const now = Math.floor(Date.now()/1000);
    if (now > exp) {
      return invalidResponse(403, JSON.stringify({
        reason: 'TOKEN_EXPIRED',
      }));
    }
    // 验证 Session ID
    if (!attr.id) {
      return invalidResponse(403, JSON.stringify({
        reason: 'TOKEN_INVALID',
      }));
    }
    // 验证 ACL
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
    // 验证成功
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


<span id="相关运行时api"></span>
## 相关运行时API


* [addEventListener() 方法](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-addEventListener-cn)

* [FetchEvent 接口](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-FetchEvent-cn)

* [Response() 方法](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Response-cn)

* [sign() 方法](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-sign-verify-cn)

* [verify() 方法](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-sign-verify-cn)
