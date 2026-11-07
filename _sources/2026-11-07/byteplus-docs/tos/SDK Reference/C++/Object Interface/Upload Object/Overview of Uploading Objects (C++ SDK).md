---
title: "Overview of Uploading Objects (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Upload-object-overview-c-sdk"
---

The TOS C++ SDK supports multiple object upload methods, including standard upload and multipart upload. You may select the most appropriate upload method according to your business requirements and the specific scenarios in which each method is applicable.

<span id=".5LiK5Lyg5pa55byP6K-05piO"></span>
## Upload methods


* [Standard Upload](https://docs.byteplus.com/docs/tos/Normal-upload-c-sdk): The maximum object size cannot exceed 5 GiB.

* [Append Upload](https://docs.byteplus.com/docs/tos/Append-upload-c-sdk): The maximum object size must not exceed 5 GiB.

* [Multipart Upload](https://docs.byteplus.com/docs/tos/Shard-upload-c-sdk): When an object is large, multipart upload can be used; the maximum size cannot exceed 48.8 TiB.

* [Resumable Upload](https://docs.byteplus.com/docs/tos/Breakpoint-resumption-c-sdk): Supports concurrency, resumable upload, and customizable part sizes. For large objects, it is recommended to use resumable upload. The maximum object size must not exceed 48.8 TiB.
