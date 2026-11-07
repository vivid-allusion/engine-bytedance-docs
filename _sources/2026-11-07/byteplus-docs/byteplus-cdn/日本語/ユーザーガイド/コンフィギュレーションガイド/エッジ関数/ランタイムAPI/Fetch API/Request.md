---
title: "Request"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Request-jp"
---

リソースリクエストを表します。詳細な定義と使用方法については、MDNドキュメントの[Request](https://developer.mozilla.org/en-US/docs/Web/API/Request)を参照してください。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Edge Functionsのランタイムは、Requestインターフェースの以下のプロパティをサポートしていません：</div>



* <div data-tips="true" data-tips-type="tip">context</div>


* <div data-tips="true" data-tips-type="tip">credentials</div>


* <div data-tips="true" data-tips-type="tip">destination</div>


* <div data-tips="true" data-tips-type="tip">integrity</div>


* <div data-tips="true" data-tips-type="tip">mode</div>


* <div data-tips="true" data-tips-type="tip">referrer</div>


* <div data-tips="true" data-tips-type="tip">referrerPolicy</div>


* <div data-tips="true" data-tips-type="tip">cache</div>



<span id="使用方法"></span>
## 使用方法

<span id="requestインターフェースの標準プロパティとメソッド"></span>
### Requestインターフェースの標準プロパティとメソッド

Requestインターフェースは以下の標準プロパティとメソッドをサポートしています。

<span id="プロパティ"></span>
#### プロパティ

以下のプロパティはすべて読み取り専用です。


* リクエストメソッドの取得：`request.method`

* リクエストURLの取得：`request.url`

* リクエストヘッダーの取得：`request.headers`

* リクエストペイロードの取得：`request.body`、bodyはReadableStreamオブジェクトです。


<span id="メソッド"></span>
#### メソッド


* JSONの取得：`await request.json()`

* フォームデータの取得：`await request.formData()`

* UTF8文字列の取得：`await request.text()`


<span id="edge-functionsランタイム固有の非標準プロパティ"></span>
### Edge Functionsランタイム固有の非標準プロパティ

Requestインターフェースの標準プロパティに加えて、Edge Functionsランタイムは以下の非標準プロパティも追加しています：

以下のプロパティはすべて読み取り専用です。


* ホストリクエストヘッダーの取得：`request.host`

* リクエストドメイン名の取得：`request.hostname`

* リクエストパスの取得：`request.path`

* リクエストURLのパラメータの取得：`request.query`


<span id="content-lengthヘッダーによるペイロード送信への影響"></span>
### Content\-Lengthヘッダーによるペイロード送信への影響

`Request`オブジェクトと`Response`オブジェクトの`Content-Length`ヘッダーはペイロードの送信方法に影響します。


* `Request`オブジェクトまたは`Response`オブジェクトに`Content-Length`ヘッダーが含まれている場合：

   * `Content-Length`ヘッダーの値が0以上の数値である場合：ランタイムは`Content-Length`ヘッダーに従い、`Content-Length`ヘッダーで指定されたバイト数のペイロードのみを送信します。ペイロードの残りの部分は破棄されます。

   * `Content-Length`ヘッダーの値が無効な場合：ランタイムは`Content-Length`ヘッダーを無視し、チャンク転送エンコーディングを使用してペイロードを送信します。

* `Request`オブジェクトまたは`Response`オブジェクトに`Content-Length`ヘッダーが含まれていない場合、ランタイムはチャンク転送エンコーディングを使用してペイロードを送信します。
