---
title: "Overview of Copying Objects (Go SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Overview-of-copy-objects-go-sdk"
---

CopyObject enables copying objects between buckets within the same region, as well as copying objects within a single bucket. Copy operations do not support cross\-region copying and require read permission on the source object.

The TOS Go SDK provides three object copy methods:


* [Standard Copy](https://docs.byteplus.com/docs/tos/Normal-copy-go-sdk): The size of the copied object must not exceed 5 GiB.

* [Multipart Copy](https://docs.byteplus.com/docs/tos/Shard-copy-go-sdk): Except for the last part, all other parts must be at least 5 MiB in size. The part numbers for uploaded parts must be within the range [1, 10000].

* [Resumable Copy](https://docs.byteplus.com/docs/tos/Breakpoint-resumption-copy-go-sdk): Applicable for scenarios where large objects are copied within a single bucket or between two buckets in the same region using the SDK.
