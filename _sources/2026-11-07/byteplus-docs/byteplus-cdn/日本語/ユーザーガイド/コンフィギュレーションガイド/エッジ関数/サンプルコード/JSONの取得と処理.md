---
title: "JSONの取得と処理"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-JSON-processing-jp"
---

この例は、JSONデータの取得と処理方法を示しています。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">この例では、具体的なJSONデータ処理ロジックは示していません。<code>handleJSON()</code>メソッド内に独自のデータ処理ロジックを追加することができます。例えば、エッジファンクションはミドルウェア層（Backend\-for\-Frontend、BFF）として機能し、以下のようなロジックを実装することができます：</div>



* <div data-tips="true" data-tips-type="tip">サーバーから返されたJSONデータの前処理を行い、データの抽出やクレンジングを行う。</div>


* <div data-tips="true" data-tips-type="tip">GraphQLライブラリを使用してエッジノードにGraphQLサーバーを設置する。ユーザーはGraphQL言語を使用してJSONデータをクエリできる。</div>


* <div data-tips="true" data-tips-type="tip">サーバーから返されたJSONデータの要約と分析を行う。</div>



```JavaScript
addEventListener('fetch', (event) => {
  event.respondWith(handle(event));
});

function handleJSON(json) {
  // Process your JSON data here
}

async function handle(event) {
  // Request a JSON API and parse it
  const req = await fetch("http://www.example.com/json");
  const json = await req.json();

  const data = handleJSON(json);
  // Return the processed data
  return data;
} 
```


<span id="関連するランタイムapi"></span>
## 関連するランタイムAPI


* [addEventListener()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-addEventListener-jp)

* [FetchEvent](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-FetchEvent-jp)

* [Response](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Response-jp)

* [fetch()](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-fetch-jp)
