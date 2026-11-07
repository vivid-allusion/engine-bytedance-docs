---
title: "Overview (iOS SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Overview-ios-sdk"
---

The TOS iOS SDK supports multiple file upload methods, including simple upload and multipart upload. You may select the appropriate upload method according to your business requirements and the scenarios applicable to each method.

<span id=".5LiK5Lyg5pa55byP6K-05piO"></span>
## Instructions for Upload Methods


* [Simple Upload](https://docs.byteplus.com/docs/tos/Simple-upload-ios-sdk): When the file size does not exceed 5 GiB, you can use the Simple Upload method.

* [Append Upload](https://docs.byteplus.com/docs/tos/Append-upload-ios-sdk): When you need to append content to the end of an already uploaded object, you can use append upload. The size of the appended object must not exceed 5 GiB.

* [Multipart Upload](https://docs.byteplus.com/docs/tos/Shard-upload-ios-sdk): The size of an individual part must not exceed 5 GiB, and up to 10,000 parts are supported. When the object is large, please use multipart upload.
