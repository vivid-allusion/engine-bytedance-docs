---
title: "通过延迟加载JavaScript实现网站加速"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/accelerate-by-defer-js"
---

本示例展示了如何通过延迟加载 JavaScript 实现网站加速。

函数把网站页面中 `<script>` 标签的 type 属性修改为一个非标准值。当浏览器遇到 `type` 属性值不是标准 JavaScript MIME 类型的 `<script>` 标签时，会忽略标签中的 .js 文件。

同时，函数向网站页面注入一个新的 `<script>` 标签。该标签引用一个外部的 .js 文件并被设置了 defer 属性。这个外部的 .js 文件会在网站页面加载完成后，把所有`<script>` 标签的 type 属性恢复为标准值，使这些 .js 文件开始加载。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">该外部 .js 文件仅作为示例。边缘函数不负责维护该 .js 文件。您在生产环境需要自行实现相关逻辑。</div>


因此，在用户的浏览器侧，网站页面的内容（例如文本、图片等）会首先被加载并渲染。JavaScript 会在这些内容渲染完成后再加载。对于用户来说，网站的加载速度会变快。

<span id="示例代码"></span>
## 示例代码

```JavaScript
const INFO_HEADER = "x-bdcdn-accelerator";

const PREFIX = `${generateRandomString(24)}-`;

// 该外部 .js 文件仅作为示例。边缘函数不负责维护该 .js 文件。您在生产环境需要自行实现相关逻辑。
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


<span id="相关运行时api"></span>
## 相关运行时API


* [addEventListener() 方法](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-addEventListener-cn)

* [FetchEvent 接口](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-FetchEvent-cn)

* [Request 接口](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Request-cn)

* [Response 接口](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Response-cn)

* [Headers 接口](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Headers-cn)

* [fetch() 方法](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-fetch-cn)

* [createHtmlStream() 方法](https://docs.byteplus.com/en/docs/byteplus-cdn/HtmlStream)
