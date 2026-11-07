---
title: "Copy Object Overview (Harmony SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Overview-of-copying-objects-harmony-sdk"
---

The copyObject operation enables copying objects between buckets within the same region, as well as copying objects within the same bucket. Copy operations do not support cross\-region copying and require read permissions on the source object. TOS Harmony SDK provides two methods for object copying:


* [Standard Copy](https://docs.byteplus.com/docs/tos/Normal-copy-node-js-sdk): The size of the copied object must not exceed 5 GiB.

* [Multipart Copy](https://docs.byteplus.com/docs/tos/Sharding-copy-node-js-sdk): Except for the last part, all other parts must be at least 5 MiB in size. The part numbers for uploaded parts must be within the range [1, 10000].
