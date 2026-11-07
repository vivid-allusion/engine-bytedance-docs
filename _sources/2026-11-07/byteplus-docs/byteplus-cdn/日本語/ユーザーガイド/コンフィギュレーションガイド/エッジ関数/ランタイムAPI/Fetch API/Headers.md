---
title: "Headers"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Headers-jp"
---

HTTPリクエストおよびレスポンスヘッダーに対して、取得、設定、追加、削除などの操作を実行します。MDNドキュメントの[Headers](https://developer.mozilla.org/en-US/docs/Web/API/Headers)を参照してください。

<span id="ヘッダーブロックリスト"></span>
## ヘッダーブロックリスト

エッジ関数のランタイムは、以下のヘッダーをデフォルトでブロックリストに設定しています。関数がブロックリストに登録されているヘッダーの読み取りや書き込みを試みると、ランタイムエラーが発生し、悪意のある意図があると見なされる可能性があり、ランタイムの一時的な禁止につながる可能性があります。


* Expect

* Te

* Trailer

* Upgrade

* Proxy\-Connection

* Connection

* Host

* Keep\-Alive

* DNT

* X\-Sparrow\-で始まるヘッダー

* その他の特別な内部ヘッダー
