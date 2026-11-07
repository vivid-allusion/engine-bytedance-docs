---
title: "透過延遲載入JavaScript實現網站加速"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/accelerate-by-defer-js-zh-tw"
---

本示例展示如何透過延遲載入 JavaScript 實現網站加速。

函式會將網頁中的 `<script>` 標籤 type 屬性修改為非標準值。當瀏覽器遇到 type 屬性非標準 JavaScript MIME 類型的 `<script>` 標籤時，會忽略其中的 .js 檔案。

同時函式會注入新的 `<script>` 標籤，引用外部 .js 檔案並設定 defer 屬性。此外部 .js 檔案會在網頁載入完成後，將所有 `<script>` 標籤的 type 屬性恢復為標準值，觸發 .js 檔案載入。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">此處外部 .js 檔案僅為示例，邊緣函式不負責維護。實際生產環境需自行實作相關邏輯。</div>


在瀏覽器端，網頁內容(文字、圖片等)會優先載入並渲染，JavaScript 將在內容渲染完成後載入。對使用者而言，可感受到網站載入速度提升。

<span id="示例程式碼"></span>
## 示例程式碼

```JavaScript
const INFO_HEADER = "x-bdcdn-accelerator";

const PREFIX = `${generateRandomString(24)}-`;

// 此外部 .js 檔案僅為示例，邊緣函數不負責維護。實際生產環境需自行實作相關邏輯。
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


<span id="相關執行時-api"></span>
## 相關執行時 API


* [addEventListener() 方法](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-addEventListener-cn-zh-tw)

* [FetchEvent 介面](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-FetchEvent-cn-zh-tw)

* [Request 介面](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Request-cn-zh-tw)

* [Response 介面](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Response-cn-zh-tw)

* [Headers 介面](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Headers-cn-zh-tw)

* [fetch() 方法](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-fetch-cn-zh-tw)

* [createHtmlStream() 方法](https://docs.byteplus.com/en/docs/byteplus-cdn/HtmlStream-zh-tw)
