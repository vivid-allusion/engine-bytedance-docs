---
title: "根据Cookie绕过CDN缓存"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-bypass-cache"
---

本示例展示了如何根据 Cookie 绕过 CDN 缓存。

如果用户请求中的 Cookie 存在一个匹配您指定的正则表达式的 key，源站返回响应时，该响应会被添加一个非标准请求头（例如本示例中的 `cache-bypass":"true"`），用于表示当前响应需要绕过 CDN 缓存。您需要 [提交工单](https://console.byteplus.com/workorder/create) 联系我们协商一个有效的非标准请求头。BytePlus CDN 不会缓存带有该非标准请求头的响应。

```JavaScript
// 在这里设置正则表达式
// 星号（*）代表其左侧的符号出现零次或多次，例如 wordpress_logged_in_* 代表下划线（_）出现零次或多次。
// 点（.）代表任何符号出现零次或多次
const PATTERN=new RegExp("wordpress_logged_in_.*");

// 一般情况下，浏览器不会在请求中包含多个重复的 Cookie 请求头。因此，代码可以通过 request.headers.get("cookie") 获取Cookie 请求头。
// Cookie 的键值对通过分号（:）分隔
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
    console.error(`KEY:${bypass} matched, cdn cache bypassed`);
    // 本示例中的非标准请求头 `cache-bypass":"true"` 仅作为展示。
    // 您需要提交工单联系我们协商一个有效的非标准请求头，用于绕过 CDN 缓存。
    request.headers.append("cache-bypass", "true");
  }
  const resp = await fetch(request);
  return resp;
}

addEventListener('fetch', (event) => {
  event.respondWith(handle(event));
});
```


<span id="相关运行时api"></span>
## 相关运行时API


* [addEventListener() 方法](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-addEventListener-cn)

* [FetchEvent 接口](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-FetchEvent-cn)

* [Request 接口](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Request-cn)

* [Headers 接口](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Headers-cn)

* [fetch() 方法](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-fetch-cn)
