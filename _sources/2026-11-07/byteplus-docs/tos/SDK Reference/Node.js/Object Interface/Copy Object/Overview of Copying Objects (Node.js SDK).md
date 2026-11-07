---
title: "Overview of Copying Objects (Node.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Overview-of-copy-objects-node-js-sdk"
---

With copyObject, you can copy objects between buckets in the same region, or within the same bucket. Copying does not support cross\-region transfers and requires read access to the original object. The TOS Node.js SDK provides three methods for copying objects:


* [Standard Copy (Node.js SDK)](https://docs.byteplus.com/docs/tos/Normal-copy-node-js-sdk):The size of the object does not exceed 5 GiB.

* [Multipart Copy (Node.js SDK)](https://docs.byteplus.com/docs/tos/Sharding-copy-node-js-sdk): Except for the last part, other parts need to be greater than or equal to 5 MiB in size, and the number range of uploaded parts is [1,10000].

* [Resumable Copy (Node.js SDK)](https://docs.byteplus.com/docs/tos/Breakpoint-resume-copy-node-js-sdk): Suitable for scenarios where large objects are copied within a single bucket or between two buckets in the same region through the SDK.
