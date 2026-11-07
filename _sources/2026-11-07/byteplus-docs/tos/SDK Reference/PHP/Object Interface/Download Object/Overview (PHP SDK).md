---
title: "Overview (PHP SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Overview-php-sdk2"
---

The TOS PHP SDK supports downloading objects through normal downloads or range downloads. You can choose the appropriate download method according to your business needs and the scenarios applicable to different methods.

<span id=".5LiL6L295pa55byP6K-05piO"></span>
## Download method description


* [Normal Download (PHP SDK)](https://docs.byteplus.com/docs/tos/Normal-download-php-sdk):It is generally used to download small objects.

* [Limited Download (PHP SDK)](https://docs.byteplus.com/docs/tos/Limited-download-php-sdk): If the qualification is met, it will be downloaded. If it is not met, an exception will be thrown and the download behavior will not be triggered.

* [Scope Download (PHP SDK)](https://docs.byteplus.com/docs/tos/Scope-download-php-sdk): Generally used for sharding to download large objects. When the object is large, use range download.
