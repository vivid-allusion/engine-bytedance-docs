---
title: "根據Cookie繞過CDN快取"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-bypass-cache-zh-tw"
---

本示例展示如何根據 Cookie 略過 CDN 快取。

若使用者請求中的 Cookie 存在符合指定正規表示式的 key，來源伺服器返回響應時會新增非標準標頭（如本示例的 `cache-bypass":"true"`），表示該響應需略過 CDN 快取。您需[提交工單](https://console.byteplus.com/workorder/create)與我們協商有效的非標準標頭。BytePlus CDN 不會快取帶有此類標頭的響應。

```JavaScript
// 在此設定正規表示式
// 星號（*）代表左側符號出現零次或多次，例如 wordpress_logged_in_* 代表底線（_）出現零次或多次
// 點號（.）代表任意字元出現零次或多次
const PATTERN=new RegExp("wordpress_logged_in_.*");

// 一般情況下瀏覽器不會包含重複 Cookie 標頭，程式碼可透過 request.headers.get("cookie") 取得
// Cookie 鍵值對以分號（;）分隔
function parseCookie(header) {
  let cookies = {};
  const cookieString = header.get("cookie");
  if (cookieString) {
    cookieString.split(';').forEach(function(cookie) {
      let parts = cookie.split('=');
      let key = parts.shift().trim();
      let value = decodeURIComponent(parts.join('='));
      cookies[key] = value;
    });
  }
  return cookies;
}

function shouldBypassCache(cookies) {
  for (const key of Object.keys(cookies)) {
    if (key.match(PATTERN)) {
      return key;
    }
  }
  return undefined;
}

async function handle(event) {
  const request = event.request;
  const headers  = request.headers;
  const cookies = parseCookie(headers);
  let bypass = shouldBypassCache(cookies);
  if (bypass !== undefined) {
    console.error(`KEY:${bypass} 符合條件，已略過CDN快取`);
    // 本示例標頭僅供展示，實際需透過工單協商有效標頭
    request.headers.append("cache-bypass", "true");
  }
  const resp = await fetch(request);
  return resp;
}

addEventListener('fetch', (event) => {
  event.respondWith(handle(event));
});
```


<span id="相關執行時-api"></span>
## 相關執行時 API


* [addEventListener() 方法](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-addEventListener-cn-zh-tw)

* [FetchEvent 介面](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-FetchEvent-cn-zh-tw)

* [Request 介面](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Request-cn-zh-tw)

* [Headers 介面](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Headers-cn-zh-tw)

* [fetch() 方法](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-fetch-cn-zh-tw)
