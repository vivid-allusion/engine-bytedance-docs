---
title: "Upload object overview (Python SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Upload-object-overview-python-sdk"
---

In TOS, the basic unit of data storage is a file. The TOS Python SDK provides a rich way to upload objects.

<span id=".5LiK5Lyg5pa55byP6K-05piO"></span>
## Upload method description


* [Normal Upload (Python SDK)](https://docs.byteplus.com/docs/tos/Normal-upload-python-sdk): Upload object size does not exceed 5GiB, support progress bar, client side speed limit.

* [Append Upload (Python SDK)](https://docs.byteplus.com/docs/tos/Append-upload-python-sdk): The size of the added object cannot be greater than 5GiB, and supports progress bars and client side speed limits.

* [Shard Upload (Python SDK)](https://docs.byteplus.com/docs/tos/Shard-upload-python-sdk): Except for the last sharding, other sharding sizes need to be greater than or equal to 5MiB, the number range of the uploaded sharding is [1,10000], and it supports progress bars and client side speed limits.

* [Breakpoint Resumption (Python SDK)](https://docs.byteplus.com/docs/tos/Breakpoint-resumption-python-sdk): Support concurrency, breakpoint continuation, custom sharding size, event callback, progress bar, cancellation mechanism, this interface is recommended for large file uploads.
