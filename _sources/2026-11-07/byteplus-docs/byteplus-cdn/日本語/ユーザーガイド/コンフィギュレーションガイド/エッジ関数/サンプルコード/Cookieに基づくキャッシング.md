---
title: "Cookieに基づくキャッシング"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/Cookie-based_Caching-jp"
---

この例は、Cookieに基づいてユーザーリクエストにカスタムクエリパラメータを追加し、Cookieベースのキャッシングを実装する方法を示しています。

BytePlus CDNは、クエリパラメータに基づいてキャッシュされたファイルを区別することができ、これによりデバイスタイプに基づいたキャッシングが可能になります。CDNキャッシングメカニズムにおけるクエリパラメータの役割については、[キャッシュキー](https://docs.byteplus.com/docs/byteplus-cdn/cache-key-jp)を参照してください。

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


<span id="関連するランタイムapi"></span>
## 関連するランタイムAPI


* [addEventListener()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-addEventListener-jp)

* [FetchEvent](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-FetchEvent-jp)

* [Request](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Request-jp)

* [Headers](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Headers-jp)

* [fetch()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-fetch-jp)
