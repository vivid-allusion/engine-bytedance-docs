---
title: "FetchEvent"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-FetchEvent-jp"
---

fetchタイプのイベントで、ドメイントリガーによってトリガーされます。

MDNドキュメントの[FetchEvent](https://developer.mozilla.org/en-US/docs/Web/API/FetchEvent)を参照してください。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">エッジ関数のランタイムでは、<code>FetchEvent()</code> コンストラクタを使用して <code>FetchEvent</code> オブジェクトを構築することはできません。<a href="https://docs.byteplus.com/en/docs/byteplus-cdn/docs-addEventListener-jp">addEventListener()</a>を呼び出してfetchイベントをリッスンするリスナーを登録することで、<code>FetchEvent</code>オブジェクトを取得する必要があります。</div>


<span id="メソッド"></span>
## メソッド

<span id="respondwith"></span>
### respondWith()

fetchイベントがトリガーされると、エッジ関数はユーザーからのリクエストをインターセプトし、このメソッドに渡した [Response](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Response-jp) オブジェクトまたは [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) オブジェクトをレスポンスとして返します。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning"><code>respondWith()</code>メソッドを呼び出さない場合、エッジ関数はfetchイベントがトリガーされたときにユーザーリクエストをBytePlus CDNに転送します。</div>


<span id="例"></span>
#### 例

```js
// エッジ関数はユーザーリクエストをBytePlus CDNに転送します。
addEventListener(
    'fetch', (event) => {
      console.log("callback1 has been triggered");
    });

// エッジ関数はユーザーリクエストをインターセプトし、メソッドのパラメータにResponseオブジェクトをレスポンスとして渡すことができます。
addEventListener(
    'fetch', (event) => {
      console.log("callback2 has been triggered");
      event.respondWith(new Response("callback2 has been triggered"));  
    });
```


<span id="waituntil"></span>
### waitUntil()

コールバック関数内で登録されたすべての[Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)オブジェクトがresolveまたはrejectされるまで、エッジ関数ランタイムが待機することを通知します。`waitUntil()`メソッドは複数回呼び出すことができます。また、`waitUntil()`メソッドをネストして使用することもできます。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">関数の実行時間が<a href="https://docs.byteplus.com/en/docs/byteplus-cdn/usage-limits-jp">エッジ関数の使用制限</a>を超える場合、エッジ関数ランタイムはリクエストコンテキストを破棄し、pending状態の<code>Promise</code>オブジェクトを待機しなくなります。</div>


* <div data-tips="true" data-tips-type="warning"><code>waitUntil()</code>で登録されたいずれかの<code>Promise</code>オブジェクトがrejectされた場合、エッジ関数ランタイムはリクエストコンテキストを破棄します。各<code>Promise</code>に対してエラーハンドリングを追加することを推奨します。例：<code>.catch()</code>メソッドまたは<code>try-catch</code>ステートメントを使用します。</div>



`waitUntil()`メソッドを呼び出さず、`await`も使用しない場合、コールバック関数が`respondWith()`を介してレスポンスを返すと、エッジ関数ランタイムはリクエストコンテキストを破棄し、pending状態の`Promise`オブジェクトを待機しなくなります。`await`は`Promise`オブジェクトがresolveまたはrejectされるのを待つことができますが、コールバック関数の実行を一時停止します。一方、`waitUntil()`メソッドは`Promise`オブジェクトがresolveまたはrejectされるのを待ちながら、コールバック関数が他の操作を継続実行できるようにします。

<span id="例"></span>
#### 例

```JavaScript
// ログアップロード用のURLを定義
const uploadURL = "https://log-collection.example.com/";

// レスポンスタイムをアップロードする非同期関数
async function uploadLog(waiter) {
    const start = Date.now();
    // waiter promiseが完了するのを待ち、これはリクエストレスポンスが送信完了したことを示します
    await waiter;
    // 終了時刻を記録。注意：エッジ関数のクロックは約10 msに調整されています。これはサイドチャネル攻撃を防ぐためです。
    const end = Date.now();
    const cost = (end - start);
    // オブジェクトをJSON文字列にシリアライズしてリクエストボディとします
    const body = JSON.stringify({ cost: cost });
    await fetch(uploadURL, {
        method: "POST",
        body: body,
        headers: {
            'Content-Type': 'application/json'
        }
    });
}

// fetchイベントをリッスンし、イベント発生時にhandle関数を呼び出して処理します
addEventListener('fetch', (event) => {
    event.respondWith(handle(event));
});

// イベントを処理する関数
async function handle(event) {
    const response = new Response("Hello World");
    // response.bodyはreadableStreamです。エッジ関数ランタイムAPIにはwaitCloseメソッドが含まれています
    // waitCloseはpromiseを返します。ストリームが終了したとき（エラーまたは完了の可能性があります）、waitCloseがresolveされます
    // 注意：もし Response が Body を含まないレスポンスを返すために使用される場合（例えば、HTTP HEAD リクエストへのレスポンス、304レスポンス、204レスポンスなど）、waitClose() は無効です
    event.waitUntil(uploadLog(response.body.waitClose()));
    return response;
}
```


<span id="プロパティ"></span>
## プロパティ

<span id="info"></span>
### info

クライアント情報を取得します。


* `info.clientIp`：クライアントのIPアドレス。クライアントにプロキシが設定されている場合、このプロパティはプロキシサーバーのIPアドレスを返します。

* `info.geo`：クライアントIPの地理情報。geoには以下のプロパティがあります：

   * `geo.country`：IPアドレスが属する国の名前を返します。例：`China`または`United States`。

   * `geo.countryCode`：IPアドレスが属する国の2文字コードを返し、ISO 3166\-1 alpha\-2標準に準拠しています。例：`CN`または`US`。

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">中国香港（Hong Kong）、中国マカオ（Macao）、および中国台湾（Taiwan）は、<code>province</code> フィールドによってのみ識別できます。香港、マカオ、および台湾の <code>countryCode</code> はすべて <code>CN</code> となります。   </div>
   

   * `geo.region`：IPアドレスが属する中国の地理的地域の名前を返します。例：`EastChina`。IPアドレスが中国本土に属していない場合、このパラメータは`XX`を返します。

   * `geo.province`：IPアドレスが属する第一レベルの行政区の名前を返します。例：`Hebei`または`New Jersey`。

   * `geo.city`：IPアドレスが属する都市の名前を返します。例：`Shijiazhuang`または`Tampere`。

   * `geo.isp`：IPアドレスが属するISPの名前を返します。例：`ChinaUnicom`または`DigitalOcean`。


<span id="例"></span>
#### 例

```JavaScript
addEventListener(
    'fetch', (event) => { event.respondWith(handle(event)); });
    
async function handle(event) {
  const info = event.info;
  console.log(info);  // すべてのクライアント情報を取得

  const clientIp = event.info.clientIp;
  console.log(clientIp); // クライアントのIPアドレスを取得

  const country = event.info.geo.country;
  console.log(country); // クライアントIPアドレスの国名を取得

  return new Response("done");
}
```


<span id="file"></span>
### File

MDNドキュメントの[File](https://developer.mozilla.org/en-US/docs/Web/API/File)を参照してください。

<span id="blob"></span>
### Blob

MDNドキュメントの[Blob](https://developer.mozilla.org/en-US/docs/Web/API/Blob)を参照してください。

<span id="formdata"></span>
### FormData

MDNドキュメントの[FormData](https://developer.mozilla.org/en-US/docs/Web/API/FormData)を参照してください.
