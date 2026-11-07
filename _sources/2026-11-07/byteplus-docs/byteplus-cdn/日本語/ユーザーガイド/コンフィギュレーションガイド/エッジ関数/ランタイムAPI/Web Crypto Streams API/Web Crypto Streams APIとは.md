---
title: "Web Crypto Streams APIとは"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/WebCryptoStream-jp"
---

[Web Crypto API](https://docs.byteplus.com/docs/byteplus-cdn/web-crypto-overview-jp)はデータを処理する際に、まずデータをメモリにロードする必要があります。ただし、エッジ関数は各関数が使用できるメモリサイズを制限しています。詳細は[使用制限](https://docs.byteplus.com/docs/byteplus-cdn/usage-limits-jp)をご参照ください。処理が必要なデータのサイズがメモリ制限を超える場合、メモリにロードすることができません。

この問題を解決するため、エッジ関数ランタイムはWeb Crypto Streams APIを提供しています。Web Crypto Streams APIは、Web Crypto APIの拡張機能で、データストリームを処理することができます。大きなデータをデータストリームに変換することで、メモリサイズの制限によってデータをメモリにロードできない問題を回避できます。

Web Crypto Streams APIは以下のAPIをサポートしています：


* [DigestStream](https://docs.byteplus.com/docs/byteplus-cdn/DigestStream-jp)
