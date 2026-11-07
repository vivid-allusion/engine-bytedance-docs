---
title: "CORS 请求代理"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-CORS-cn"
---

该示例展示了如何将 CORS 响应头添加到第三方 API 的响应中。

浏览器在渲染网站的 HTML 页面时，会运行 JavaScript 调用第三方 API 获取 HTML 页面的动态内容。浏览器一般会遵循同源策略（same\-origin policy），不允许跨域请求（cross\-origin request）。如果网站与第三方 API 的来源（Origin）不同，您可以在第三方 API 的响应中添加 CORS 响应头，允许跨域请求。

```JavaScript
addEventListener('fetch', event => {
  const request = event.request
  const url = new URL(request.url)
  if (url.pathname.startsWith(PROXY_ENDPOINT)) {
    // 处理OPTIONS方法
    if (request.method === 'OPTIONS') {
      event.respondWith(handleOptions(request));
    } else if (
        //  处理跨域请求
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
    <h1>API GET without CORS Proxy</h1>
    <a target="_blank" href="https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch#Checking_that_the_fetch_was_successful">Shows TypeError: Failed to fetch since CORS is misconfigured</a>
    <p id="noproxy-status"/>
    <code id="noproxy">Waiting</code>
    <h1>API GET with CORS Proxy</h1>
    <p id="proxy-status"/>
    <code id="proxy">Waiting</code>
    <h1>API POST with CORS Proxy + Preflight</h1>
    <p id="proxypreflight-status"/>
    <code id="proxypreflight">Waiting</code>
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
    return new Response('invalid url, require apiurl', {status: 403});
  }

  request = new Request(apiUrl, request);
  request.headers.set('Origin', new URL(apiUrl).origin);

  let response = await fetch(request);

  // 重新创建回复到浏览器的回复
  response = new Response(response.body, response);

  // 增加跨域头
  response.headers.set('Access-Control-Allow-Origin', url.origin);

  return response
}

function handleOptions(request) {
  // 处理跨域请求的HEAD方法
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


<span id="相关运行时-api"></span>
## 相关运行时 API


* [addEventListener() 方法](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-addEventListener-cn)

* [FetchEvent 接口](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-FetchEvent-cn)

* [Response 接口](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Response-cn)
