---
title: "什麼是 Web Crypto Streams API"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/WebCryptoStream-zh-tw"
---

[Web Crypto API](https://docs.byteplus.com/docs/byteplus-cdn/web-crypto-overview-zh-tw) 在處理資料時，需要先將資料載入到記憶體。但是，邊緣函數限制了每個函數可使用的記憶體大小。參見 [使用限制](https://docs.byteplus.com/docs/byteplus-cdn/functions-usage-limits-zh-tw)。如果需要被處理的資料大小超出了記憶體限制，就無法被載入到記憶體。

為了解決這個問題，邊緣函數執行時期提供了 Web Crypto Streams API。Web Crypto Streams API 是對 Web Crypto API 的擴展，能處理資料流。您將較大的資料轉換為資料流後，就可以避免因記憶體大小限制造成資料無法被載入到記憶體的問題。

Web Crypto Streams API 支援以下 API：


* [DigestStream](https://docs.byteplus.com/docs/byteplus-cdn/DigestStream-zh-tw)
