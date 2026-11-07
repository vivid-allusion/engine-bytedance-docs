---
title: "Cookie-based Caching"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/Cookie-based_Caching"
---

This example demonstrates how to add custom query parameters to user requests based on Cookies, implementing Cookie\-based caching.

BytePlus CDN can differentiate cached files based on query parameters, thus enabling device type\-based caching. For information on the role of query parameters in the CDN caching mechanism, please refer to [Cache Key](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-cache-keys).

```JavaScript
const COOKIE_NAME = ["key1", "key2"];
const HEADER_NAME = ["custom-header"];
const CACHE_KEY_DELIMITER = ',';  
const CACHE_KEY  = 'kfc-cachekey';  

function parseCookie(cookieString) {
  let cookies = {};
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

function composeProxyUrl(
    inputUrl,           
    cookie,             
    reqHeader,          
    delimiter          
) {
  const url = new URL(inputUrl);
  const searchParams = url.searchParams;
  let out = [];
  
  for (const hdr of HEADER_NAME) {
    let value = reqHeader.get(hdr);
    if (value === null || value === undefined) {
      throw new Error(`header ${hdr} is not found`);
    }
    out.push(value);
  }
  
  for (const cname of COOKIE_NAME) {
    let value = cookie[cname];
    if (value === undefined) {
      throw new Error(`cookie ${cname} is not found`);
    }
    out.push(value);
  }
  
  searchParams.set(CACHE_KEY, out.join(delimiter));
  return url.href;
}

function fallbackProxy(event, msg) {
  // Implement fallback logic here
  // return new Response(msg, {status: 400});
  // -------------------------------------------------------------------------
  return fetch(event.request);
}

async function doProxy(event) {
  const req = event.request;
  const cookie = req.headers.get('cookie');
  if (!cookie) {
    throw new Error('request does not have cookie header');
  }
  const cookieMap = parseCookie(cookie);

  const proxyUrl = composeProxyUrl(
      req.url,          
      cookieMap,        
      req.headers,      
      CACHE_KEY_DELIMITER
  );

  console.log(`[proxy_url: ${proxyUrl}]`);

  const proxyReq = new Request(
      proxyUrl, 
      {
        method: req.method,    
        headers: req.headers,  
        body: req.body         
      });


  return fetch(proxyReq);
  
}

async function main(event) {
  try {
     return await doProxy(event);
  } catch (e) {
     console.log(`Error: ${e}`);
     return fallbackProxy(event, `${e}`);
  }
}

addEventListener('fetch', (event) => {
  event.respondWith(main(event));
});
```


<span id="related-runtime-apis"></span>
## Related runtime APIs


* [addEventListener()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-addEventListener)

* [FetchEvent](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-FetchEvent)

* [Request](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Request)

* [Headers](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Headers)

* [fetch()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-fetch)
