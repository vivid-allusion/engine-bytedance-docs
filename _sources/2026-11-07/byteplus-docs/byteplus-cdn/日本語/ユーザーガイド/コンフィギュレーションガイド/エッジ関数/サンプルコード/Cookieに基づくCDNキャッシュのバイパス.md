---
title: "Cookieに基づくCDNキャッシュのバイパス"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/Bypass_CDN_Cache_Based_on_Cookie-jp"
---

この例は、Cookieに基づいてCDNキャッシュをバイパスする方法を示しています。

ユーザーのリクエストCookieのキーが指定した正規表現と一致する場合、オリジンサーバーがレスポンスを返す際に、非標準のリクエストヘッダー（この例では`cache-bypass":"true"`）がレスポンスに追加されます。これは、現在のレスポンスがCDNキャッシュをバイパスする必要があることを示します。非標準のリクエストヘッダーについては、[チケットを提出](https://console.byteplus.com/workorder/create)して当社に連絡し、協議する必要があります。BytePlus CDNは、この非標準のリクエストヘッダーを含むレスポンスをキャッシュしません。

```JavaScript
// Set the regular expression here
// The asterisk (*) represents zero or more occurrences of the symbol to its left. For example, wordpress_logged_in_* represents zero or more occurrences of the underscore (_).
// The dot (.) represents zero or more occurrences of any symbol
const PATTERN = new RegExp("wordpress_logged_in_.*");

// Generally, browsers do not include multiple duplicate Cookie request headers in a request. Therefore, the code can obtain the Cookie request header through request.headers.get("cookie").
// Cookie key-value pairs are separated by semicolons (;)
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
  const headers = request.headers;
  const cookies = parseCookie(headers);
  let bypass = shouldBypassCache(cookies);
  if (bypass !== undefined) {
    console.error(`KEY:${bypass} matched, cdn cache bypassed`);
    // The non-standard request header `cache-bypass":"true"` in this example is for demonstration purposes only.
    // You need to submit a ticket to contact us and negotiate a valid non-standard request header for bypassing the CDN cache.
    request.headers.append("cache-bypass", "true");
  }
  const resp = await fetch(request);
  return resp;
}

addEventListener('fetch', (event) => {
  event.respondWith(handle(event));
});
```


<span id="関連するランタイムapi"></span>
## 関連するランタイムAPI


* [addEventListener()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-addEventListener-jp)

* [FetchEvent](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-FetchEvent-jp)

* [Request](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Request-jp)

* [Headers](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Headers-jp)

* [fetch()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-fetch-jp)
