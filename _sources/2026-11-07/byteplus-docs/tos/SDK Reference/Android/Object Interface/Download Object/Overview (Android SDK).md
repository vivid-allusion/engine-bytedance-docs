---
title: "Overview (Android SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Overview-android-sdk11"
---

The TOS Android SDK supports methods for downloading objects, such as direct download and range download. You can select the appropriate download method based on your business requirements and the scenarios in which each method is applicable.

<span id=".5LiL6L295pa55byP6K-05piO"></span>
## Download Method Instructions


* [Standard Download](https://docs.byteplus.com/docs/tos/Normal-download-android-sdk): Typically used for downloading small objects.

* [Conditional Download](https://docs.byteplus.com/docs/tos/Limited-download-android-sdk): The download will proceed only if the specified conditions are met; otherwise, an exception will be thrown and the download action will not be triggered.

* [Range Download](https://docs.byteplus.com/docs/tos/Scope-download-android-sdk): Typically used for segmented downloading of large objects. When the object is large, please use range downloading.

* [Resumable Download](https://docs.byteplus.com/docs/tos/Breakpoint-resume-download-android-sdk): When downloading large files, you can use resumable download.
