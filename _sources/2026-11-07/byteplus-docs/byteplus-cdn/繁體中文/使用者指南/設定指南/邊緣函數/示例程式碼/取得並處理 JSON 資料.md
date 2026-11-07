---
title: "取得並處理 JSON 資料"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-JSON-processing-cn-zh-tw"
---

本示例展示如何取得並處理 JSON 資料。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">本示例未展示具體的 JSON 資料處理邏輯。您可以在 <code>handleJSON()</code> 方法中自行新增資料處理邏輯。例如，邊緣函數可作為中介層（Backend\-for\-Frontend, BFF）實現以下邏輯：</div>



* <div data-tips="true" data-tips-type="tip">對服務端返回的 JSON 資料進行預處理，用於資料抽取或清洗</div>


* <div data-tips="true" data-tips-type="tip">透過 GraphQL 庫在邊緣節點建立 GraphQL 伺服器。使用者可透過 GraphQL 語言查詢 JSON 資料</div>


* <div data-tips="true" data-tips-type="tip">對服務端返回的 JSON 資料進行匯總和統計</div>



```JavaScript
addEventListener('fetch', (event) => {
  event.respondWith(handle(event));
});

function handleJSON(json) {
  // 處理您的JSON資料
}

async function handle(event) {
  // 請求一個JSON API並解析
  const req = await fetch("http://www.example.com/json");
  const json = await req.json();

  const data = handleJSON(json);
  // 返回處理過的資料
  return data;
}
```


<span id="相關運行時-api"></span>
## 相關運行時 API


* [addEventListener() 方法](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-addEventListener-cn-zh-tw)

* [FetchEvent 介面](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-FetchEvent-cn-zh-tw)

* [Response 介面](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Response-cn-zh-tw)

* [fetch() 方法](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-fetch-cn-zh-tw)
