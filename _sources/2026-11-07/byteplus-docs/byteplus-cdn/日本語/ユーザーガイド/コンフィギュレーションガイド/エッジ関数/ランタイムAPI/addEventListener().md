---
title: "addEventListener()"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-addEventListener-jp"
---

イベントリスナーを登録します。MDNのドキュメント [addEventListener](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener) を参照してください。

エッジ関数は以下のイベントタイプをサポートしています：


* fetch: ドメイン名トリガーによってトリガーされるイベントタイプ。詳細は[FetchEvent](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-FetchEvent-jp)を参照してください。

* cron: Cronトリガーによってトリガーされるイベントタイプ。詳細は[CronEvent](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-CronEvent-jp)を参照してください。


同じコードファイル内でcronイベントとfetchイベントの両方を登録できます。これら2種類のイベントのコールバック関数は互いに干渉しません。各イベントに対して最大16個のコールバック関数を登録できます。

`addEventListener()`を複数回呼び出して、同じまたは異なるイベントに対して複数のリスナーを登録できます。各リスナーで1つのコールバック関数を登録します。


* fetchイベントの場合、複数のコールバック関数が登録された順序で実行されます。コールバック関数が既に [FetchEvent](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-FetchEvent-jp#respondwith) を呼び出して結果を返している場合、その後に登録されたが呼び出されていないコールバック関数は実行されません。すべてのコールバック関数が応答時間制限内に結果を返せない場合、ランタイムはエラーをスローします。

* cronイベントの場合、最初のコールバック関数のみが実行されます。最初のコールバック関数が応答時間制限内に結果を返さない場合、ランタイムはエラーをスローします。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">エッジ関数の応答時間制限については、<a href="https://docs.byteplus.com/docs/byteplus-cdn/Usage_Limits_Functions">使用制限</a>を参照してください。</div>


<span id="例"></span>
## 例

<span id="fetchイベントのリッスン"></span>
### fetchイベントのリッスン

以下のコードは、fetchイベントをリッスンする方法を説明しています。

```JavaScript
addEventListener(
    'fetch', (event) => {
      console.log("callback1 has been triggered");
    });

addEventListener(
    'fetch', (event) => {
      console.log("callback2 has been triggered");
      event.respondWith(new Response("callback2 has been triggered"));  
    });
// This callback function will never be executed
addEventListener('fetch', (event) => {
    console.log("This will never be displayed");
});
```


<span id="cronイベントのリッスン"></span>
### cronイベントのリッスン

以下のコードは、cronイベントをリッスンする方法を説明しています。

```javascript
addEventListener('cron', onCron);

async function onCron(event) {

    // 1. You can add payload data to each Cron trigger through OpenAPI or console. 
    // You can get payload data by using the following API of the event object.
  const text = await event.text();

  // 2. Gets attributes of the Cron trigger
  const job = event.job; 
  const cronExpression = event.cronExpression; 
  console.log("cron triggered");
}
```
