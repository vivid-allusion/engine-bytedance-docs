---
title: "获取并处理JSON数据"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-JSON-processing-cn"
---

该示例展示了如何获取并处理 JSON 数据。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">本示例没有展示具体的 JSON 数据处理逻辑。您可以在 <code>handleJSON()</code> 方法中自行添加数据处理逻辑。例如，边缘函数可以作为中间层（Backend\-for\-Frontend, BFF）实现以下逻辑：</div>



* <div data-tips="true" data-tips-type="tip">对服务端返回的 JSON 数据进行预处理，用于数据抽取或清洗。</div>


* <div data-tips="true" data-tips-type="tip">通过 GraphQL 库在边缘节点搭建 GraphQL 服务器。用户可以通过 GraphQL 语言查询 JSON 数据。</div>


* <div data-tips="true" data-tips-type="tip">对服务端返回的 JSON 数据进行汇总和统计。</div>



```JavaScript
addEventListener('fetch', (event) => {
  event.respondWith(handle(event));
});

function handleJSON(json) {
  // 处理您的JSON数据
}

async function handle(event) {
  // 请求一个JSON API并且解析
  const req = await fetch("http://www.example.com/json");
  const json = await req.json();

  const data = handleJSON(json);
  // 返回处理过的数据
  return data;
}
```


<span id="相关运行时-api"></span>
## 相关运行时 API


* [addEventListener() 方法](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-addEventListener-cn)

* [FetchEvent 接口](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-FetchEvent-cn)

* [Response 接口](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Response-cn)

* [fetch() 方法](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-fetch-cn)
