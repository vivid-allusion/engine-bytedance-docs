---
title: "Overview (.NET SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Overview7"
---

The TOS .NET SDK supports various object download methods, including standard download and range download. You may select the appropriate download method according to your business requirements and the applicable scenarios for each method.

<span id=".5LiL6L295pa55byP6K-05piO"></span>
## Download Method Instructions


* [Standard Download](https://docs.byteplus.com/docs/tos/Normal-download-net-sdk): typically used for downloading small objects.

* [Conditional Download](https://docs.byteplus.com/docs/tos/Limited-download-net-sdk): The download will proceed only if the restrictive conditions are met; if not, an exception will be returned and the download will not be triggered.

* [Range Download](https://docs.byteplus.com/docs/tos/Scope-download-net-sdk): When you only need to download a portion of an object's data, you can use range download.


When downloading objects, the TOS .NET SDK supports streaming downloads. The object download interface returns a Stream, which serves as the data source for reading.
