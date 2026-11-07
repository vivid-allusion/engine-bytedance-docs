---
title: "Copy Object Overview (Browser.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Overview-of-copy-objects-browser-js-sdk"
---

The copyObject operation enables copying objects either between buckets within the same region or within the same bucket. Copy does not support cross\-region copying and requires read permission on the source object.

<span id=".5ou36LSd5a-56LGh6K-05piO"></span>
## Copy Object Description

The TOS Browser SDK provides the following object copy methods:


* [Standard Copy](https://docs.byteplus.com/docs/tos/Normal-copy-browser-js-sdk): The size of the object to be copied must not exceed 5 GiB.

* [Multipart Copy](https://docs.byteplus.com/docs/tos/Shard-copy-browser-js-sdk): Except for the last part, all other parts must be at least 5 MiB in size. The part numbers for uploaded parts must be within the range [1, 10000].

* [Resumable Copy](https://docs.byteplus.com/docs/tos/Breakpoint-resume-copy-browser-js-sdk): Applicable to scenarios where large objects are copied within a single bucket or between two buckets in the same region using the SDK.
