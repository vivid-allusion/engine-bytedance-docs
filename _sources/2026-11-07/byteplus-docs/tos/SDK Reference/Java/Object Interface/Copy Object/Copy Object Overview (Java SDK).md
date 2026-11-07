---
title: "Copy Object Overview (Java SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Overview-of-copy-objects-java-sdk"
---

The TOS SDK supports copying objects between storage buckets within the same region, as well as copying objects within a single storage bucket. Copy operations do not support cross\-region copying and require read permission on the source object.

The TOS SDK provides two object copying methods:


* [Standard Copy](https://docs.byteplus.com/docs/tos/Normal-copy-java-sdk): The size of the copied object must not exceed 5 GiB.

* [Multipart Copy](https://docs.byteplus.com/docs/tos/Shard-copy-java-sdk): Except for the last part, each part must be at least 5 MiB in size. The part numbers for uploaded parts must be within the range [1, 10000].

* [Resumable Copy](https://docs.byteplus.com/docs/tos/Breakpoint-resumption-java-sdk1): Applicable to scenarios where large objects are copied via SDK within a single bucket or between two buckets in the same region.
