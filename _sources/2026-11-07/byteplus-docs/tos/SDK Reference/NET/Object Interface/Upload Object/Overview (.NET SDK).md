---
title: "Overview (.NET SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Overview-net-sdk"
---

In TOS, the basic data unit for operations is the object. The TOS .Net SDK offers a comprehensive range of upload methods. Below is a brief explanation of the limitations of each method.


* [Standard Upload](https://docs.byteplus.com/docs/tos/Normal-upload-net-sdk): The maximum file size must not exceed 5 GiB.

* [Additional Upload](https://docs.byteplus.com/docs/tos/Append-upload-net-sdk): The maximum file size must not exceed 5 GiB.

* [Multipart Upload](https://docs.byteplus.com/docs/tos/Shard-upload-net-sdk): For large files, multipart upload can be used, but the maximum size cannot exceed 48.8 TiB.


When uploading objects, the TOS .NET SDK supports streaming uploads. In the upload object interface, you can use a Stream as the data source to upload to a TOS bucket.
