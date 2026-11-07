---
title: "將HTTP重新導向至HTTPS"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/redirect-http-to-https-zh-tw"
---

本示例展示如何將使用者請求使用的 HTTP 協定重新導向為 HTTPS 協定。

```JavaScript
addEventListener("fetch", (event) => {
  event.respondWith(upgradeToSSL(event));
});

// 定義非同步函式用於將HTTP重新導向為HTTPS
async function upgradeToSSL(event) {
  // 取得傳入請求物件
  const incomingRequest = event.request;
  // 解析請求的URL
  const url = new URL(incomingRequest.url);

  // 檢查請求所使用的協定是否為HTTP
  if (url.protocol == 'http:') {
    // 若是HTTP協定，則將協定變更為HTTPS
    url.protocol = 'https';
    // 發送新請求至HTTPS位址，原始請求中協定以外的部分正常透傳
    return fetch(url.toString(), {
      method: incomingRequest.method,
      headers: incomingRequest.headers,
      body: incomingRequest.body
    });
  } else {
    // 若是HTTPS協定，則直接發送原始請求
    return fetch(incomingRequest);
  }
}
```


<span id="相關執行時-api"></span>
## 相關執行時 API


* [addEventListener() 方法](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-addEventListener-cn-zh-tw)

* [FetchEvent 介面](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-FetchEvent-cn-zh-tw)

* [Response 介面](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Response-cn-zh-tw)

* [fetch() 方法](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-fetch-cn-zh-tw)
