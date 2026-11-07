---
title: "Accelerate Website by Deferring JavaScript Loading"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/Accelerate_Website_by_Deferring_JavaScript_Loading"
---

This example demonstrates how to accelerate a website by implementing delayed loading of JavaScript.

The function modifies the type attribute of `<script>` tags in the website's pages to a non\-standard value. When the browser encounters a `<script>` tag with a type attribute value that is not a standard JavaScript MIME type, it ignores the .js file within the tag.

At the same time, the function injects a new `<script>` tag into the website's page. This tag references an external .js file and is set with the defer attribute. This external .js file will restore the type attribute of all `<script>` tags to the standard value after the website page has finished loading, allowing these .js files to start loading.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This external .js file is provided only as an example. Edge Functions are not responsible for maintaining this .js file. You need to implement the relevant logic yourself in a production environment.</div>


Therefore, on the user's browser side, the content of the website page (such as text, images, etc.) will be loaded and rendered first. JavaScript will be loaded after this content has been rendered. For users, the loading speed of the website will become faster.

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


<span id="related-runtime-apis"></span>
## Related runtime APIs


* [addEventListener()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-addEventListener)

* [FetchEvent](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-FetchEvent)

* [Request](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Request)

* [Response](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Response)

* [Headers](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Headers)

* [fetch()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-fetch)

* [createHtmlStream()](https://docs.byteplus.com/en/docs/byteplus-cdn/function-createHtmlStream)
