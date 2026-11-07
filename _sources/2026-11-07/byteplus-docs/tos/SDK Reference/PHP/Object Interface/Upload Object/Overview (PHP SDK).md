---
title: "Overview (PHP SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Overview-php-sdk"
---

TOS PHP SDK supports standard upload, multipart upload and other methods of uploading objects. You can choose the appropriate upload method according to your business needs and the scenarios applicable to different methods.

<span id=".5LiK5Lyg5pa55byP6K-05piO"></span>
## Upload methods


* [Standard Upload (PHP SDK)](https://docs.byteplus.com/docs/tos/Normal-upload-php-sdk): When the object size does not exceed 5 GiB, you can use the standard upload method.

* [Append Upload (PHP SDK)](https://docs.byteplus.com/docs/tos/Append-upload-php-sdk): When you need to append content to the end of an uploaded object, you can use the append upload method. The size of the appended object cannot exceed 5 GiB.

* [Multipart Upload (PHP SDK)](https://docs.byteplus.com/docs/tos/Shard-upload-php-sdk): The size of a single part cannot exceed 5 GiB, and a maximum of 10,000 parts are supported. When the object is large, use multipart upload.
