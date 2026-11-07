---
title: "Object Upload Overview (Harmony SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Overview-of-uploading-objects-harmony-sdk"
---

TOS Harmony SDK supports multiple object upload methods, including standard upload and multipart upload. You may select the most suitable upload method according to your business requirements and the scenarios applicable to each approach.

<span id="c2a86289"></span>
## Description of upload methods


* [Standard Upload](https://docs.byteplus.com/docs/tos/Normal-upload-node-js-sdk): The maximum object size must not exceed 5 GiB.

* [Append Upload](https://docs.byteplus.com/docs/tos/Append-upload-node-js-sdk): The maximum object size must not exceed 5 GiB.

* [Multipart Upload](https://docs.byteplus.com/docs/tos/Shard-upload-node-js-sdk): When dealing with large objects, multipart upload can be used, with a maximum size that cannot exceed 48.8 TiB.
