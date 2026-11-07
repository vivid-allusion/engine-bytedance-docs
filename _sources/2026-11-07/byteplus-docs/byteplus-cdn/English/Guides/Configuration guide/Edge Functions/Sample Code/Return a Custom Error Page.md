---
title: "Return a Custom Error Page"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-HTML-rendering"
---

This example demonstrates how to generate a custom error page based on the HTTP status code returned by the origin server and return this page to the user.

```JavaScript
const htmlResponse = `
<html>
  <head>Error Page</head>
  <body>The server is experiencing a small hiccup. Please try again later.</body>
</html>
`;

addEventListener('fetch', (event) => {
  event.respondWith(handleResponse(event));
});

function isErrorStatus(st) {
  return st >= 500;
}

async function handleResponse(event) {
  const response = await fetch(event.request);

  // If the origin server returns a status code >= 500, we return a custom error page.
  // Otherwise, we return the information from the origin server.
  if (isErrorStatus(response.status)) {
    return htmlResponse;
  } else {
    return response;
  }
}
```


<span id="related-runtime-apis"></span>
## Related runtime APIs


* [addEventListener()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-addEventListener)

* [FetchEvent](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-FetchEvent)

* [Response](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Response)

* [fetch()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-fetch)
