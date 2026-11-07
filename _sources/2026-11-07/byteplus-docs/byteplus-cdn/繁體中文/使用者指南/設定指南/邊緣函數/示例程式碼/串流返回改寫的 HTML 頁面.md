---
title: "串流返回改寫的 HTML 頁面"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Modify-the-footer-header-cn-zh-tw"
---

本示例展示如何將取得的 HTML 頁面寫入可寫串流中，對串流中的 HTML 頁面進行改寫，並將改寫後的 HTML 頁面作為響應串流返回給用戶端。

```JavaScript
addEventListener('fetch', (event) => {
  event.respondWith(handle(event));
});

// 定義非同步函式用於處理請求
async function handle(event) {

  // 建立可讀寫的TransformStream物件
  const {readable, writable} = new TransformStream();
  
  // 非同步取得'http://www.example.com'的請求內容
  const request = await fetch('http://www.example.com');
  
  // 非同步將請求內容寫入可寫串流，並在內容末尾新增註解作為頁尾
  (async () => {
    await request.body.pipeTo(writable, {preventClose: true});
    {
      const writer = writable.getWriter();
      await writer.write('\n\n\n<!----------- 這就是footer喲！---------->');
      await writer.close();
    }
  })();

  // 將可讀串流作為Response物件的內容返回
  return new Response(readable);
}
```


<span id="相關執行時-api"></span>
## 相關執行時 API


* [addEventListener() 方法](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-addEventListener-cn-zh-tw)

* [FetchEvent 介面](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-FetchEvent-cn-zh-tw)

* [fetch() 方法](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-fetch-cn-zh-tw)

* [Streams 介面](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Streams-cn-zh-tw)
