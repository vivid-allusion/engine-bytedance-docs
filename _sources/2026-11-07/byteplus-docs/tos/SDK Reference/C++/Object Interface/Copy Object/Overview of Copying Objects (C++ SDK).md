---
title: "Overview of Copying Objects (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Overview-of-copy-objects-c-sdk"
---

The TOS SDK supports copying objects between buckets within the same region, as well as copying objects within a single bucket. Copying does not support cross\-region transfers and requires read permissions on the source object.

The TOS SDK provides three methods for object copying:


* [Standard Copy](https://docs.byteplus.com/docs/tos/Normal-copy-c-sdk): The size of the copied object must not exceed 5 GiB.

* [Multipart Copy](https://docs.byteplus.com/docs/tos/Shard-copy-c-sdk): Except for the final part, each of the other parts must be at least 5 MiB in size. The valid part number range for uploaded parts is [1, 10000].

* [Resumable Copy](https://docs.byteplus.com/docs/tos/Breakpoint-resume-copy-c-sdk): Suitable for scenarios where large objects are copied via SDK within a single bucket or between two buckets in the same region.
