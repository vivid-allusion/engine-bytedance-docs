---
title: "Bypass CDN Cache Based on Cookie"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/Bypass_CDN_Cache_Based_on_Cookie"
---

This example demonstrates how to bypass the CDN cache based on a Cookie.

If a key in the user's request Cookie matches a regular expression you specify, when the origin server returns a response, a non\-standard request header (for example, `cache-bypass":"true"` in this example) will be added to the response to indicate that the current response needs to bypass the CDN cache. You need to [submit a ticket](https://console.byteplus.com/workorder/create) to contact us and negotiate a non\-standard request header. BytePlus CDN will not cache responses with this non\-standard request header.

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


<span id="related-runtime-apis"></span>
## Related runtime APIs


* [addEventListener()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-addEventListener)

* [FetchEvent](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-FetchEvent)

* [Request](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Request)

* [Headers](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Headers)

* [fetch()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-fetch)
