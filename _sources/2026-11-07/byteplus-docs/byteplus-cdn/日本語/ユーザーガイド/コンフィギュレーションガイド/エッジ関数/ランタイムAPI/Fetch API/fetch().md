---
title: "fetch()"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-fetch-jp"
---

HTTPまたはHTTPSリクエストを送信します。MDNドキュメントの[fetch()](https://developer.mozilla.org/docs/Web/API/WindowOrWorkerGlobalScope/fetch)を参照してください。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">関数が<code>fetch()</code>を呼び出してHTTPレスポンスを取得し、HTMLボディを変更する場合（たとえば、<a href="https://docs.byteplus.com/en/docs/byteplus-cdn/function-createHtmlStream-jp">createHtmlStream()</a>を使用してHTMLボディをストリーム変更する場合）、元のHTTPレスポンスから<code>Content-Length</code>ヘッダーを削除することをお勧めします。そうしないと、データ送信エラーが発生する可能性があります。これは、HTTPレスポンスに<code>Content-Length</code>ヘッダーが含まれている可能性があるためです。ランタイムが元のレスポンスの<code>Content-Length</code>ヘッダーを転送している間に、関数がHTTPレスポンスのHTMLボディを変更すると、ペイロードの実際のサイズが<code>Content-Length</code>ヘッダーの値と異なります。詳細については、<a href="https://docs.byteplus.com/en/docs/18/36556#payload">Content\-Lengthヘッダーによるペイロード送信への影響</a>を参照してください。</div>


<span id="使用制限"></span>
## 使用制限


* `fetch()`メソッドは、デフォルトのポートを使用してリクエストを送信します。HTTPリクエストのデフォルトポートは80、HTTPSリクエストのデフォルトポートは443です。

* リクエストアドレスにIPアドレスは使用できません。

* リクエストアドレスからスキームを省略することはできません。たとえば、`fetch("www.example.com")`は正しくありません。`fetch("https://www.example.com")`に変更する必要があります。


<span id="使用方法"></span>
## 使用方法

<span id="byteplus-cdnドメインへのアクセス"></span>
### BytePlus CDNドメインへのアクセス

デフォルトでは、`fetch()`はインターネット経由でリクエストを送信します。`fetch()`メソッドがアクセスするドメインがBytePlus CDNドメインである場合、`{proxy: "cdn"}`パラメータを使用して、エッジノード内でリクエストを内部的に送信するように`fetch()`メソッドを設定することをお勧めします。エッジ関数とBytePlus CDNはエッジノードを共有しているため、関数によって送信されたリクエストはエッジノード内で直接BytePlus CDNに転送されます。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">BytePlus CDNドメインは、BytePlus CDNがコンテンツ配信サービスを提供する任意のドメイン名です。BytePlus CDNでのドメインのステータスは<strong>有効</strong>である必要があります。</div>


たとえば、次のメソッドを使用して、BytePlus CDNドメイン`cdn.example.com`およびサードパーティAPIサービスドメイン`api.example.com`をリクエストできます。

```js
// BytePlus CDNドメインcdn.example.comをリクエストする
const responseCDN = await fetch("https://cdn.example.com", { proxy: "cdn" });

// サードパーティAPIサービスドメインapi.example.comをリクエストする
const responseAPI = await fetch("https://api.example.com");
```


次の図は、`{proxy: "cdn"}`パラメータを渡した場合と渡さなかった場合のリクエストパスの違いを示しています。

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_e0b83d3c4f38d9c7c09b64a8673fea6d.png) </span>

次の表は、`{proxy: "cdn"}`パラメータを渡した場合と渡さなかった場合の違いを比較したものです。


|相違点 |`{proxy: "cdn"}`を使用 |`{proxy: "cdn"}`を使用しない（デフォルト） |
|---|---|---|
| **リクエストパス**  |関数によって送信されたリクエストは、エッジノード内で直接BytePlus CDNに転送されます。 |関数によって送信されたリクエストは、DNS解決を介してインターネット経由でエッジノードにルーティングされます。このエッジノードは、関数が実行されるエッジノードと必ずしも同じではありません。 |
| **コスト**  |BytePlus CDN側でトラフィックコストは発生しません。 |リクエストされたドメインがBytePlus CDNドメインである場合、インターネット経由のリクエストはBytePlus CDN側でトラフィックコストが発生します。 |
|**適用シナリオ**  |BytePlus CDNドメインへのアクセスにのみ適用されます。リクエストされたドメインがBytePlus CDNドメインでない場合、リクエストは失敗します。関数は403エラーコードを返します。 |BytePlus CDNドメインを除く、インターネット経由でアクセスできる任意のドメインへのアクセスに適用されます。リクエストされたドメインがBytePlus CDNドメインである場合、リクエストはドメインのアクセス制御（IPブロックリスト/許可リスト、地理的制限など）の対象となる場合があります。 |


<span id="_3xxリダイレクトの追跡"></span>
### 3xxリダイレクトの追跡

`redirect`パラメータを使用して、`fetch()`メソッドが3xxリダイレクトをどのように処理するかを設定できます。


* `{redirect: "manual"}`（デフォルト）：3xxリダイレクトを自動的に追跡しません。リダイレクトを手動で処理できます。

* `{redirect: "follow"}`：3xxリダイレクトを自動的に追跡します。同じリクエストに対して、`fetch()`メソッドはデフォルトで最大4つのリダイレクトを追跡し、クロスドメインおよびクロスプロトコルのリダイレクトを許可します。

* `{redirect: "error"}`：3xxリダイレクトが発生した場合にエラーをスローします。


次の例は、3xxリダイレクトを自動的に追跡する方法を示しています。

```js
const response = await fetch("https://www.example.com", {redirect: "follow"});
```


さまざまなステータスコードに対する`fetch()`のリダイレクト動作は次のとおりです。


| **ステータスコード**  | **リダイレクト動作** |
|---|---|
|301, 302, 303, 308 |リダイレクトされたリクエストのリクエストメソッドはGETに変更されます。リクエストボディは無視されます。 |
|307 |GETメソッドのみを追跡します。他のHTTPメソッドで開始されたリクエストの場合、このメソッドはリダイレクトを自動的に追跡せず、エラーをスローします。 |


リダイレクトアドレスは、`Location`レスポンスヘッダーから取得されます。`Location`レスポンスヘッダーは現在、カンマ区切りのリストを受け入れますが、最初のURLのみが追跡され、その他は無視されます。

<span id="レスポンスデータの解凍"></span>
### レスポンスデータの解凍

`fetch()` メソッドは現在、**gzip** 形式のレスポンスデータの解凍のみをサポートしています。`decompression` パラメータを使用して、`fetch()` メソッドがレスポンスデータを解凍するかどうかを設定できます。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><code>fetch()</code> メソッドは、レスポンスの <code>Content-Encoding</code> ヘッダーを介して圧縮形式を識別します。例えば：</div>



* <div data-tips="true" data-tips-type="tip"><code>Content-Encoding</code> が <code>gzip</code> または <code>gzip, identity</code> の場合、レスポンスは gzip 圧縮として認識されます。</div>


* <div data-tips="true" data-tips-type="tip"><code>Content-Encoding</code> が <code>brotli, gzip</code> の場合、<code>fetch()</code> メソッドは最も外側の gzip 圧縮のみを解凍します。</div>


* `manual`：**解凍しない** 。元のレスポンスデータを直接返します。

* `fallbackIdentity`：（デフォルト）**自動的に解凍する** 。サポートされていない圧縮形式の場合は、元のデータを返します。

* `decompress`：**自動的に解凍する** 。サポートされていない圧縮形式の場合は、エラーをスローします。


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">解凍後、<code>Content-Length</code> レスポンスヘッダーはデータサイズを正確に反映しなくなります。データ転送エラーを防ぐため、ランタイムはこのレスポンスヘッダーを削除し、<code>X-Content-Length-Before-Decompression</code> レスポンスヘッダーを追加して元のデータサイズを記録します。</div>


次の例は、`fetch()` メソッドがレスポンスデータを自動的に解凍し、サポートされていない圧縮形式の場合は元のデータを返すように設定する方法を示しています。

```js
const response = await fetch("https://www.example.com", {decompression: "fallbackIdentity"});
```


<span id="解凍後の-content-encoding-ヘッダーの処理"></span>
#### 解凍後の `Content-Encoding` ヘッダーの処理

解凍後、`fetch()` メソッドは `Content-Encoding` レスポンスヘッダーを次のように修正します：


* `Content-Encoding: identity, gzip` は `Content-Encoding: identity` に変更されます。

* `Content-Encoding: gzip` は削除されます。

* `Content-Encoding: gzip, identity` は削除されます。

* `Content-Encoding: brotli, gzip` は `Content-Encoding:brotli` に変更されます。


<span id="追加情報"></span>
## 追加情報

&nbsp;

<span id="content-lengthヘッダーによるペイロード送信への影響"></span>
### Content\-Lengthヘッダーによるペイロード送信への影響

`Request`オブジェクトと`Response`オブジェクトの`Content-Length`ヘッダーはペイロードの送信方法に影響します。


* `Request`オブジェクトまたは`Response`オブジェクトに`Content-Length`ヘッダーが含まれている場合：

   * `Content-Length`ヘッダーの値が0以上の数値である場合：ランタイムは`Content-Length`ヘッダーに従い、`Content-Length`ヘッダーで指定されたバイト数のペイロードのみを送信します。ペイロードの残りの部分は破棄されます。

   * `Content-Length`ヘッダーの値が無効な場合：ランタイムは`Content-Length`ヘッダーを無視し、チャンク転送エンコーディングを使用してペイロードを送信します。

* `Request`オブジェクトまたは`Response`オブジェクトに`Content-Length`ヘッダーが含まれていない場合、ランタイムはチャンク転送エンコーディングを使用してペイロードを送信します。
