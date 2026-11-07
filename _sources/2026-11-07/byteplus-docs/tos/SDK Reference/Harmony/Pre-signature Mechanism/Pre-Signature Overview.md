---
title: "Pre-Signature Overview"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Overview-of-pre-signature"
---

You can add signature information to the query parameters of the URL. This URL contains information such as AK, validity period, resource, operation, signature, etc. Anyone who uses this URL within the validity period can perform the operation corresponding to this URL. This method is referred to as pre\-signing.


* [Standard Pre-signed](https://docs.byteplus.com/docs/tos/Normal-pre-signature-node-js-sdk): Use the Harmony SDK to generate a pre\-signed URL, and then access TOS via the pre\-signed URL.

* [POST Form Pre-Signing](https://docs.byteplus.com/docs/tos/Post-form-presignature-node-js-sdk): TOS supports browser\-based POST object upload requests, enabling you to upload content directly to TOS. You can use the Harmony SDK to generate the POST form pre\-signed parameters.
