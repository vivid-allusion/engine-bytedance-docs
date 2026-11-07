---
title: "Response"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Response-jp"
---

リクエストに対するレスポンスを表します。MDNドキュメントの[Response](https://developer.mozilla.org/en-US/docs/Web/API/Response)を参照してください。

<span id="使用方法"></span>
## 使用方法

<span id="responseインターフェースがサポートするメソッド"></span>
### Responseインターフェースがサポートするメソッド

Responseインターフェースは以下のメソッドをサポートしています。


* `Response`オブジェクトのコピーを作成する：`Response.clone()`

* 異なるURLで新しいレスポンスを作成する：`Response.redirect(url, status)`


<span id="content-lengthヘッダーによるペイロード送信への影響"></span>
### Content\-Lengthヘッダーによるペイロード送信への影響

`Request`オブジェクトと`Response`オブジェクトの`Content-Length`ヘッダーはペイロードの送信方法に影響します。


* `Request`オブジェクトまたは`Response`オブジェクトに`Content-Length`ヘッダーが含まれている場合：

   * `Content-Length`ヘッダーの値が0以上の数値である場合：ランタイムは`Content-Length`ヘッダーに従い、`Content-Length`ヘッダーで指定されたバイト数のペイロードのみを送信します。ペイロードの残りの部分は破棄されます。

   * `Content-Length`ヘッダーの値が無効な場合：ランタイムは`Content-Length`ヘッダーを無視し、チャンク転送エンコーディングを使用してペイロードを送信します。

* `Request`オブジェクトまたは`Response`オブジェクトに`Content-Length`ヘッダーが含まれていない場合、ランタイムはチャンク転送エンコーディングを使用してペイロードを送信します。
