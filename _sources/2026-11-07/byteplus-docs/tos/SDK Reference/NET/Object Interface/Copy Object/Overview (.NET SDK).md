---
title: "Overview (.NET SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Overview-net-sdk1"
---

CopyObject enables the copying of objects between buckets within the same region, as well as within a single bucket. Object copying does not support cross\-region operations and requires read permission on the source object.

The TOS .Net SDK provides two methods for object copying:


* [Standard Copy](https://docs.byteplus.com/docs/tos/Normal-copy-net-sdk): The size of the copy object must not exceed 5 GiB.

* [Multipart Copy](https://docs.byteplus.com/docs/tos/Shard-copy-net-sdk): Except for the last part, all other parts must be at least 5 MiB in size. The part numbers for uploaded parts must be within the range [1, 10000].
