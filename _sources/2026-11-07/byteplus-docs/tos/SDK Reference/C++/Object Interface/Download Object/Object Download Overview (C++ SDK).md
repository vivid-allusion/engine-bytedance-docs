---
title: "Object Download Overview (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Download-object-overview-c-sdk"
---

The TOS C++ SDK supports object downloads through methods such as standard download and range download. You can select the appropriate download method according to your business requirements and the scenarios in which each method is applicable.

<span id=".5LiL6L295pa55byP6K-05piO"></span>
## Instructions for download methods


* [Standard Download](https://docs.byteplus.com/docs/tos/Normal-download-c-sdk): Directly download the entire object from the specified bucket.

* [Conditional Download](https://docs.byteplus.com/docs/tos/Limited-download-c-sdk): The download will proceed only if the specified conditions are met; if not, an exception will be thrown and the download action will not be triggered.

* [Range Download](https://docs.byteplus.com/docs/tos/Scope-download-c-sdk): If you do not need to download the entire object but only require part of its data, you can use range download to download data within a specified range.

* [Resumable Download](https://docs.byteplus.com/docs/tos/Breakpoint-resume-download-c-sdk): When downloading a file, if the download fails due to network issues or program crashes, you can use resumable download to continue downloading files that were not successfully downloaded.
