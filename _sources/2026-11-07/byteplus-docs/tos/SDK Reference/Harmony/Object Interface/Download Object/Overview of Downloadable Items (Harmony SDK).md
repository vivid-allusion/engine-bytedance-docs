---
title: "Overview of Downloadable Items (Harmony SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Overview-of-downloading-objects-harmony-sdk"
---

TOS Harmony SDK supports object downloads through methods such as direct download and range download. You may select the appropriate download method according to your business requirements and the scenarios in which each method is applicable.

<span id="19cf195e"></span>
## Download Method Instructions


* [Standard Download](https://docs.byteplus.com/docs/tos/Normal-download-node-js-sdk): Directly download the entire object from the specified bucket.

* [Conditional Download](https://docs.byteplus.com/docs/tos/Limited-download-node-js-sdk): The download will proceed only if the specified conditions are met; if not, an exception will be thrown and the download action will not be triggered.

* [Range Download](https://docs.byteplus.com/docs/tos/Scope-download-node-js-sdk): If you do not need to download the entire object and only require a portion of the object's data, you can use range download to download data within the specified range.


When downloading objects, the Harmony SDK supports streaming downloads, with the download object interface returning a Readable stream as the data source for reading.
