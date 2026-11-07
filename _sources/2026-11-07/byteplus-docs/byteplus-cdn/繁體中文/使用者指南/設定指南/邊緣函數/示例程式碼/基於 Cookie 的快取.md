---
title: "基於 Cookie 的快取"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cookie-based-caching-zh-tw"
---

本示例展示如何根據 Cookie 在請求中新增自訂查詢參數，實現基於 Cookie 的快取機制。

BytePlus CDN 能根據查詢參數區分快取檔案，因此可實現基於裝置類型的快取。關於查詢參數在 CDN 快取機制中的作用，請參閱 [快取索引鍵](https://docs.byteplus.com/en/docs/byteplus-cdn/cache-key_zh-tw)。

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
      throw new Error(`標頭 ${hdr} 未找到`);
    }
    out.push(value);
  }
  
  for (const cname of COOKIE_NAME) {
    let value = cookie[cname];
    if (value === undefined) {
      throw new Error(`Cookie ${cname} 未找到`);
    }
    out.push(value);
  }
  
  searchParams.set(CACHE_KEY, out.join(delimiter));
  return url.href;
}

function fallbackProxy(event, msg) {
  // 在此添加您的備援邏輯
  // return new Response(msg, {status: 400});
  // -------------------------------------------------------------------------
  return fetch(event.request);
}

async function doProxy(event) {
  const req = event.request;
  const cookie = req.headers.get('cookie');
  if (!cookie) {
    throw new Error('請求缺少Cookie標頭');
  }
  const cookieMap = parseCookie(cookie);

  const proxyUrl = composeProxyUrl(
      req.url,          
      cookieMap,        
      req.headers,      
      CACHE_KEY_DELIMITER
  );

  console.log(`[代理網址: ${proxyUrl}]`);

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
     console.log(`錯誤: ${e}`);
     return fallbackProxy(event, `${e}`);
  }
}

addEventListener('fetch', (event) => {
  event.respondWith(main(event));
});
```


<span id="相關執行時-api"></span>
## 相關執行時 API


* [addEventListener() 方法](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-addEventListener-cn-zh-tw)

* [FetchEvent 介面](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-FetchEvent-cn-zh-tw)

* [Request 介面](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Request-cn-zh-tw)

* [Headers 介面](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Headers-cn-zh-tw)

* [fetch() 方法](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-fetch-cn-zh-tw)
