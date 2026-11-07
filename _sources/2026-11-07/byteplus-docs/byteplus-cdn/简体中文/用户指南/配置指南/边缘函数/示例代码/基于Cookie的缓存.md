---
title: "基于Cookie的缓存"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cookie-based-caching"
---

本示例展示了如何根据 Cookie 向用户请求添加自定义查询参数，实现基于 Cookie 的缓存。

BytePlus CDN 能根据查询参数区分缓存文件，因此可以实现基于设备类型的缓存。关于查询参数在 CDN 缓存机制中的作用，请参见 [缓存键值](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-cache-keys-cn)。

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
  // 在这里添加您的兜底逻辑
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


<span id="相关运行时api"></span>
## 相关运行时API


* [addEventListener() 方法](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-addEventListener-cn)

* [FetchEvent 接口](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-FetchEvent-cn)

* [Request 接口](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Request-cn)

* [Headers 接口](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Headers-cn)

* [fetch() 方法](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-fetch-cn)
