---
title: "CORSプロキシ"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-CORS-jp"
---

この例は、サードパーティAPIからのレスポンスにCORSレスポンスヘッダーを追加する方法を示しています。

ブラウザがウェブサイトのHTMLページをレンダリングする際、JavaScriptを実行してサードパーティAPIを呼び出し、HTMLページの動的コンテンツを取得します。ブラウザは一般的に同一オリジンポリシーに従い、クロスオリジンリクエストを許可しません。あなたのウェブサイトのオリジンがサードパーティAPIのオリジンと異なる場合、サードパーティAPIからのレスポンスにCORSレスポンスヘッダーを追加することで、クロスオリジンリクエストを許可することができます。

```JavaScript
addEventListener('fetch', event => {
  const request = event.request
  const url = new URL(request.url)
  if (url.pathname.startsWith(PROXY_ENDPOINT)) {
    // Handle OPTIONS requests
    if (request.method === 'OPTIONS') {
      event.respondWith(handleOptions(request));
    } else if (
        //  Handle cross-origin requests
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

  // Create a response
  response = new Response(response.body, response);

  // Add CORS header
  response.headers.set('Access-Control-Allow-Origin', url.origin);

  return response
}

function handleOptions(request) {
  // handle the HEAD requests
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


<span id="関連するランタイムapi"></span>
## 関連するランタイムAPI


* [addEventListener()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-addEventListener-jp)

* [FetchEvent](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-FetchEvent-jp)

* [Response](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Response-jp)
