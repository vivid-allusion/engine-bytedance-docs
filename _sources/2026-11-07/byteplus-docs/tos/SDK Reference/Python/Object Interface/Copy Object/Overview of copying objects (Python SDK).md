---
title: "Overview of copying objects (Python SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Overview-of-copy-objects-python-sdk"
---

TOS SDK can copy objects between buckets within the same region or within the same bucket. Copying does not support cross\-region transfers and requires read permission on the source object.

TOS SDK offers three methods for object copying:


* [Standard Copy](https://docs.byteplus.com/docs/tos/Normal-copy-python-sdk): Copies objects up to 5 GiB in size.

* [Multipart Copy](https://docs.byteplus.com/docs/tos/Shard-copy-python-sdk): Except for the last part, each part must be at least 5 MiB; part numbers range from 1 to 10,000.

* [Resumable Copy](https://docs.byteplus.com/docs/tos/Breakpoint-continuation-copy-python-sdk): Suitable for copying large objects within a single bucket or between two buckets in the same region via the SDK.
