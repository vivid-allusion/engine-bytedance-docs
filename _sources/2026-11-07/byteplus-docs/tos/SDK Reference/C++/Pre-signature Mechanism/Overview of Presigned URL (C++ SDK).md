---
title: "Overview of Presigned URL (C++ SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Presignature-overview-c-sdk"
---

You can add signature information to the query parameters of the URL. This URL contains information such as AK, validity period, resource, operation, and signature. Anyone who uses this URL within its validity period can perform the operation specified by the URL. This method is referred to as pre\-signature.


* [Standard Presigned URL](https://docs.byteplus.com/docs/tos/Normal-pre-signature-c-sdk): You can access the TOS service by generating a presigned link using the SDK.

* [Presigned POST Form](https://docs.byteplus.com/docs/tos/Post-form-Presignature-c-sdk): TOS supports browser\-based POST object upload requests, allowing you to upload content directly to TOS. You can use the SDK to generate presigned POST form parameters.
