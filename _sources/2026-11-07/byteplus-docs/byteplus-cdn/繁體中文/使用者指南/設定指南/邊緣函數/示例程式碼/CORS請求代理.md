---
title: "CORS請求代理"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-CORS-cn-zh-tw"
---

本示例展示如何將 CORS 回應標頭新增至第三方 API 的回應中。

瀏覽器在渲染網站的 HTML 頁面時，會執行 JavaScript 呼叫第三方 API 取得 HTML 頁面的動態內容。瀏覽器通常會遵循同源政策（same\-origin policy），不允許跨來源請求（cross\-origin request）。若網站與第三方 API 的來源（Origin）不同，您可以在第三方 API 的回應中新增 CORS 回應標頭，允許跨來源請求。

```JavaScript
addEventListener('fetch', event => {
  const request = event.request
  const url = new URL(request.url)
  if (url.pathname.startsWith(PROXY_ENDPOINT)) {
    // 處理OPTIONS方法
    if (request.method === 'OPTIONS') {
      event.respondWith(handleOptions(request));
    } else if (
        //  處理跨來源請求
        request.method === 'GET' || request.method === 'HEAD' ||
        request.method === 'POST') {
      event.respondWith(handleRequest(request));
    } else {
      event.respondWith(
          new Response(null, {
            status: 405,
            statusText: 'Method Not Allowed',
          }),
      );
    }
  }
  else {
    event.respondWith(rawHtmlResponse(DEMO_PAGE));
  }
})

const corsHeaders = {
  'Access-Control-Allow-Origin': '*',
  'Access-Control-Allow-Methods': 'GET,HEAD,POST,OPTIONS',
  'Access-Control-Max-Age': '86400',
};

const PROXY_ENDPOINT = '/corsproxy/'

function rawHtmlResponse(html) {
  return new Response(html, {
    headers: {
      'content-type': 'text/html;charset=UTF-8',
    },
  });
}

const DEMO_PAGE = `
  <!DOCTYPE html>
  <html>
  <body>
    <h1>未使用CORS代理的API GET請求</h1>
    <a target="_blank" href="https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch#Checking_that_the_fetch_was_successful">顯示TypeError: 因CORS配置錯誤導致請求失敗</a>
    <p id="noproxy-status"/>
    <code id="noproxy">等待中</code>
    <h1>使用CORS代理的API GET請求</h1>
    <p id="proxy-status"/>
    <code id="proxy">等待中</code>
    <h1>使用CORS代理+預檢請求的API POST請求</h1>
    <p id="proxypreflight-status"/>
    <code id="proxypreflight">等待中</code>
    <script>
    let reqs = {};
    reqs.noproxy = () => {
      return fetch("${API_URL}").then(r => r.json())
    }
    reqs.proxy = async () => {
      let href = "${PROXY_ENDPOINT}?apiurl=${API_URL}"
      return fetch(window.location.origin + href).then(r => r.json())
    }
    reqs.proxypreflight = async () => {
      let href = "${PROXY_ENDPOINT}?apiurl=${API_URL}"
      let response = await fetch(window.location.origin + href, {
        method: "POST",
        headers: {
          "Content-Type": "application/json"
        },
        body: JSON.stringify({
          msg: "Hello world!"
        })
      })
      return response.json()
    }
    (async () => {
      for (const [reqName, req] of Object.entries(reqs)) {
        try {
          let data = await req()
          document.getElementById(reqName).innerHTML = JSON.stringify(data)
        } catch (e) {
          document.getElementById(reqName).innerHTML = e
        }
      }
    })()
    </script>
  </body>
  </html>`

async function handleRequest(request) {
  const url = new URL(request.url);
  let apiUrl = url.searchParams.get('apiurl');

  if (apiUrl == null) {
    return new Response('無效網址，需提供apiurl參數', {status: 403});
  }

  request = new Request(apiUrl, request);
  request.headers.set('Origin', new URL(apiUrl).origin);

  let response = await fetch(request);

  // 重新建立回傳至瀏覽器的回應
  response = new Response(response.body, response);

  // 新增跨來源標頭
  response.headers.set('Access-Control-Allow-Origin', url.origin);

  return response
}

function handleOptions(request) {
  // 處理跨來源請求的預檢方法
  let headers = request.headers;
  if (headers.get('Origin') !== null &&
      headers.get('Access-Control-Request-Method') !== null &&
      headers.get('Access-Control-Request-Headers') !== null) {
    let respHeaders = {
      ...corsHeaders,
      'Access-Control-Allow-Headers':
          request.headers.get('Access-Control-Request-Headers'),
    };

    return new Response(null, {
      headers: respHeaders,
    });
  } else {
    return new Response(null, {
      headers: {
        Allow: 'GET, HEAD, POST, OPTIONS',
      },
    });
  }
}
```


<span id="相關執行時-api"></span>
## 相關執行時 API


* [addEventListener() 方法](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-addEventListener-cn-zh-tw)

* [FetchEvent 介面](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-FetchEvent-cn-zh-tw)

* [Response 介面](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Response-cn-zh-tw)
