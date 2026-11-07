---
title: "Overview of Uploading Objects (Browser.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Upload-object-overview-browser-js-sdk"
---

The TOS Browser SDK supports multiple object upload methods, including standard upload and multipart upload. You may select the most appropriate upload method based on your business requirements and the scenarios applicable to each method.

<span id=".5LiK5Lyg5pa55byP6K-05piO"></span>
## Upload methods


* [Standard Upload](https://docs.byteplus.com/docs/tos/Normal-upload-browser-js-sdk): The maximum object size cannot exceed 5 GiB.

* [Append upload](https://docs.byteplus.com/docs/tos/Append-upload-browser-js-sdk): The maximum object size must not exceed 5 GiB.

* [Multipart Upload](https://docs.byteplus.com/docs/tos/Shard-upload-browser-js-sdk): For large objects, multipart upload can be used, with a maximum size that cannot exceed 48.8 TiB.

* [Resumable Upload](https://docs.byteplus.com/docs/tos/Breakpoint-resume-upload-browser-js-sdk): Supports concurrency, resumable upload, and customizable part size. For large objects, it is recommended to use resumable upload. The maximum object size must not exceed 48.8 TiB.
