---
title: "Overview (Android SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Overview-android-sdk"
---

The TOS Android SDK supports multiple file upload methods, including simple upload and multipart upload. You may select the most suitable upload method according to your business requirements and the specific scenarios in which each method is applicable.

<span id=".5LiK5Lyg5pa55byP6K-05piO"></span>
## Instructions for Upload Methods


* [Standard Upload](https://docs.byteplus.com/docs/tos/Normal-upload-android-sdk): When the file size does not exceed 5 GiB, you may use the standard upload method.

* [Append Upload](https://docs.byteplus.com/docs/tos/Append-upload-android-sdk): Each append operation must be at least 128 KiB in size, and the total size of a single object after appending must not exceed 5 GiB.

* [Multipart Upload](https://docs.byteplus.com/docs/tos/Shard-upload-android-sdk): For large files, it is recommended to use multipart upload. Except for the final fragment, all other fragments must be at least 5 MiB in size. The numbering of uploaded fragments is also subject to a range constraint, which is [1, 10,000].

* [Resumable Upload](https://docs.byteplus.com/docs/tos/Breakpoint-resume--android-sdk): For large local files, it is recommended to use the resumable upload method, which supports concurrent uploading, progress bars, resumable transfer features, and allows configuration of concurrency level and chunk size.
