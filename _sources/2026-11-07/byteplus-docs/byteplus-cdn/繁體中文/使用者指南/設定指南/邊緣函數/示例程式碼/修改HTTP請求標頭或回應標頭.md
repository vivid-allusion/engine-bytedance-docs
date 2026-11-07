---
title: "修改HTTP請求標頭或回應標頭"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Reverse-proxy-cn-zh-tw"
---

本示例展示如何修改使用者請求中的 HTTP 請求標頭和返回給使用者的響應中的響應標頭。

```JavaScript
addEventListener("fetch", (event) => {
  event.respondWith(handle(event));
});

// 定義非同步函式用於處理fetch請求並新增自訂請求標頭資訊
async function handle(event) {
  // 取得用戶端傳入的請求
  const request = event.request;

  // 在請求標頭中新增自訂標頭"x-via-sparrow-start"，值為當前時間戳
  request.headers.append("x-via-sparrow-start", `${Date.now()}`);

  // fetch 反向代理，發送請求並等待響應
  const response = await fetch(request);

  // 在響應標頭中新增自訂標頭"x-via-sparrow-done"，值為當前時間戳
  response.headers.append("x-via-sparrow-done", `${Date.now()}`);
  
  // 將處理後的響應物件返回給用戶端
  return response;
}
```


<span id="相關執行時-api"></span>
## 相關執行時 API


* [addEventListener() 方法](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-addEventListener-cn-zh-tw)

* [FetchEvent 介面](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-FetchEvent-cn-zh-tw)

* [Headers 介面](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Headers-cn-zh-tw)

* [Response 介面](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Response-cn-zh-tw)

* [fetch() 方法](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-fetch-cn-zh-tw)
