---
title: "JavaScriptの遅延読み込みによるウェブサイトの高速化"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/accelerate-by-defer-js-jp"
---

この例は、JavaScriptの遅延読み込みを実装することでウェブサイトを高速化する方法を示しています。

この関数は、ウェブサイトのページ内の`<script>`タグのtype属性を非標準の値に変更します。ブラウザが標準的なJavaScript MIMEタイプではないtype属性値を持つ`<script>`タグに遭遇すると、そのタグ内の.jsファイルを無視します。

同時に、この関数はウェブサイトのページに新しい`<script>`タグを挿入します。このタグは外部の.jsファイルを参照し、defer属性が設定されています。この外部.jsファイルは、ウェブサイトページの読み込みが完了した後、すべての`<script>`タグのtype属性を標準値に戻し、これらの.jsファイルの読み込みを開始できるようにします。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">この外部.jsファイルは例としてのみ提供されています。エッジ関数はこの.jsファイルのメンテナンスに責任を負いません。本番環境では、関連するロジックを自身で実装する必要があります。</div>


したがって、ユーザーのブラウザ側では、ウェブサイトページのコンテンツ（テキストや画像など）が最初に読み込まれてレンダリングされます。JavaScriptはこのコンテンツがレンダリングされた後に読み込まれます。ユーザーにとっては、ウェブサイトの読み込み速度が速くなります。

```JavaScript
const INFO_HEADER = "x-bdcdn-accelerator";

const PREFIX = `${generateRandomString(24)}-`;

// This external .js file is provided only as an example. Edge Functions are not responsible for maintaining this .js file. 
// You need to implement the relevant logic yourself in a production environment.
const SDKURL =
  "https://sf16-sg.tiktokcdn.com/obj/eden-sg/nuhpsvhpebf/test/main.js";

const SCRIPT_TYPES = [
  "application/ecmascript",
  "application/javascript",
  "application/x-ecmascript",
  "application/x-javascript",
  "text/ecmascript",
  "text/javascript",
  "text/javascript1.0",
  "text/javascript1.1",
  "text/javascript1.2",
  "text/javascript1.3",
  "text/javascript1.4",
  "text/javascript1.5",
  "text/jscript",
  "text/livescript",
  "text/x-ecmascript",
  "text/x-javascript",
  "module",
];

// Possbile content type for html
//
// [0] text/html
// [1] text/html; charset=UTF-8
// [2] application/html
// [3] application/xhtml+xml
// [4] text/plain (sometimes this is possible)
const HTML_MIMETYPE = [
  "text/html",
  "application/html",
  "application/xhtml+xml",
  "text/plain",
];

function generateRandomString(length) {
  let result = "";
  const characters =
    "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789";

  for (let i = 0; i < length; i++) {
    const randomIndex = Math.floor(Math.random() * characters.length);
    result += characters.charAt(randomIndex);
  }

  return result;
}

function isHTMLMimeType(contentType) {
  if (typeof contentType == "string") {
    return HTML_MIMETYPE.some((item) => contentType.includes(item));
  }
  return false;
}

function isRelativeDomain(domain) {
  if (domain.startsWith("/") && !domain.startsWith("//")) {
    return true;
  }
  return false;
}

async function handleRequest(event) {
  const request = event.request;
  const resp = await fetch(request);

  if (resp.status != 200) {
    console.error(`bypass, response status code is ${resp.status}`);
    resp.headers.set(INFO_HEADER, "status");
    return resp;
  }

  const contentType = resp.headers.get("content-type");
  if (!isHTMLMimeType(contentType)) {
    console.error(`bypass, response mimetype is ${contentType}`);
    resp.headers.set(INFO_HEADER, "mimetype");
    return resp;
  }

  const htmlStream = createHtmlStream(resp.body, undefined, [
    [
      "script",
      {
        onElement(element) {
          const src = element.getAttribute("src");
          const type = element.getAttribute("type") || "text/javascript";
          if(!src||
            (src && isRelativeDomain(src)) ||
            (src && SCRIPT_TYPES.includes(type))
         ) {
           element.setAttribute(
             "type",
             `${PREFIX}${type || "text/javascript"}`,
           );
         }
        },
      },
    ],
    [
      "body",
      {
        onElement(body) {
          body.after(
            `<script
                src="${SDKURL}"
                data-pt-config="${PREFIX}|24"
                crossorigin="anonymous"
                defer>
              </script>`,
            { isHtml: true },
          );
        },
      },
    ],
  ]);

  resp.headers.delete("content-length");
  resp.headers.set(INFO_HEADER, "v16");
  return new Response(htmlStream, {
    status: 200,
    headers: resp.headers,
  });
}

addEventListener('fetch', (event) => {
  event.respondWith(handleRequest(event));
});

```


<span id="関連するランタイムapi"></span>
## 関連するランタイムAPI


* [addEventListener()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-addEventListener-jp)

* [FetchEvent](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-FetchEvent-jp)

* [Request](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Request-jp)

* [Response](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Response-jp)

* [Headers](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Headers-jp)

* [fetch()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-fetch-jp)

* [createHtmlStream()](https://docs.byteplus.com/en/docs/byteplus-cdn/function-createHtmlStream-jp)
